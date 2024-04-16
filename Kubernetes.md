The master node has these 5 services

- APT Server (Application programming interface, send req & get responce, Take the req from outside world
- ETCD (store key value)(database)
- controller  (maintains desired state of the workload, desire dstate = actual stae of the workload)
- scheduler ( is responsible to schedule the work load to desired host)
- Kubelet (it interfaces with CRE and it also ensures that the health of the work load is good

 <u>Worker node services</u>

- kubelet ( this is like a manger talks with container)
- kube-proxy (
- container run time engine


**INSTALLATION : VIDEO 1 - 1:29:00**

- K8 wont support SWAP so we have to disable the SWAP for k8

<u>packages</u>

- Kubeadm - Admin related cammands on k8
- Kubectl - Is the command line for managing the entire k8 environment
- Kubernetes-cni - it is used for networking (kube proxy installed form this package only )

- to create a cluster in k8 we have to make a node master, without masternode we cant create a cluster

- In K8 containers are always creadted in a POD.
 
- POD is a cover for containers
- in a pod multiple containers can exist, but there will be a one main container and all others are helper conatiners

**how to create a POD there are 2 methods**

- Declarative via ymil file
- imparative via CLI file


- all  the operation task related to k8 is done using kubectl command
- any cluster related actions not the pod kubeadm

**To create a pod**

- $ kubectl run (pod-name) --image (imagename like nginx)
- to check list of pods = kubectl get pod
- to go inside the pod= $ kubectl exec -it (pod name)  /bin/sh
- to come out from the POD = type exit
- to get more info about the POD = $ kubectl describe pod (pod_name)


###############################################################################################

#### VIDEO 2

- to check the status of node = $ kubectl get node
- more detailed info about node = $ kubectl get node -o wide (or) $ kubectl describe node
- to get more info about POD = $ kubectl get pods -o wide
- to get more info about specific one pod = $ kubectl describe pod pod_name
- to get all commands of k8 = $ kubectl --help


* <u>Kubectl commands $</u> *
- create = use for first time creation
- run = to craete pods using cli
- expose = use to expose the ports
- apply = to make changes of exist file
- exec = use to connect inside the container
- kubectl cluster-info = to get the cluster health/performance
                            
- Declarative approach required a Yaml file

- indentation = plain spaces no tab

<u>to write yaml file : $ vi filename.yaml</u>

-  to write a yaml file there are 4 important things
1.api verison
2.kind (defind what you are craeting ex:pod)
3.meta data (its a data about data,name of the pod,it will also contain more info)
4.specification (what are the specification of the pod define about your pod parts)

- defines/denotes ARRAY

**to apply created yaml file = $ kubectl apply -f filename.yaml**

Indentation format:


- defines/denotes ARRAY


apiVersion: v1
kind: Pod
metadata:
   name: monday
spec:
   containers:
    - name: apple
      image: nginx
    - name: banana
      image:  mariadb

to delete a pod = $ kubectl delete pod pod_name
              
**image pull policy there are 3**

1.default (pull from internet)
2.if not present (this is the best one, it has 2 ways to pull)
3.never (never pull from internet)

**example:**

apiVersion: v1
kind: Pod
metadata:
   name: monday
spec:
   containers:
    - name: apple
      image: nginx
      imagePullPolicy:  IfNotPresent

$ Kubectl replace --force -f podname.yaml   (delete existing file and recreates automatically)

                       ## LABELS

- to list the lables of any pod = $ kubectl get pods --show-labels
- to add a label to the pod = $ kubectl label pod pod_name custom_label_name
- to delete a pod's label = $ kubectl label pod po_name run/app- (select which label you want to delete run's or app's )
- to overwrite a pod's label = $ kubectl label pod pod_name --overwrite app/run=new_label_name


 **labels can be used by selectors**

                         ## selector

 to get the all pods which is labeled as raja = $ kubectl get pods --selector app/run=raja

<u>two type selectors</u>

1.**equality** ( equal to = or not equal to !=
ex: app =mywebapp ( these selctor shows which is equal to =)
     app !=mywebapp (these selector shows which is not equal to !=)
$kubectl get pods --selector app/run !=label_name --show-labels

2.**set_base_selector** there are 2 operators

      in and not in  operators
**this is for IN**
$kubectl get pods --selector 'fruit/app/run in(label name1, label name 2)'

**this is for NOT IN**
$kubectl get pods --selector 'fruit/app/run notin(label name1, label name 2)'


(2:09:30 - stoped video)

**always pod version is v1**

- to know more about the pod use
$ kubectl explain pod

- labels are applicator to only pods


                     **REPLICA (group of POD's)**

<u>There are 2 types of replica's</u>

1.replication controller (based on equality labels)
2.Replica set (based on both equality and set based labels)

- replica helps to create multiple copys of the pods






























