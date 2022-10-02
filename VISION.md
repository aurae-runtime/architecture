# Aurae Vision

The Aurae Project intends to make the right path, the easy path for application teams. 

I started not by asking what the industry was doing that seemed to be working, but rather asking the industry what they would chose to do again if given the chance to start over.
My findings were surprising as I uncovered common themes.

### Guiding Principles 

Simplicity and opinions were the words I found myself repeating. I have taken these concepts and formed a number of actionable guiding principles.

#### Opinionated Defaults, With Optional Replacements

The Aurae standard library is a reflection of things people do, not things computers need.
A problem with Kubernetes is that its flexibility became it's dysfunction. The system was vastly flexible, and vastly unopionated.
Forming and holding an opinion on the implementation detail in Kubernetes became an unwritten ritual in building every aspect of a platform.

Aurae reverses this paradigm. Aurae will form and maintain an opinion on what it considers to be sane, reasonable, and secure default opinions.
These opinions, like all aspects of Aurae, will be modular and extensible.

Each subsystem of Aurae will come with a default implementation that is completely replacable.

#### Less is More

When in doubt, simplify.

Hold a thoughtful and validated opinion. The project prefers pleasant surprises in favor of counter productive magic.
We never let a feature get in the way of usefulness. 

We prefer a single function with a powerful paradigm in favor of extension and modularity. Be thoughtful, but do not let thoughts stand between the user and elegance.

#### Organic Libraries

We prefer organic libraries over mechanistic structure. Expose what people need, however keep the core well structured. 
As the needs of the project grows we must carefully consider our APIs and do our best to prevent ourselves from re-creating POSIX and confusing systemcalls.

#### Dialtone Security

Aurae is designed to be a Distributed Operating System and act as a responsible `PID 1/init`.

Security is something we should not compromise on. If Aurae is online, it must be default secure, and easy to keep secure by making doing the right thing either built-in, or straight forward and well documented.

Every organization's threat model and appetite for risk is unique. Aurae is designed to mitigate risk through its architecture and implementation decisions.

Decisions in Aurae are simple and transparent, allowing you to examine and understand the risk of Aurae and how it integrates with workloads under its control.
