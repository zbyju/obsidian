It's a language for describing and validating RDF graphs against constraints.

It uses these terms:

# Shape
Defines how to validate a *Focus Node* based on values of properties.

# Focus Node
RDF term that is validated against a Shape (URI, literal, blank node).

# Node Shape
Specifies constraints that need to be met with respect to Focus Nodes.
(Directly on the node)

# Property Shape
Specify constraints that need to be met with respect to nodes that can be reached from the Focus Node.
(Connected to the node)

# Targets
T