
**These are claude-generated templates for UCAP convertors.**
# UCAP OneToOne template

For a transformation with **one input subscription → one output property**. No event builder needed.

## Device definition JSON

```json
{
  "$schema": "https://ucap-docs.web.cern.ch/device_schema.json",
  "ucapJsonSchemaVersion": "v3",
  "name": "SPS.MY.DEVICE",
  "description": "One-line summary of what this device does.",
  "transformations": [
    {
      "type": "OneToOne",
      "name": "MyTransformation",
      "description": "What this transformation does.",
      "subscription": {
        "parameter": "INPUT.DEVICE/Property",
        "selector": "SPS.USER.SFTPRO1",
        "ignoreErrors": false,
        "ignoreFirstUpdates": false
      },
      "converter": {
        "language": "Python",
        "className": "my_pkg.converters.my_module.MyConverter",
        "configuration": {
          "threshold": 42
        }
      },
      "publishedProperty": "MY_RESULT"
    }
  ]
}
```

### Knobs to tune

| Field | What to consider |
|---|---|
| `subscription.parameter` | `DEVICE/Property` or `DEVICE/Property#field` (subscribe to one field only) |
| `subscription.selector` | Include for **PPM** properties; omit entirely for **non-PPM** (settings, status). Wildcards OK: `SPS.USER.SFT*`. |
| `subscription.alias` | Optional. Not used in OneToOne (only one input), but harmless. |
| `subscription.ignoreErrors` | `true` to swallow upstream exceptions before they reach `convert()`. |
| `subscription.ignoreFirstUpdates` | `true` to drop the cached value JAPC delivers at subscribe time. Don't enable for rarely-publishing sources. |
| `converter.configuration` | Free-form dict; read in `convert()` via `self.configuration["key"]`. |
| `publishedProperty` | Singular. Must match the `parameter_name` you build in your `AcquiredParameterValue`. |

## Python converter (class-based)

```python
import logging

from ucap.common import (
    FailSafeParameterValue,
    AcquiredParameterValue,
    ParameterException,
    ValueType,
)
from ucap.common.converter import OneToOneConverter


class MyConverter(OneToOneConverter):

    def configuration_post_processing(self) -> None:
        # Runs once at load. self.configuration is populated.
        self._threshold = float(self.configuration["threshold"])

    def __init__(self):
        super().__init__()
        # State retained across convert() calls
        self._last_value = None

    def convert(
        self,
        input_value: FailSafeParameterValue,
    ) -> FailSafeParameterValue | None:
        logger = logging.getLogger(__name__)

        # 1. Handle exceptions
        if input_value.exception:
            logger.warning(
                f"Upstream exception: {input_value.exception.message}"
            )
            return None  # publish nothing this cycle

        # 2. Extract input
        apv = input_value.value
        assert apv is not None
        x = apv.get_value("field_name")
        # Or, if subscribed with #field, no field arg:
        # x = apv.get_value()

        # 3. Apply logic / filtering
        if x < self._threshold:
            return None

        # 4. Build output, carrying input's header through
        out = AcquiredParameterValue(
            f"{self.device_name}/{self.published_property_name}",
            value_header=apv.header,
        )
        out.update_value("result", float(x), ValueType.FLOAT)

        return FailSafeParameterValue(out)
```

## Python converter (function-based, simpler)

```python
from ucap.common import (
    FailSafeParameterValue,
    AcquiredParameterValue,
    ValueType,
)
from ucap.common.context import (
    device_name,
    published_property_name,
    configuration,
)


def convert(
    input_value: FailSafeParameterValue,
) -> FailSafeParameterValue | None:
    if input_value.exception:
        return None

    apv = input_value.value
    x = apv.get_value("field_name")
    if x < configuration["threshold"]:
        return None

    out = AcquiredParameterValue(
        f"{device_name}/{published_property_name}",
        value_header=apv.header,
    )
    out.update_value("result", float(x), ValueType.FLOAT)
    return FailSafeParameterValue(out)
```

For function-based, point `converter.className` at the **module** path (e.g. `my_pkg.converters.my_module`), not a class. UCAP discovers the `convert` function at module scope.

## Publishing an upstream exception

```python
return FailSafeParameterValue(
    ParameterException(
        f"meaningful message: x={x}",
        f"{self.device_name}/{self.published_property_name}",
    )
)
```

