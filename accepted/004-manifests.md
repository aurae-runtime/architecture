# Manifests

One of the main gripes about Kubernetes, is the management of YAML and the need to making the YAML turing complete with templates, logic, wrappers, and management utilities.

The YAML merely represents the specific values of an instance of a struct in Go.

We can easily adopt the "define your application in a manifest" paradigm, without actually using any of the native aurae functions to mutate a system.

### Simple Manifest

This manifest can be sourced from higher level applications, or even other aurae scripts.
Application teams will be able to define their applications directly as valid aurae code.

Notice how the application can be defined without connecting to an Aurae system, or accessing any of the subsystems at runtime.

```typescript
// ingress.aurae

let nginx = container("nginx-container-001");
nginx.image("nginx:latest");
nginx.expose(80);
nginx.env("key", "val");

let ingress = pod("ingress-001");
ingress.add(nginx);

```

### Turing Complete Logic

Application teams can easily use turing complete logical syntax for their manifests. 

If statements, conditions, loops, and more are all possible in their application definition.

```typescript
// ingress.aurae

// Define a flag to expose the pod or not.
let production = false;

let nginx = container("nginx-container-001");
nginx.image("nginx:latest");
nginx.expose(80);
nginx.env("key", "val");

let ingress = pod("ingress-001");

if production {
  ingress.expose(80); // Only expose in production
}

ingress.add(nginx);

```
