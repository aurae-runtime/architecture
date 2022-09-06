# Workloads

This architecture document calls out a proposal for how workloads should be managed and ran within aurae.

### Pods

I am convinced that the best way to represent a workload with Aurae is to continue to use the Kubernetes **Pod** terminology.
However unlike Kubernetes, Aurae Pods will be composed of the most fundamental runtime unit: a process, or a "proc".

Pods are designed to be as isolated as possible by default. Aurae and subsequent Pods will be designed with the assumption that all other Pods in the system will be owned by unknown application owners.
In other words, pods are multi-tenant by default.

### Process Types

A process can be one of the following types:

| Proc Type   | Description                                                                                     |
|-----------	|------------------------------------------------------------------------------------------------	|
| Exec      	| A system executable process, such as a binary or command line program.                         	|
| Container 	| A system container running in a cgroup namespace, such as a docker container.                  	|
| MicroVM   	| A system container running with an application specific kernel, such as a firecracker microvm. 	|

Pods have a few constraints with regard to process types.

 - A pod must contain the same process types.
 - A pod must contain only a single `MicroVM`.

## Subsystems

This proposal begins to form the first 2 subsystems of Aurae:

 - Runtime
 - Observe

Each subsystem will have independent access control at the function level.


### Example: Single Container Pod

This script would replace a traditional `nginx.yaml` style manifest. 

```typescript

about();

let aurae = connect();
let runtime = aurae.runtime();
let observe = aurae.observe();

// Define a container
let nginx = container("nginx-container-001");
nginx.image("nginx:latest");
nginx.expose(80);
nginx.env("key", "val");

// Add to a Pod
let ingress = pod("ingress-001");
ingress.add(nginx);

// Run the pod
runtime.run(ingress);

// Tail the logs
observe.logs(ingress);

```

### Example: Single MicroVM Pod

Run an even more isolated workload with aurae.

```typescript

about();

let aurae = connect();
let runtime = aurae.runtime();
let observe = aurae.observe();

// Define a microvm
let isolated = microvm("my-isolated-workload-001");
isolated.image("mycorp/application:latest");

// Add to a Pod
let sandbox = pod("sandbox-001");
sandbox.add(isolated);

// Run the pod
runtime.run(sandbox);

// Tail the logs
observe.logs(sandbox);

```

### Example: A Group of Executables

Group together a set of system executables that run without a container or microvm runtime.

```typescript

about();

let aurae = connect();
let runtime = aurae.runtime();
let observe = aurae.observe();

// Define 1st executable
let execA = exec("my-daemon");
execA.cmd("/bin/daemon");
execA.flag("--verbose", "true");
execA.arg("--daemon");
execA.arg("--watch");

let execB = exec("my-util");
execB.cmd("/bin/util");

// Add to a Pod
let sysUtil = pod("system-util-001");
sysUtil.add(execA);
sysUtil.add(execB);


// Run the pod
runtime.run(sysUtil);

// Tail the logs
observe.logs(sysUtil);

```

