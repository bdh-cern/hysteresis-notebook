
# Tips

- Signals emitted by an object are declared on the class level. During execution, PyQt finds them and integrates them into its C++ structure.
- Layouts and widgets:
	- A layout is an element of geometry management. Widgets added to them end up in a list. The layout object manages to the layout of the elements in this list
	- A widget is something which is displayed to the user which contains its own geometry. Only a widget can be a parent or child of other widgets.
- A parent widget owns its child widgets. Child widgets are clipped inside the area of their parents. The parent provides the surface for drawing the children.
- Each widget owns one layout (which arranges its children) and is a member of one layout (that of its parent).
	- Violation of this rule in code will result in a warning and correction by PyQt.k