## Variant: OneToMany

Same shape, but `type: "OneToMany"`, `publishedProperties: ["A", "B"]`, and return `list[FailSafeParameterValue]` (one per output property, with matching `parameter_name`).

```python
def convert(self, input_value) -> list[FailSafeParameterValue]:
    apv = input_value.value
    out_a = AcquiredParameterValue(f"{self.device_name}/A", value_header=apv.header)
    out_a.update_value("v", apv.get_value("field1"), ValueType.FLOAT)
    out_b = AcquiredParameterValue(f"{self.device_name}/B", value_header=apv.header)
    out_b.update_value("v", apv.get_value("field2"), ValueType.FLOAT)
    return [FailSafeParameterValue(out_a), FailSafeParameterValue(out_b)]
```

`return []` to publish nothing on a given cycle.

# UCAP EventToOne template

For a transformation with **several input subscriptions → one output property**. Requires an event builder.

The example below uses `SubscriptionTriggered` (one trigger + buffered context), which is the most common shape. See bottom of file for variations.

## Device definition JSON

```json
{
  "$schema": "https://ucap-docs.web.cern.ch/device_schema.json",
  "ucapJsonSchemaVersion": "v3",
  "name": "SPS.MY.DEVICE",
  "description": "One-line summary.",
  "transformations": [
    {
      "type": "EventToOne",
      "name": "MyTransformation",
      "description": "What this transformation does.",
      "event": {
        "type": "SubscriptionTriggered",
        "trigger": {
          "subscription": {
            "parameter": "TRIGGER.DEVICE/Acquisition",
            "selector": "SPS.USER.SFTPRO1",
            "alias": "trig"
          }
        },
        "bufferedSubscriptions": [
          {
            "parameter": "CONTEXT.DEVICE.A/Acquisition",
            "selector": "SPS.USER.SFTPRO1",
            "alias": "a",
            "bufferSize": 1
          },
          {
            "parameter": "CONTEXT.DEVICE.B/Setting",
            "alias": "b"
          }
        ]
      },
      "converter": {
        "language": "Python",
        "className": "my_pkg.converters.my_module.MyConverter",
        "configuration": {
          "threshold": 42
        }
      },
      "publishedProperty": "MY_RESULT"
    }
  ]
}
```

### Knobs to tune

| Field | What to consider |
|---|---|
| `event.type` | `SubscriptionTriggered`, `CombiningLatestValues`, `GroupTriggeredCycleStampGrouped`, `FixedIntervalTriggered`, `Scheduled`, etc. — pick from the decision flow in `ucap-basics.md`. |
| `trigger.subscription` | The one subscription whose arrival fires `convert()`. Has its own selector/PPM rules. Set `alias` for clean access (`event.trigger_value` is also available without alias). |
| `bufferedSubscriptions[]` | Everything else. Latest N values held in memory (default N=1). Each has its own selector. |
| `bufferedSubscriptions[].bufferSize` | Default 1. Increase to N if your converter needs history. |
| `bufferedSubscriptions[].timestampSortType` | `NO_SORTING` (default), `ACQ_STAMP`, `CYCLE_STAMP`. Sorted buffers reject late values when full. |
| `bufferedSubscriptions[].ignoreErrors` / `ignoreFirstUpdates` | Same semantics as OneToOne. |
| `bufferedBySelectorSubscriptions` | (Alternative block) Same as buffered but with one buffer **per selector** — for per-user setting lookup. |

## Python converter (class-based)

```python
import logging

from ucap.common import (
    FailSafeParameterValue,
    AcquiredParameterValue,
    Event,
    ValueType,
)
from ucap.common.converter import EventToOneConverter


class MyConverter(EventToOneConverter):

    def configuration_post_processing(self) -> None:
        self._threshold = float(self.configuration["threshold"])

    def __init__(self):
        super().__init__()
        self._last_value = None

    def convert(self, event: Event) -> FailSafeParameterValue | None:
        logger = logging.getLogger(__name__)

        # 1. Get the trigger value
        trig = event.trigger_value
        if trig.exception:
            logger.warning(f"Trigger exception: {trig.exception.message}")
            return None

        # 2. Get context values (by alias)
        a_fspv = event.get_value("a")
        b_fspv = event.get_value("b")

        if a_fspv.exception or b_fspv.exception:
            return None

        # 3. Extract fields
        x = trig.value.get_value("field_in_trigger")
        a = a_fspv.value.get_value("field_in_a")
        b = b_fspv.value.get_value("field_in_b")

        # 4. Logic
        if x < self._threshold:
            return None

        result = float(x) * float(a) + float(b)

        # 5. Build output, carrying trigger's header
        out = AcquiredParameterValue(
            f"{self.device_name}/{self.published_property_name}",
            value_header=trig.value.header,
        )
        out.update_value("result", result, ValueType.FLOAT)
        return FailSafeParameterValue(out)
```

