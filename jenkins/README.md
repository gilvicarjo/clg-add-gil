# Jenkins

1. Create Jenkins Namespace: 
   ```
   k create ns jenkins
   ```
2. Validate namespace running: 
   ```
   k get ns
   ```
3. Run deployment YAML 
   ```
   k create -f jenkinsdeployment.yaml -n jenkins
   ```
4. Check Jenkins Deployment running: 
   ```
   k get deploy -n jenkins
   ```
5. Check Jenkins PODs  running:
   ```
   k get pods -n jenkins
   ```
6. Check Jenkins PODs logs
   ```
   k logs <pod> -n jenkins
   ```
   We would have an output like that
```
Jenkins initial setup is required. An admin user has been created and a password generated.
Please use the following password to proceed to installation:

<pass here!>

This may also be found at: /var/jenkins_home/secrets/initialAdminPassword

*************************************************************
*************************************************************
*************************************************************

2021-09-19 20:02:18.057+0000 [id=29]    INFO    jenkins.InitReactorRunner$1#onAttained: Completed initialization
2021-09-19 20:02:18.092+0000 [id=22]    INFO    hudson.WebAppMain$3#run: Jenkins is fully up and running
2021-09-19 20:02:18.542+0000 [id=42]    INFO    h.m.DownloadService$Downloadable#load: Obtained the updated data file for hudson.tasks.Maven.MavenInstaller
2021-09-19 20:02:18.543+0000 [id=42]    INFO    hudson.util.Retrier#start: Performed the action check updates server successfully at the attempt #1
2021-09-19 20:02:18.548+0000 [id=42]    INFO    hudson.model.AsyncPeriodicWork#lambda$doRun$0: Finished Download metadata. 34,654 ms
```

1. Check Pod and Namespace reunning:
```
➜  k get pods -n jenkins   
NAME                       READY   STATUS    RESTARTS   AGE
jenkins-585799558b-f6fc9   1/1     Running   0          7m52s

➜  k get deploy -n jenkins
NAME      READY   UP-TO-DATE   AVAILABLE   AGE
jenkins   1/1     1            1           7m56s
```

10. Service deploy:
    
```
k create -f jenkinsservice.yaml -n jenkins
```

11. Check Service running:
```
➜ k get svc -n jenkins

NAME      TYPE       CLUSTER-IP      EXTERNAL-IP   PORT(S)          AGE
jenkins   NodePort   10.101.122.85   <none>        8080:30785/TCP   31s
```
Neste exemplo, temos a porta 30785 utilizada para acessar o serviço do Jenkins. <br>
Agora precisamos apenas do endereço IP do Cluster Kubernetes

Então acessamos o Jenkins com: http://192.168.64.8:30785 <br>
Neste primeiro acesso, precisamos inserir a senha inicial exibida no passo 6.

12. Get into POD bash:
```
k exec -it <nome_do_pod_jenkins> -n jenkins -- /bin/bash
```

1.  Check **java** and **git** versions

```
$ java -version
openjdk version "11.0.12" 2021-07-20
OpenJDK Runtime Environment Temurin-11.0.12+7 (build 11.0.12+7)
OpenJDK 64-Bit Server VM Temurin-11.0.12+7 (build 11.0.12+7, mixed mode)

$ git --version
git version 2.30.2
```