It is more similar to [[MVP]] rather than [[MVC]]. The communication is more straight-forward = View <-> ViewModel <-> Model.
# Model
Used for business logic.
# View
Used for GUI or other user interface.
# ViewModel
Provides data binding between model and view. It also handles most of the view display logic.

ViewModel doesn't know about View. View subscribes to ViewModel and listens for changes.

# Implementation
![](https://i.imgur.com/s1CW5Fr.png)

[[Architectures]]