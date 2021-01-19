# The Kubernetes Book
```
book: The Kubernetes Book
date: 2021-01-15
``` 
- Pods are to kubernetes what containers are to docker. It's the basic structural unit.
- Pods may contain multiple containers but apparently that is used for more sophisticated cases.
- Pods are used to encapsulate containers. They have their own network and namespace. I think this means that containers inside a pod can communicate much like they do in a docker compose (yeah they can, localhost is defined for inside the pod).
- Prods are treated as a unit, so a pod has an ip address which means that containers inside the pod all share the same IP.
- Scaling is done by adding pods, not containers in a pod. Makes sense as it was said multi-container pods are for resource sharing.
- Controllers:  daemon sets, deployment and stateful sets.
- Pods are ephemeral and stateless, each time they die a new one spawn with different ip and ID. As such, kubernetes defines the `service` construct which acts as an `interface` to a deployment controller or daemon set controller (not sure about wording). anyway, a group of pods.
- Services provide a reliable interface as well as load balancing, managing the traffic to the available pod instances. Their attributes are: DNS name, ip address and port.

