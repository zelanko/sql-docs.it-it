---
title: Configurare Kubernetes con kubeadm
titleSuffix: SQL Server big data clusters
description: Informazioni su come configurare Kubernetes in più computer Ubuntu 16,04 o 18,04 (fisici o virtuali) per [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] le distribuzioni.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 63a3529755267137cb7a1094060499e5db008ec8
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2019
ms.locfileid: "69652370"
---
# <a name="configure-kubernetes-on-multiple-machines-for-sql-server-big-data-cluster-deployments"></a>Configurare Kubernetes in più computer per distribuzioni di cluster Big Data di SQL Server

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Questo articolo fornisce un esempio di come usare **kubeadm** per configurare Kubernetes in più computer per [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] le distribuzioni. In questo esempio la destinazione è rappresentata da più computer Ubuntu 16.04 o 18.04 LTS (fisici o virtuali). Se la distribuzione viene eseguita in una piattaforma Linux diversa, è necessario modificare alcuni dei comandi per adeguarli al sistema in uso.  

> [!TIP] 
> Per gli script di esempio che configurano Kubernetes, vedere [Creare un cluster Kubernetes usando Kubeadm in Ubuntu 16.04 LTS or 18.04 LTS](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/deployment/kubeadm).
Vedere anche [questo](deployment-script-single-node-kubeadm.md) argomento per uno script di esempio che automatizza la distribuzione di uno strumento kubeadm per nodo singolo in una macchina virtuale e quindi distribuisce una configurazione predefinita di un cluster Big Data.

## <a name="prerequisites"></a>Prerequisiti

- Almeno 3 computer fisici o macchine virtuali Linux
- Configurazione consigliata per singolo computer:
   - 8 CPU
   - 64 GB di memoria
   - 100 GB di spazio di archiviazione

## <a name="prepare-the-machines"></a>Preparare i computer

Per ogni computer sono previsti prerequisiti diversi. In ogni computer eseguire i comandi seguenti in un terminale Bash:

1. Aggiungere il computer corrente al file `/etc/hosts`:

   ```bash
   echo $(hostname -i) $(hostname) | sudo tee -a /etc/hosts
   ```

1. Disabilitare lo scambio in tutti i dispositivi.

   ```bash
   sudo sed -i "/ swap / s/^/#/" /etc/fstab
   sudo swapoff -a
   ```

1. Importare le chiavi e registrare il repository per Kubernetes.

   ```bash
   sudo curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
   echo 'deb http://apt.kubernetes.io/ kubernetes-xenial main' | sudo tee -a /etc/apt/sources.list.d/kubernetes.list
   ```

1. Configurare i prerequisiti Docker e Kubernetes nel computer.

   ```bash
   KUBE_DPKG_VERSION=1.15.0-00
   sudo apt-get update && /
   sudo apt-get install -y ebtables ethtool && /
   sudo apt-get install -y docker.io && /
   sudo apt-get install -y apt-transport-https && /
   sudo apt-get install -y kubelet=$KUBE_DPKG_VERSION kubeadm=$KUBE_DPKG_VERSION kubectl=$KUBE_DPKG_VERSION && /
   curl https://raw.githubusercontent.com/kubernetes/helm/master/scripts/get | bash
   ```
 
1. Impostare `net.bridge.bridge-nf-call-iptables=1`. In Ubuntu 18.04 i comandi seguenti abilitano prima `br_netfilter`.

   ```bash
   . /etc/os-release
   if [ "$VERSION_CODENAME" == "bionic" ]; then sudo modprobe br_netfilter; fi
   sudo sysctl net.bridge.bridge-nf-call-iptables=1
   ```

## <a name="configure-the-kubernetes-master"></a>Configurare il nodo master Kubernetes

Dopo aver eseguito i comandi precedenti in ogni computer, scegliere uno dei computer come nodo master Kubernetes. Eseguire quindi nel computer i comandi seguenti.

1. Per prima cosa, creare un file rbac.yaml nella directory corrente usando il comando seguente. 

   ```bash
   cat <<EOF > rbac.yaml
   apiVersion: rbac.authorization.k8s.io/v1beta1
   kind: ClusterRoleBinding
   metadata:
     name: default-rbac
   subjects:
   - kind: ServiceAccount
     name: default
     namespace: default
   roleRef:
     kind: ClusterRole
     name: cluster-admin
     apiGroup: rbac.authorization.k8s.io
   EOF
   ```

1. Inizializzare il nodo master Kubernetes nel computer. Verrà visualizzato un messaggio per informare l'utente che il nodo master Kubernetes è stato inizializzato correttamente.

   ```bash
   KUBE_VERSION=1.11.3
   sudo kubeadm init --pod-network-cidr=10.244.0.0/16 --kubernetes-version=$KUBE_VERSION
   ```

1. Annotare il comando `kubeadm join` da usare negli altri server per unire in join il cluster Kubernetes. Copiare il comando per poterlo usare in seguito.

   ![kubeadm join](./media/deploy-with-kubeadm/kubeadm-join.png)

1. Configurare un file di configurazione di Kubernetes nella home directory.

   ```bash
   mkdir -p $HOME/.kube
   sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
   sudo chown $(id -u):$(id -g) $HOME/.kube/config
   ```

1. Configurare il cluster e il dashboard di Kubernetes.

   ```bash
   kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/master/Documentation/kube-flannel.yml
   helm init
   kubectl apply -f rbac.yaml
   kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/master/src/deploy/recommended/kubernetes-dashboard.yaml
   kubectl create clusterrolebinding kubernetes-dashboard --clusterrole=cluster-admin --serviceaccount=kube-system:kubernetes-dashboard
   ```

## <a name="configure-the-kubernetes-agents"></a>Configurare gli agenti Kubernetes

Gli altri computer svolgeranno la funzione di agenti Kubernetes nel cluster. 

In ognuno degli altri computer eseguire il comando `kubeadm join` copiato nella sezione precedente.

![kubeadm join agents](./media/deploy-with-kubeadm/kubeadm-join-agents.png)

## <a name="view-the-cluster-status"></a>Visualizzare lo stato del cluster

Per verificare la connessione al cluster, usare il comando [kubectl get](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands) per restituire un elenco di nodi del cluster.

```bash
kubectl get nodes
```

## <a name="next-steps"></a>Passaggi successivi

La procedura illustrata in questo articolo ha consentito la configurazione di un cluster Kubernetes in più computer Ubuntu. Il passaggio successivo prevede la distribuzione di un cluster Big Data di SQL Server 2019. Per informazioni, vedere l'articolo seguente:

[Distribuire SQL Server in Kubernetes](deployment-guidance.md#deploy)
