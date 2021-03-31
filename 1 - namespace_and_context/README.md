
# namespaces and context

In kubernetes, namespaces are logical partitions of a cluster or environment. Its primary use is to scope access, or partition a cluster.

For example we might want to partition our cluster with a development namespace, a test namespace, and a prod namespace.

  Lets get the current namespaces - 

```
$ kubectl get namespaces
```

Create a new namespace 

```
$ kubectl create namespace dev
```


To make things easy lets look at all the contexts we have then create a context for this namespace - 

```
$ kubectl config get-contexts
```

you should see something like:

```
$ kubectl config get-contexts

CURRENT   NAME       CLUSTER    AUTHINFO   NAMESPACE
*         minikube   minikube   minikube   
```

Lets make a new context within our minikube environment with our dev namespace and use the same minikube user.

```
$ kubectl config set-context kubedev --cluster=minikube --namespace=dev --user minikube
```

Now when running  `kubectl config get-contexts`, we should see our new context.

```
$ kubectl config get-contexts

CURRENT   NAME       CLUSTER    AUTHINFO   NAMESPACE
          kubedev    minikube   minikube   dev
*         minikube   minikube   minikube   

```

Now lets switch to this context.

```
$ kubectl config use-context kubedev
```

Now that we have a context we can switch between them easily. In a real environment I might have a context for each namespace.

Creating namespaces serve has providing scope to names, and access to resources.

---