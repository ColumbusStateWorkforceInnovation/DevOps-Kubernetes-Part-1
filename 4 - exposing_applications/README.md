# Exposing applications with Services

## **Note - You will need the pods from the previous task running to complete this task**

Before starting this task -

1. Create the pod `pod-nginx` from the first task. (pod_1.yml)
2. Add the label `app_name=nginx` to the `pod-nginx` pod using what we learned in Task 3
3. Create the pod `labeled-pod` from third excerise (label_1.yml).
4. Verify you have done this by running `kubectl get pods --show-labels`
   - you should see something like:
    ```
    NAME          READY   STATUS    RESTARTS   AGE   LABELS
    labeled-pod   2/2     Running   0          33m   app_name=nginx,env=dev
    pod-nginx     1/1     Running   0          27s   app_name=nginx
    ```

Use this [service-reference](https://kubernetes.io/docs/concepts/services-networking/service/) for the next two tasks.

---
## Task 4 - (Cluster IP)

In this task you will create a service using `clusterIP`.

1. You will be updating the `manifests/cluster-ip-service.yml` file
2. Create a Service of type `ClusterIP` and call the service `nginx-service`
    - note: what is the default `type` for a object of `kind` == `Service`
3. Expose the app from our previous task `nginx` using the `app_name` label and expose it at port 80, with the TCP protocol
   - hint : you will use the `selector` field in the manifest
4. `create` or `apply` the manifest.  
5. run `kube proxy` and visit the url of the service at  http://127.0.0.1:8001/api/v1/namespaces/dev/services/nginx-service/proxy/ in your browser or using curl
6. Refresh the browser, or execute curl multiple times
7. Describe what is happening and what you see in the `expose_tasks.md`

### notes -
ClusterIP is the most common way to expose application in kubernetes, and is how pod/services are consumed within kubernetes. Remember that the service is a static IP abd DNS entry that maps to pods.

---
## Task 5 - (NodePort)

In this task we will expose our application using the `NodePort` object. Like before you will need the pods from before (pod_1.yml and label_1.yml), please refer to the note in Task 4 to get it setup if you deleted them.

1. You will be updating the `manifests/nodeport-service.yml`
2. Update the manifest so that it is a `Service` of type `NodePort` with name `nodeport-nginx`
3. Similar to Task 4, expose our pods at port `80` using the selector for `app_name=nginx` and `env=dev` with the `nodePort` equal to `32410`
4. `create` or `apply` the manifest. 
5.  Run the command `minikube service -n dev nodeport-nginx`
6.  Under Question 2 in the `expose_task.md` desribe the behavior you see, then explain the *why* you think it is different than what we saw in Task 4

---