- A design pattern and technique in which an object's dependencies (services, resources) are provided to it from an external source rather than the object creating them itself.
- Increases modularity and makes testing easier by allowing dependencies to be swapped, particularly with mocks or stubs in testing environments.

Improved Principles:
- Open/closed
- Single responsibility

*Example: Web application: a service like `EmailService` may require a connection to an email server. Instead of instantiating a specific email server connection within the `EmailService` (e.g., `new SMTPServer()`), the server instance is injected into `EmailService`—possibly defined in a configuration file or through a framework's IoC (Inversion of Control) container. This makes it easy to change the email server or to inject a mock server for testing.*