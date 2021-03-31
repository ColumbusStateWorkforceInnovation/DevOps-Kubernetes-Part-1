# Pods

### refresher
- Pods serve as the atomic unit in kubernetes. 
- It is the single unit of work. When containers are run the containers are assigned to pods.
- We can deploy one or more containers in a pod, and mount volumes to containers within a pod

## Task 1 (Single Pod)

Your first task is to update a manifest file the following properties:

1. Open the `manifests/pod_1.yml` file 
2. Update it so the resource is type kind `Pod` using the image -  `nginx:stable-alpine`
3. Name the pod should be `pod-nginx`
4. Name the container `nginx`
5. Open port `80` for the container
   
- Save the `manifests/pod_1.yml`.
- Use `create` or `apply` the manifest file
  - Save the command you used to create the pod in the `pod_task.md` file
- Verify the pod is deployed using the `describe` or `proxy` command
  - Record the command you used to verify in the `pod_task.md` file
  - if using the `proxy` command also record the url you used to view the pod.

---

## Task 2 (Multi Pod with Volume mount)

In this task we will be adding a second container to the pod and mounting a volume with content.


In the `manifests/pod_2.yml`, add an additional update the manifest with the following properties:

1. Change the name of the pod to `multi-pod-volume-nginx`
2. Add a volume called `html-content` using an `emptyDir`
3. Add a second container to the pod using the image -  `alpine:latest`
   -  The name of the container should be `pod-content`
4. On the `nginx` container add a `volumeMount`
   - mount the created `html-content` volume to the pod using `/user/share/nginx/html` as the `mountPath`
5. Similarly on the `pod-content` container add a `volumeMount`
   - mount the created `html-content` volume to the pod using `/html` as the `mountPath`
6. On the `pod-content` container add a `command` with value `["/bin/sh", "-c"]`
7. On the `pod-content` and to `args` the following code:
  
  ```
while true; do
    echo "current time<br/>"$(date)"<br/>" >> /html/index.html;
    sleep 5;
done
   ```
   
- Save the manifest file.
- Use `create` or `apply` the manifest file
- Using `proxy` visit the url for this pod
- In `pod_task.md` breifly describe how the containers are working together to display what you see on the browser.

delete the pod using the `kubectl delete` command.

---
