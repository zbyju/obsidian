It is an evolution of [[MVC]] to improve separation of concerns and facilitate automatic unit testing.
# Model
Manages data and business logic of the application.
# View
Display the data to the user and relays user actions to the Presenter
# Presenter
Acts as a middle layer between the View and the Model. It retrieves data from the model and formats them for the View.

# Implementation
![](https://i.imgur.com/NfGAcJH.png)

View and presenter are coupled together and work together. Presenter only works with an **interface of View**.

[[Architectures]]