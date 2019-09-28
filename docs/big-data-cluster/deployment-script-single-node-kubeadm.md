---
title: Eseguire la distribuzione con uno script Bash in un cluster kubeadm a nodo singolo
titleSuffix: SQL Server big data clusters
description: Usare uno script di distribuzione bash per distribuire un [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] in un cluster kubeadm a nodo singolo.
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 2379f96e3b5288fc33f5c925613bf9fd5d35612d
ms.sourcegitcommit: c4875c097e3aae1b76233777d15e0a0ec8e0d681
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/27/2019
ms.locfileid: "71341844"
---
# <a name="deploy-with-a-bash-script-to-a-single-node-kubeadm-cluster"></a>Eseguire la distribuzione con uno script Bash in un cluster kubeadm a nodo singolo

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

In questa esercitazione si userà uno script di distribuzione Bash di esempio per distribuire un cluster Kubernetes a nodo singolo usando kubeadm e un cluster Big Data di SQL Server.  

## <a name="prerequisites"></a>Prerequisiti

- Una macchina virtuale o un computer fisico della vaniglia Ubuntu 18,04 o 16,04 **Server** . Tutte le dipendenze sono configurate dallo script e lo script viene eseguito dalla macchina virtuale.

  > [!NOTE]
  > L'uso di macchine virtuali Linux di Azure non è ancora supportato.

- La macchina virtuale deve avere almeno 8 CPU, 64 GB di RAM e 100 GB di spazio su disco. Dopo aver eseguito il pull di tutte le immagini Docker del cluster Big Data, rimarranno 50 GB per i dati e i log da distribuire su tutti i componenti.

- Aggiornare i pacchetti esistenti usando i comandi seguenti per assicurarsi che l'immagine del sistema operativo sia aggiornata.

   ``` bash
   sudo apt update && sudo apt upgrade -y
   sudo systemctl reboot
   ```

## <a name="recommended-virtual-machine-settings"></a>Impostazioni della macchina virtuale consigliate

1. Usare la configurazione della memoria statica per la macchina virtuale. Nelle installazioni di Hyper-V, ad esempio, non viene utilizzata l'allocazione di memoria dinamica, ma viene allocata la versione consigliata 64 GB o successiva.

1. Usare la funzionalità di checkpoint o snapshot nell'Hyper-visiera per poter eseguire il rollback della macchina virtuale a uno stato pulito.


## <a name="instructions-to-deploy-sql-server-big-data-cluster"></a>Istruzioni per la distribuzione di SQL Server cluster Big Data

1. Scaricare lo script nella macchina virtuale che si prevede di usare per la distribuzione.

   ```bash
   curl --output setup-bdc.sh https://raw.githubusercontent.com/microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/deployment/kubeadm/ubuntu-single-node-vm/setup-bdc.sh
   ```

2. Rendere lo script eseguibile con il comando seguente.

   ```bash
   chmod +x setup-bdc.sh
   ```

3. Eseguire lo script (assicurarsi che sia in esecuzione con *sudo*)

   ```bash
   sudo ./setup-bdc.sh
   ```

   Quando richiesto, specificare la password da usare per gli endpoint esterni seguenti: controller, istanza master di SQL Server e gateway. La password deve essere sufficientemente complessa in base alle regole esistenti per SQL Server password. Per impostazione predefinita, il nome utente del controller è *admin*.

4. Configurare un alias per lo strumento **azdata**.

   ```bash
   source ~/.bashrc
   ```

5. Aggiornare l'installazione degli alias per azdata.

   ```bash
   azdata --version
   ```

## <a name="cleanup"></a>Pulizia

Lo script [Cleanup-BDC.sh](https://raw.githubusercontent.com/microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/deployment/kubeadm/ubuntu-single-node-vm/cleanup-bdc.sh) viene fornito come vantaggio per reimpostare l'ambiente, se necessario. Tuttavia, è consigliabile usare una macchina virtuale a scopo di test e usare la funzionalità snapshot nell'hypervisor per eseguire il rollback della macchina virtuale a uno stato pulito.

## <a name="next-steps"></a>Passaggi successivi

Per iniziare a usare i cluster di Big Data, vedere [Tutorial: Caricare i dati di esempio in un cluster SQL Server Big Data @ no__t-0.
