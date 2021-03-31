# Labels/Selectors

Labels are kv pairs added as meta data to resources that allow for identification, and grouping. Selectors allow a user to filter or select objects via labels. 

## Task 3 (Labels and Selectors)

In this task we will add some labels to our manifest from Task 2, so copy the content `pod_2.yml` from the previous excerise into `manifests/labels_1.yml`


1. In the `manifests/labels_1.yml` change the name of the pod to `labeled-pod` and `create` or `apply` the resource.
   
   
2. Now, using the [kubectl label] command, add the following labels to the pod
   - app_name=nginx
   - env=dev 
3. You can verify the labels were added via `kubectl get pods --show-labels`
4. In the `label_task.md` file - write the command used to add the labels to the pod.
5. Again using the [kubectl label] command remove these labels. Record the command down in the `label_task.md` file.
6. Add the labels to the `labels_1.yml` and `apply` the changes.
7. Using the [equality selector](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/#equality-based-requirement) and the [set selector](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/#set-based-requirement) run and record the `kubectl get` commands in the `label_task.md` that will do the following -
   1. using equality the command to get pods that have app_name=nginx
   2. using set the command to get pods that has app_name=nginx and env != prod
8. 
 
### Take note -
Although it might seem tedious from the command line to use selectors, labels and selectors are heavily used in higher level abstractions in kubernetes. 

Being comfortable with using them is also highly helpful when trying to filter/find resources in a kubernetes environment with alot of running things.

---

[kubectl label]: https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#label
