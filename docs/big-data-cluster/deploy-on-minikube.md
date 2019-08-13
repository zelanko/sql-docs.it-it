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
ms.openlocfilehash: 6c2261b5cfbbe590c76ce410da4b95ee678a20b5
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/25/2019
ms.locfileid: "67958472"
---
# <a name="configure-minikube-for-sql-server-big-data-cluster-deployments"></a>Configurare minikube per le distribuzioni di cluster Big Data di SQL Server

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Questo articolo descrive come configurare **minikube** in un singolo computer per le distribuzioni di cluster Big Data di SQL Server 2019 (anteprima). Minikube è uno strumento che semplifica l'esecuzione di Kubernetes in un singolo computer, ad esempio un computer portatile o un desktop. Minikube esegue un cluster Kubernetes a nodo singolo all'interno di una macchina virtuale nel portatile per gli utenti che vogliono provare Kubernetes o che usano quotidianamente questa piattaforma per lo sviluppo. 

## <a name="prerequisites"></a>Prerequisites

- 32 GB di memoria (consigliati 64 GB).

- Se il computer ha solo la memoria minima consigliata, configurare la distribuzione del cluster in modo che abbia una sola istanza del pool di calcolo, un'istanza del pool di dati e un'istanza del pool di archiviazione. Questa configurazione deve essere usata solo per gli ambienti di valutazione in cui la durabilità e la disponibilità dei dati non sono importanti. Vedere la [documentazione sulla distribuzione](deployment-guidance.md#configfile) per altre informazioni sulle variabili di ambiente da impostare per configurare il numero di repliche per pool di dati, pool di calcolo e pool di archiviazione.

- La virtualizzazione VT-x o AMD-v deve essere abilitata nel BIOS del computer.

## <a name="install-dependencies"></a>Installare le dipendenze

1. Installare [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/).

1. Installare Python 3:
   - Se pip non è presente, scaricare [get-clspip.py](https://bootstrap.pypa.io/get-pip.py) ed eseguire `python get-pip.py`.
   - Installare il pacchetto di richieste usando `python -m pip install requests`.

1. Se non è già installato un hypervisor, installarne uno ora.
   - Per OS X, installare il [driver xhyve](https://git.k8s.io/minikube/docs/drivers.md), [VirtualBox](https://www.virtualbox.org/wiki/Downloads) o [VMware Fusion](https://www.vmware.com/products/fusion).
   - Per Linux, installare [VirtualBox](https://www.virtualbox.org/wiki/Downloads) o [KVM](https://www.linux-kvm.org/).
   - Per Windows, installare [VirtualBox](https://www.virtualbox.org/wiki/Downloads) o [Hyper-V](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install). Se non si ha un commutatore esterno configurato in Hyper-V, crearne uno con accesso di rete esterno.  Vedere come [creare un commutatore esterno in Hyper-V per minikube](https://blogs.msdn.microsoft.com/wasimbloch/2017/01/23/setting-up-kubernetes-on-windows10-laptop-with-minikube/).

## <a name="install-minikube"></a>Installare minikube

Installare minikube seguendo le istruzioni per la [versione 0.28.2](https://github.com/kubernetes/minikube/releases/tag/v0.28.2). Il cluster Big Data di SQL Server 2019 (anteprima) funziona solo con le versioni 0.24.1 e successive.

## <a name="create-a-minikube-cluster"></a>Creare un cluster minikube

Il comando seguente crea un cluster minikube in una macchina virtuale Hyper-V con 8 CPU, 28 GB di memoria e dimensioni del disco di 100 GB. Le dimensioni del disco non sono costituite da spazio riservato.  Lo spazio aumenta sul disco fino a tale valore in base alle esigenze.  Si consiglia di non modificare lo spazio su disco con un valore inferiore a 100 GB, perché durante i test si sono verificati problemi con una configurazione di questo tipo. Il comando specifica anche in modo esplicito il commutatore Hyper-v con accesso esterno.

Modificare i parametri, ad esempio **--memory**, in base alle esigenze, a seconda dell'hardware disponibile e dell'hypervisor in uso.  Assicurarsi che il parametro per il commutatore virtuale **--hyper-v** corrisponda al nome usato in fase di creazione del commutatore virtuale.

```bash
minikube start --vm-driver="hyperv" --cpus 8 --memory 28672 --disk-size 100g --hyperv-virtual-switch "External"
```

Se si usa minikube con VirtualBox, il comando sarà simile al seguente:

```base
minikube start --cpus 8 --memory 28672 --disk-size 100g
```

## <a name="disable-automatic-checkpoint-with-hyper-v"></a>Disabilitare il checkpoint automatico con Hyper-V

In Windows 10 il checkpoint automatico è abilitato in una macchina virtuale. Eseguire il comando seguente in PowerShell per disabilitare il checkpoint automatico nella macchina virtuale.

```PowerShell
Set-VM -Name minikube -CheckpointType Disabled -AutomaticCheckpointsEnabled $false
```

## <a name="next-steps"></a>Passaggi successivi

Tramite i passaggi in questo articolo è stato configurato un cluster minikube. Il passaggio successivo consiste nel distribuire un cluster Big Data di SQL Server 2019. Per informazioni, vedere l'articolo seguente:

[Distribuire cluster Big Data di SQL Server 2019 in Kubernetes](deployment-guidance.md#deploy)
