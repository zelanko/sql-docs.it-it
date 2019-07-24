---
title: Configurare Kubernetes con kubeadm
titleSuffix: SQL Server big data clusters
description: Informazioni su come configurare Kubernetes in più computer Ubuntu 16,04 o 18,04 (fisici o virtuali) per le distribuzioni di SQL Server 2019 Big Data cluster (anteprima).
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: ea79503869e7d403e4d3f4f960de9c95760eda0f
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419453"
---
# <a name="configure-kubernetes-on-multiple-machines-for-sql-server-big-data-cluster-deployments"></a>Configurare Kubernetes su più computer per le distribuzioni di SQL Server Big Data cluster

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Questo articolo fornisce un esempio di come usare **kubeadm** per configurare Kubernetes in più computer per le distribuzioni SQL Server 2019 Big Data cluster (anteprima). In questo esempio, più computer Ubuntu 16,04 o 18,04 LTS (fisico o virtuale) rappresentano la destinazione. Se si esegue la distribuzione in una piattaforma Linux diversa, è necessario modificare alcuni dei comandi in modo che corrispondano al sistema.  

> [!TIP] 
> Per gli script di esempio che configurano Kubernetes, vedere [creare un cluster Kubernetes con Kubeadm in Ubuntu 16,04 LTS o 18,04 LTS](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/deployment/kubeadm).

## <a name="prerequisites"></a>Prerequisiti

- Almeno 3 computer fisici Linux o macchine virtuali
- Configurazione consigliata per computer:
   - 8 CPU
   - 64 GB di memoria
   - 100 GB di spazio di archiviazione

## <a name="prepare-the-machines"></a>Preparare i computer

In ogni computer sono previsti diversi prerequisiti. In un terminale bash eseguire i comandi seguenti in ogni computer:

1. Aggiungere il computer corrente al `/etc/hosts` file:

   ```bash
   echo $(hostname -i) $(hostname) | sudo tee -a /etc/hosts
   ```

1. Disabilitare lo scambio su tutti i dispositivi.

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
   KUBE_DPKG_VERSION=1.11.3-00
   sudo apt-get update && /
   sudo apt-get install -y ebtables ethtool && /
   sudo apt-get install -y docker.io && /
   sudo apt-get install -y apt-transport-https && /
   sudo apt-get install -y kubelet=$KUBE_DPKG_VERSION kubeadm=$KUBE_DPKG_VERSION kubectl=$KUBE_DPKG_VERSION && /
   curl https://raw.githubusercontent.com/kubernetes/helm/master/scripts/get | bash
   ```
 
1. Impostare `net.bridge.bridge-nf-call-iptables=1`. In Ubuntu 18,04, i comandi seguenti abilitano `br_netfilter`prima.

   ```bash
   . /etc/os-release
   if [ "$VERSION_CODENAME" == "bionic" ]; then sudo modprobe br_netfilter; fi
   sudo sysctl net.bridge.bridge-nf-call-iptables=1
   ```

## <a name="configure-the-kubernetes-master"></a>Configurare il Master Kubernetes

Dopo aver eseguito i comandi precedenti in ogni computer, scegliere uno dei computer come Kubernetes master. Eseguire quindi i comandi seguenti nel computer.

1. Per prima cosa, creare un file RBAC. YAML nella directory corrente con il comando seguente. 

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

1. Inizializzare Kubernetes master nel computer. Verrà visualizzato un output che Kubernetes Master è stato inizializzato correttamente.

   ```bash
   KUBE_VERSION=1.11.3
   sudo kubeadm init --pod-network-cidr=10.244.0.0/16 --kubernetes-version=$KUBE_VERSION
   ```

1. Si noti `kubeadm join` il comando che è necessario usare negli altri server per aggiungere il cluster Kubernetes. Copiarlo per usarlo in seguito.

   ![Join kubeadm](./media/deploy-with-kubeadm/kubeadm-join.png)

1. Configurare un file di configurazione Kubernetes della Home Directory.

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

Gli altri computer fungono da agenti Kubernetes nel cluster. 

In ognuno degli altri computer eseguire il `kubeadm join` comando copiato nella sezione precedente.

![kubeadm join-agenti](./media/deploy-with-kubeadm/kubeadm-join-agents.png)

## <a name="view-the-cluster-status"></a>Visualizzare lo stato del cluster

Per verificare la connessione al cluster, usare il comando [kubectl Get](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands) per restituire un elenco dei nodi del cluster.

```bash
kubectl get nodes
```

## <a name="next-steps"></a>Passaggi successivi

La procedura descritta in questo articolo ha configurato un cluster Kubernetes in più computer Ubuntu. Il passaggio successivo consiste nel distribuire SQL Server cluster 2019 Big Data. Per istruzioni, vedere l'articolo seguente:

[Distribuire SQL Server in Kubernetes](deployment-guidance.md#deploy)
