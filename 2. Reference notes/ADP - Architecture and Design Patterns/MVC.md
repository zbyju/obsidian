It was first a design pattern, now it is used as an architecture / bigger picture. The implementation of is bent a lot => there is no one solid definition.

# Model
Handles business part of the application. It does:
- data validation
- main logic

# Controller
Handles user input and updates the model. It can do some validations but they should be just basic user input (e.g. checking email pattern; but model would do some advanced check if that email actually exists)

# View
Handles displaying data to the user. Typically using GUI, but not necessary - generally it's any interface the user can communicate with.

# Implementation
## 1. Controller updates View
![](https://i.imgur.com/bGUJA6K.png)

# 2. Model updating View
![](https://i.imgur.com/WnjuGqN.png)



[[Architectures]]