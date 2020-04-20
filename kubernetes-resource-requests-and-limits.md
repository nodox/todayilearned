# Kubernetes resource requests and limits

Today I learned. In Kubernetes CPU is considered a “compressible” resource. If your app starts hitting your CPU limits, 
Kubernetes starts throttling your container. This means the CPU will be artificially restricted, 
giving your app potentially worse performance! However, it won’t be terminated or evicted. 
You can use a liveness health check to make sure performance has not been impacted.

However, memory cannot be compressed. Because there is no way to throttle memory usage, 
if a container goes past its memory limit it will be terminated. If your pod is managed 
by a Deployment, StatefulSet, DaemonSet, or another type of controller, then the controller spins up a replacement.

Another thing to keep in mind about CPU requests is that if you put in a 
value larger than the core count of your biggest node, your pod will never be scheduled. Let’s say you have a pod
that needs four cores, but your Kubernetes cluster is comprised of dual core VMs—your pod will never be scheduled!

Just like CPU, if you put in a memory request that is larger than the amount of memory on your nodes, 
the pod will never be scheduled.

## Source
- https://cloud.google.com/blog/products/gcp/kubernetes-best-practices-resource-requests-and-limits

Tags
- kubernetes
