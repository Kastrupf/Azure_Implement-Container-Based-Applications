# Azure_Implement-Container-Based-Applications
### Configuring an Azure Kubernetes Services (AKS)


#### Pour cette activité, nos objectifs sont les suivants :
* Créer une structure AKS
* Effectuer le déploiement d'un cluster
* Effectuer le déploiement d'applications
* Effectuer des tests d'ajout de nouveaux POD
* Effectuer de nouveaux tests d'ajout de nœud

<img width="653" alt="image" src="https://user-images.githubusercontent.com/43493818/183902516-55b41d83-0647-4215-89d6-0e89dd4038d8.png">

## Le Projet
*En cours de rédaction* 


1. 

```
fernanda@Azure:~$ kubectl config get-contexts
CURRENT   NAME          CLUSTER       AUTHINFO                            NAMESPACE
*         aks-orlando   aks-orlando   clusterUser_rg-akslab_aks-orlando  
```

2.

```
fernanda@Azure:~$ kubectl top nodes
NAME                                CPU(cores)   CPU%   MEMORY(bytes)   MEMORY%   
aks-agentpool-35944412-vmss000000   133m         7%     1997Mi          92%       
aks-agentpool-35944412-vmss000001   120m         6%     1502Mi          69%       
aks-agentpool-35944412-vmss000002   112m         5%     1439Mi          66%     
```

3.

```
fernanda@Azure:~$ kubectl scale --replicas=3 deployment/azure-vote-front
Warning: spec.template.spec.nodeSelector[beta.kubernetes.io/os]: deprecated since v1.14; use "kubernetes.io/os" instead
deployment.apps/azure-vote-front scaled
fernanda@Azure:~$ kubectl scale --replicas=3 deployment/azure-vote-back
Warning: spec.template.spec.nodeSelector[beta.kubernetes.io/os]: deprecated since v1.14; use "kubernetes.io/os" instead
deployment.apps/azure-vote-back scaled
```

4.

```
fernanda@Azure:~$ kubectl get pods --show-labels
NAME                                READY   STATUS    RESTARTS   AGE   LABELS
azure-vote-back-5f46f8f4cc-77krj    1/1     Running   0          41m   app=azure-vote-back,pod-template-hash=5f46f8f4cc
azure-vote-back-5f46f8f4cc-lpcc2    1/1     Running   0          31m   app=azure-vote-back,pod-template-hash=5f46f8f4cc
azure-vote-back-5f46f8f4cc-wtqs8    1/1     Running   0          31m   app=azure-vote-back,pod-template-hash=5f46f8f4cc
azure-vote-front-5d68fcf586-4rhlz   1/1     Running   0          35m   app=azure-vote-front,pod-template-hash=5d68fcf586
azure-vote-front-5d68fcf586-qbdzz   1/1     Running   0          41m   app=azure-vote-front,pod-template-hash=5d68fcf586
azure-vote-front-5d68fcf586-whbc6   1/1     Running   0          35m   app=azure-vote-front,pod-template-hash=5d68fcf586
```

5.

```
fernanda@Azure:~$ kubectl get pod -o=custom-columns=NODE:.spec.nodeName,POD:.metadata.name
NODE                                POD
aks-agentpool-35944412-vmss000000   azure-vote-back-5f46f8f4cc-77krj
aks-agentpool-35944412-vmss000001   azure-vote-back-5f46f8f4cc-lpcc2
aks-agentpool-35944412-vmss000001   azure-vote-back-5f46f8f4cc-wtqs8
aks-agentpool-35944412-vmss000002   azure-vote-front-5d68fcf586-4rhlz
aks-agentpool-35944412-vmss000000   azure-vote-front-5d68fcf586-qbdzz
aks-agentpool-35944412-vmss000002   azure-vote-front-5d68fcf586-whbc6
```

6.

