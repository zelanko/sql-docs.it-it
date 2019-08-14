---
title: Configurare minikube
titleSuffix: SQL Server big data clusters
description: Informazioni su come configurare minikube per le distribuzioni di cluster Big Data di SQL Server 2019 (anteprima) in un singolo computer.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 04/23/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 1991176de132062c46f36f30f4f384e483c069f9
ms.sourcegitcommit: 316c25fe7465b35884f72928e91c11eea69984d5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/13/2019
ms.locfileid: "68969418"
---
# <a name="configure-minikube-for-sql-server-big-data-cluster-deployments"></a>Configurare minikube per le distribuzioni di cluster Big Data di SQL Server

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Questo articolo descrive come configurare **minikube** in un singolo computer per le distribuzioni di cluster Big Data di SQL Server 2019 (anteprima). Minikube è uno strumento che semplifica l'esecuzione di Kubernetes in un singolo computer, ad esempio un computer portatile o un desktop. Minikube esegue un cluster Kubernetes a nodo singolo all'interno di una macchina virtuale nel portatile per gli utenti che vogliono provare Kubernetes o che usano quotidianamente questa piattaforma per lo sviluppo. 

## <a name="prerequisites"></a>Prerequisiti

- 64 GB di memoria.

- Se il computer ha solo la memoria minima consigliata, configurare la distribuzione del cluster in modo che abbia una sola istanza del pool di calcolo, un'istanza del pool di dati e un'istanza del pool di archiviazione. Questa configurazione deve essere usata solo per gli ambienti di valutazione in cui la durabilità e la disponibilità dei dati non sono importanti. Vedere la [documentazione sulla distribuzione](deployment-guidance.md#configfile) per altre informazioni sulle variabili di ambiente da impostare per configurare il numero di repliche per pool di dati, pool di calcolo e pool di archiviazione.

- La virtualizzazione VT-x o AMD-v deve essere abilitata nel BIOS del computer.

## <a name="install-dependencies"></a>Installare le dipendenze

1. Installare [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/).

1. Se non è già installato un hypervisor, installarne uno ora.
   - Per OS X, installare il [driver xhyve](https://git.k8s.io/minikube/docs/drivers.md), [VirtualBox](https://www.virtualbox.org/wiki/Downloads) o [VMware Fusion](https://www.vmware.com/products/fusion).
   - Per Linux, installare [VirtualBox](https://www.virtualbox.org/wiki/Downloads) o [KVM](https://www.linux-kvm.org/).
   - Per Windows, installare [VirtualBox](https://www.virtualbox.org/wiki/Downloads) o [Hyper-V](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install). Se non si dispone di un commutire esterno configurato in Hyper-V, crearne uno con accesso alla rete esterno. Informazioni su come [creare un commute esterno in Hyper-V per minikube](https://blogs.msdn.microsoft.com/wasimbloch/2017/01/23/setting-up-kubernetes-on-windows10-laptop-with-minikube/).

## <a name="install-minikube"></a>Installare minikube

Installare la versione minikube in base alle istruzioni per la [versione v 1.3.0](https://github.com/kubernetes/minikube/releases/tag/v1.3.0). Il cluster di Big Data SQL Server 2019 (anteprima) funziona solo con la versione v 1.0.0 e versioni di.

## <a name="create-a-minikube-cluster"></a>Creare un cluster minikube

Il comando seguente crea un cluster minikube in una macchina virtuale Hyper-V con 8 CPU, 64 GB di memoria e dimensioni del disco pari a 100 GB. Le dimensioni del disco non sono costituite da spazio riservato.  Lo spazio aumenta sul disco fino a tale valore in base alle esigenze.  Si consiglia di non modificare lo spazio su disco con un valore inferiore a 100 GB, perché durante i test si sono verificati problemi con una configurazione di questo tipo. Consente inoltre di specificare in modo esplicito il commutire Hyper-V con accesso esterno.

Modificare i parametri, ad esempio **--memory**, in base alle esigenze, a seconda dell'hardware disponibile e dell'hypervisor in uso.  Assicurarsi che il parametro per il commutatore virtuale **--hyper-v** corrisponda al nome usato in fase di creazione del commutatore virtuale.

```bash
minikube start --vm-driver="hyperv" --cpus 8 --memory 65536 --disk-size 100g --hyperv-virtual-switch "External"
```

Se si usa minikube con VirtualBox, il comando sarà simile al seguente:

```base
minikube start --cpus 8 --memory 65536 --disk-size 100g
```

## <a name="disable-automatic-checkpoint-with-hyper-v"></a>Disabilitare il checkpoint automatico con Hyper-V

In Windows 10 il checkpoint automatico è abilitato in una macchina virtuale. Eseguire il comando seguente in PowerShell per disabilitare il checkpoint automatico nella macchina virtuale e impostare la memoria su static.

```PowerShell
Set-VM -Name minikube -CheckpointType Disabled -AutomaticCheckpointsEnabled $false -StaticMemory
```

## <a name="next-steps"></a>Passaggi successivi

Tramite i passaggi in questo articolo è stato configurato un cluster minikube. Il passaggio successivo consiste nel distribuire un cluster Big Data di SQL Server 2019. Per informazioni, vedere l'articolo seguente:

[Distribuire cluster Big Data di SQL Server 2019 in Kubernetes](deployment-guidance.md#deploy)
