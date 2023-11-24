Given the recommended utilization of WSL for Windows users, I've crafted a user-friendly tutorial to facilitate the initiation of tasks using the Windows Subsystem for Linux. This is particularly beneficial because accessing and editing files from the Linux subsystem can be more challenging when the primary Pipeline directory is located within Linux.
As Kubectl has been downloaded, there is no necessity to install Minikube separately. 

Some extra commands to know before starting:\
***IF YOU WANT TO CODE INSIDE YOUR PIPELINE DIRECTORY BUT IT IS INSIDE LINUX, THEN CHANGE DIRECTORIES TILL YOU REACH YOUR PIPELINE DIRECTORY, THEN USE ```$ code .``` 
This should automatically open up the pipeline directory inside VSCode so you can edit whatever you want to.***

***If you want to view your changes to the file and make sure the contents are correct, then you can use:\
```$ cat filename``` i.e. filename being the file that you want to observe the contents of.\
If you want to remove a file because you misspelled the file name, then you can use:\
```$ rm -rf filename```***

First to install the latest version of Tekton Pipelines use kubectl: 
```$ kubectl apply --filename \ https://storage.googleapis.com/tekton-releases/pipeline/latest/release.yaml```


After this we are able to monitor the installation using: 
```$ kubectl get pods --namespace tekton-pipelines --watch```

Wait for ```tekton-pipelines-controller``` and ```tekton-pipelines-webhook``` to show 1/1 under the READY column, then you can proceed to creating and running a basic task. 
```
NAME                                           READY   STATUS              RESTARTS   AGE
tekton-pipelines-controller-6d989cc968-j57cs   0/1     Pending             0          3s
tekton-pipelines-webhook-69744499d9-t58s5      0/1     ContainerCreating   0          3s
tekton-pipelines-controller-6d989cc968-j57cs   0/1     ContainerCreating   0          3s
tekton-pipelines-controller-6d989cc968-j57cs   0/1     Running             0          5s
tekton-pipelines-webhook-69744499d9-t58s5      0/1     Running             0          6s
tekton-pipelines-controller-6d989cc968-j57cs   1/1     Running             0          10s
tekton-pipelines-webhook-69744499d9-t58s5      1/1     Running             0          20s
```

Navigating the creation of files and similar tasks within Linux poses a challenge, complicating the original tutorial, especially for those using WSL users. Therefore, **assuming the Pipeline directory is inside your Linux home directory**, we should be able to solely use Linux commands to work through creating and running tasks.

First, navigate to your pipeline directory:\
```$ cd ~ ```\
then:\
```$ cd pipeline```\
Then subsequently, write ```$ touch hello-world.yaml``` in your command line and press enter. This command should create a file named ```hello-world.yaml``` inside the directory you are currently in, which should be the pipeline directory. Now that the file has been created, we can edit and paste the following content into the ```hello-world.yaml``` file.\
To do so we can use the nano command to write inside the file:\
```$ nano hello-world.yaml```
Then you can paste the following content below into the file:
```
apiVersion: tekton.dev/v1beta1
kind: Task
metadata:
  name: hello
spec:
  steps:
    - name: echo
      image: alpine
      script: |
        #!/bin/sh
        echo "Hello World"
```
To save and exit, press ```Ctrl + X``` then press Y and enter.\
Then you can apply the changes your cluster:\
```$ kubectl apply --filename hello-world.yaml```
You can confirm if the task successfully created from the resulting output which should look like this:\
```task.tekton.dev/hello created```
Now to instantiate and execute this task, we need to create another YAML file called ```hello-world-run.yaml```.\
As before create the file using:\
```$ touch hello-world-run.yaml```\
Then edit the file using:\
```$ nano hello-world-run.yaml```\
Finally you can paste in the following contents below:
```
apiVersion: tekton.dev/v1beta1
kind: TaskRun
metadata:
  name: hello-task-run
spec:
  taskRef:
    name: hello
```
Then press ```Ctrl + X```, press Y and then press enter.\
After this you can apply the changes to your cluster by using the command below:\
```$ kubectl apply --filename hello-world-run.yaml```\
Then you can verify that everything worked correctly:\
```$ kubectl get taskrun hello-task-run```\
The output should show the status of the task:
```
 NAME                    SUCCEEDED    REASON       STARTTIME   COMPLETIONTIME
 hello-task-run          True         Succeeded    22h         22h
```
Then finally if we take a look at the logs:\
```$ kubectl logs --selector=tekton.dev/taskRun=hello-task-run```\
Consequently, we can see the output, which is ```Hello World```.