```
fernanda@Azure:~$ kubectl scale --replicas=10 deployment/azure-vote-front
Warning: spec.template.spec.nodeSelector[beta.kubernetes.io/os]: deprecated since v1.14; use "kubernetes.io/os" instead
deployment.apps/azure-vote-front scaled
fernanda@Azure:~$ kubectl scale --replicas=10 deployment/azure-vote-back
Warning: spec.template.spec.nodeSelector[beta.kubernetes.io/os]: deprecated since v1.14; use "kubernetes.io/os" instead
deployment.apps/azure-vote-back scaled
fernanda@Azure:~$ kubectl get pods --show-labels
NAME                                READY   STATUS    RESTARTS   AGE   LABELS
azure-vote-back-5f46f8f4cc-4g6bf    1/1     Running   0          6s    app=azure-vote-back,pod-template-hash=5f46f8f4cc
azure-vote-back-5f46f8f4cc-6wxmj    1/1     Running   0          6s    app=azure-vote-back,pod-template-hash=5f46f8f4cc
azure-vote-back-5f46f8f4cc-77krj    1/1     Running   0          43m   app=azure-vote-back,pod-template-hash=5f46f8f4cc
azure-vote-back-5f46f8f4cc-7lrnv    1/1     Running   0          6s    app=azure-vote-back,pod-template-hash=5f46f8f4cc
azure-vote-back-5f46f8f4cc-jtvgl    1/1     Running   0          6s    app=azure-vote-back,pod-template-hash=5f46f8f4cc
azure-vote-back-5f46f8f4cc-k882q    1/1     Running   0          6s    app=azure-vote-back,pod-template-hash=5f46f8f4cc
azure-vote-back-5f46f8f4cc-ln5jh    1/1     Running   0          6s    app=azure-vote-back,pod-template-hash=5f46f8f4cc
azure-vote-back-5f46f8f4cc-lpcc2    1/1     Running   0          32m   app=azure-vote-back,pod-template-hash=5f46f8f4cc
azure-vote-back-5f46f8f4cc-nhrtb    1/1     Running   0          6s    app=azure-vote-back,pod-template-hash=5f46f8f4cc
azure-vote-back-5f46f8f4cc-wtqs8    1/1     Running   0          32m   app=azure-vote-back,pod-template-hash=5f46f8f4cc
azure-vote-front-5d68fcf586-46g5r   1/1     Running   0          23s   app=azure-vote-front,pod-template-hash=5d68fcf586
azure-vote-front-5d68fcf586-4rhlz   1/1     Running   0          36m   app=azure-vote-front,pod-template-hash=5d68fcf586
azure-vote-front-5d68fcf586-7blwf   1/1     Running   0          23s   app=azure-vote-front,pod-template-hash=5d68fcf586
azure-vote-front-5d68fcf586-hblt5   1/1     Running   0          23s   app=azure-vote-front,pod-template-hash=5d68fcf586
azure-vote-front-5d68fcf586-hg9rh   1/1     Running   0          23s   app=azure-vote-front,pod-template-hash=5d68fcf586
azure-vote-front-5d68fcf586-j56q4   1/1     Running   0          23s   app=azure-vote-front,pod-template-hash=5d68fcf586
azure-vote-front-5d68fcf586-npc4p   1/1     Running   0          23s   app=azure-vote-front,pod-template-hash=5d68fcf586
azure-vote-front-5d68fcf586-qbdzz   1/1     Running   0          43m   app=azure-vote-front,pod-template-hash=5d68fcf586
azure-vote-front-5d68fcf586-whbc6   1/1     Running   0          36m   app=azure-vote-front,pod-template-hash=5d68fcf586
azure-vote-front-5d68fcf586-znpcn   1/1     Running   0          23s   app=azure-vote-front,pod-template-hash=5d68fcf586
```

7.

```
fernanda@Azure:~$ kubectl get deployments
NAME               READY   UP-TO-DATE   AVAILABLE   AGE
azure-vote-back    10/10   10           10          44m
azure-vote-front   10/10   10           10          44m
```

8.

```
fernanda@Azure:~$ kubectl get service azure-vote-front --watch
NAME               TYPE           CLUSTER-IP   EXTERNAL-IP   PORT(S)        AGE
azure-vote-front   LoadBalancer   10.0.253.5   20.81.36.94   80:31456/TCP   44m
```

9.

```
^Cfernanda@Azure:~$ kubectget pod -o=custom-columns=NODE:.spec.nodeName,POD:.metadata.name
NODE                                POD
aks-agentpool-35944412-vmss000002   azure-vote-back-5f46f8f4cc-4g6bf
aks-agentpool-35944412-vmss000002   azure-vote-back-5f46f8f4cc-6wxmj
aks-agentpool-35944412-vmss000000   azure-vote-back-5f46f8f4cc-77krj
aks-agentpool-35944412-vmss000002   azure-vote-back-5f46f8f4cc-7lrnv
aks-agentpool-35944412-vmss000002   azure-vote-back-5f46f8f4cc-jtvgl
aks-agentpool-35944412-vmss000001   azure-vote-back-5f46f8f4cc-k882q
aks-agentpool-35944412-vmss000000   azure-vote-back-5f46f8f4cc-ln5jh
aks-agentpool-35944412-vmss000001   azure-vote-back-5f46f8f4cc-lpcc2
aks-agentpool-35944412-vmss000001   azure-vote-back-5f46f8f4cc-nhrtb
aks-agentpool-35944412-vmss000001   azure-vote-back-5f46f8f4cc-wtqs8
aks-agentpool-35944412-vmss000001   azure-vote-front-5d68fcf586-46g5r
aks-agentpool-35944412-vmss000002   azure-vote-front-5d68fcf586-4rhlz
aks-agentpool-35944412-vmss000001   azure-vote-front-5d68fcf586-7blwf
aks-agentpool-35944412-vmss000002   azure-vote-front-5d68fcf586-hblt5
aks-agentpool-35944412-vmss000002   azure-vote-front-5d68fcf586-hg9rh
aks-agentpool-35944412-vmss000001   azure-vote-front-5d68fcf586-j56q4
aks-agentpool-35944412-vmss000000   azure-vote-front-5d68fcf586-npc4p
aks-agentpool-35944412-vmss000000   azure-vote-front-5d68fcf586-qbdzz
aks-agentpool-35944412-vmss000002   azure-vote-front-5d68fcf586-whbc6
aks-agentpool-35944412-vmss000001   azure-vote-front-5d68fcf586-znpcn
```




