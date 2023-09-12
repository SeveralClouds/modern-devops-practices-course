# Kubernetes II
*This topic is split in two parts.*

## Resources
Here are some key resources we will be covering.

### ConfigMap
The ConfigMap concept allow you to decouple configuration artifacts from image content to keep containerized applications portable. For example, you can download and run the same container image to spin up containers for the purposes of local development, system test, or running a live end-user workload.

### Secret
A Secret is an object that contains a small amount of sensitive data such as a password, a token, or a key. Such information might otherwise be put in a Pod specification or in a container image. Using a Secret means that you don't need to include confidential data in your application code.

### Jobs
A Job creates one or more Pods and will continue to retry execution of the Pods until a specified number of them successfully terminate. As pods successfully complete, the Job tracks the successful completions.

### Service
In Kubernetes, a Service is a method for exposing a network application that is running as one or more Pods in your cluster. A key aim of Services in Kubernetes is that you don't need to modify your existing application to use an unfamiliar service discovery mechanism. You can run code in Pods, whether this is a code designed for a cloud-native world, or an older app you've containerized.

## Kubernetes exercises
We will focus on the rest of the resources in this topic. Suitable exercises for beginners: [CKAD exercises](https://github.com/dgkanatsios/CKAD-exercises).

## Further reading
- "Kubernetes: Up and Running", 3rd Edition, Brendan Burns and others, O'Reilly Media, Inc., ISBN: 9781098110208
- [Kubernets docs](https://kubernetes.io/docs/concepts/overview/)