## Useful Event API calls

| Call | Returns |
|---|---|
| `event.trigger_value` | trigger's `FailSafeParameterValue` (only with `SubscriptionTriggered*`) |
| `event.trigger_name` | trigger's alias |
| `event.get_value("alias")` | latest FSPV for that alias |
| `event.get_values("alias")` | all buffered FSPVs (oldest → newest) |
| `event.get_value("alias@SPS.USER.SFTPRO1")` | bufferedBySelector lookup |
| `event.get_plain_value("alias", "field")` | unwrap to Python scalar; raises `ValueError` on miss |
| `event.timeout_reached` | True ⇒ partial event (Group*Triggered builders only) |
| `event.missing_value_names` | aliases whose data didn't arrive |

## Function-based variant

```python
from ucap.common import (FailSafeParameterValue, AcquiredParameterValue, Event, ValueType)
from ucap.common.context import device_name, published_property_name, configuration


def convert(event: Event) -> FailSafeParameterValue | None:
    trig = event.trigger_value
    if trig.exception:
        return None
    a = event.get_plain_value("a", "field_in_a")
    out = AcquiredParameterValue(f"{device_name}/{published_property_name}",
                                 value_header=trig.value.header)
    out.update_value("v", float(a), ValueType.FLOAT)
    return FailSafeParameterValue(out)
```

`converter.className` points at the **module path** for function-based.

## Event-builder variations

### `CombiningLatestValues` — fire on any input, snapshot all latest

```json
"event": {
  "type": "CombiningLatestValues",
  "bufferedSubscriptions": [
    {"parameter": "DEV.A/Acquisition", "selector": "SPS.USER.SFTPRO1", "alias": "a"},
    {"parameter": "DEV.B/Setting", "alias": "b"},
    {"parameter": "DEV.C/Acquisition", "selector": "SPS.USER.SFTPRO1", "alias": "c"}
  ]
}
```

No `trigger`. In the converter, no `event.trigger_value` — use `event.get_value("a")` for each. Watch out for partial / stale data on the first few fires.

### `GroupTriggeredCycleStampGrouped` — all of a group, aligned by cycle

```json
"event": {
  "type": "GroupTriggeredCycleStampGrouped",
  "triggerGroup": {
    "subscriptions": [
      {"parameter": "MAGNET.1/Acquisition", "selector": "PSB.USER.ALL"},
      {"parameter": "MAGNET.2/Acquisition", "selector": "PSB.USER.ALL"}
    ],
    "timeoutMs": 1000
  },
  "bufferedSubscriptions": [
    {"parameter": "LSA.DEVICE/Setting", "alias": "lsa"}
  ]
}
```

In the converter, check `event.timeout_reached` to decide if you got a partial event; `event.missing_value_names` tells you which.

### `FixedIntervalTriggered` — periodic, no subscription drives timing

```json
"event": {
  "type": "FixedIntervalTriggered",
  "intervalMs": 1000,
  "bufferedSubscriptions": [
    {"parameter": "DEV.A/Acquisition", "selector": "SPS.USER.SFTPRO1", "alias": "a"}
  ]
}
```

### `Scheduled` — cron-driven

```json
"event": {
  "type": "Scheduled",
  "cronExpression": "0 0 6 * * ?",
  "bufferedSubscriptions": [
    {"parameter": "DEV.A/Setting", "alias": "a"}
  ]
}
```

(Cron is Quartz format: `sec min hour day-of-month month day-of-week`.)

## Variant: EventToMany

Same shape with `type: "EventToMany"`, `publishedProperties: ["A","B"]`, and `convert()` returns `list[FailSafeParameterValue]` (one per output property). Return `[]` to publish nothing.

