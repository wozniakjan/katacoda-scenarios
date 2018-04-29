## Kubernetes introduction

[Kubernetes](https://kubernetes.io/docs/tutorials/kubernetes-basics/) is system that orchestrates containers and services on multiple node clusters. As an administrator, you declare how you want the environment to look and kubernetes tries to make the real environment as close to your declaration as possible. One way to send information to your cluster is with `kubectl create -f xyz.yaml` where xyz.yaml is a file where you declared some of the objects. This will send information to the [API
server](https://kubernetes.io/docs/reference/generated/kube-apiserver/) and [controllers](https://kubernetes.io/docs/concepts/overview/components/#kube-controller-manager) will pick that information up and trigger some action.

[Pod](https://kubernetes.io/docs/concepts/workloads/pods/pod/) is a basic building block in kubernetes world. Just like any other object, it is commonly defined in declarative format structured as [YAML](https://en.wikipedia.org/wiki/YAML) or [json](https://en.wikipedia.org/wiki/JSON).

Your kubernetes environment is split into multiple [namespaces](https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/) (these are different from previously mentioned [linux namespaces](https://en.wikipedia.org/wiki/Linux_namespaces)).

Make sure kubernetes is up and running, then take a look at namespaces and create one new for your task. Then set your new namespace to be your default for subsequent commands.

```
launch.sh
kubectl get namespaces
kubectl create namespace test
kubectl config set-context $(kubectl config current-context) --namespace=test
```{{execute}}

##### Question 2.
Are you familiar with linux shell? What does `$()` do?

A command can be executed accross all namespaces as well. This is a set of useful commands when dealing with pods.

```
kubectl get pods --all-namespaces
kubectl get pods --all-namespaces -o wide
kubectl describe pod -n kube-system etcd-master
```{{execute}}

##### Task 2.

Inspect `pod.yaml`. There are two things wrong with it and you should find and fix them. Ideally your pod will expose the same web service from first part of the lesson accessible via `curl [POD_IP]:[POD_PORT]`

Lets start with
```
kubectl create -f pod.yaml
kubectl describe pod pod1
```{{execute}}
The output provides a lot of information, can you spot the error? Call a teacher if you need some help.
You may want to take a look at the documentation https://kubernetes.io/docs/user-guide/walkthrough/#pod-definition

When dealing with pods, delete and recreate from edited file again is usually the simplest
```
kubectl delete pod pod1
kubectl create -f pod.yaml
```{{execute}}

You can also edit some properties in already existing pod1 with
```
kubectl edit pod pod1
```{{execute}}

But due to the fact a lot of pod properties are immutable, you will find this command more useful in next labs when dealing with other kubernetes objects

