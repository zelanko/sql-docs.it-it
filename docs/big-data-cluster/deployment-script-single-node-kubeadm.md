---
title: Eseguire la distribuzione con uno script Bash in un cluster kubeadm a nodo singolo
titleSuffix: SQL Server big data clusters
description: Usare uno script di distribuzione Bash per distribuire un cluster Big Data di SQL Server 2019 (anteprima) in un cluster kubeadm a nodo singolo.
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 37017221b636146a003f8af8890c655ed605bca9
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/25/2019
ms.locfileid: "68473073"
---
# <a name="deploy-with-a-bash-script-to-a-single-node-kubeadm-cluster"></a>Eseguire la distribuzione con uno script Bash in un cluster kubeadm a nodo singolo

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

In questa esercitazione si userà uno script di distribuzione Bash di esempio per distribuire un cluster Kubernetes a nodo singolo usando kubeadm e un cluster Big Data di SQL Server.  

## <a name="prerequisites"></a>Prerequisites

- Una macchina virtuale **server** con Vanilla Ubuntu 18.04 o 16.04. Tutte le dipendenze sono configurate dallo script e lo script viene eseguito dalla macchina virtuale.

  > [!NOTE]
  > L'uso di macchine virtuali di Azure non è ancora supportato.

- La macchina virtuale deve avere almeno 8 CPU, 64 GB di RAM e 100 GB di spazio su disco. Dopo aver eseguito il pull di tutte le immagini Docker del cluster Big Data, rimarranno 50 GB per i dati e i log da distribuire su tutti i componenti.

## <a name="instructions"></a>Istruzioni

1. Scaricare lo script nella macchina virtuale che si prevede di usare per la distribuzione.

   ```bash
   curl --output setup-bdc.sh https://raw.githubusercontent.com/microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/deployment/kubeadm/ubuntu-single-node-vm/setup-bdc.sh
   ```

2. Rendere lo script eseguibile con il comando seguente.

   ```bash
   chmod +x setup-bdc.sh
   ```

3. Eseguire lo script con **sudo**.

   ```bash
   sudo ./setup-bdc.sh
   ```

   Quando richiesto, specificare la password da usare per gli endpoint esterni seguenti: controller, istanza master di SQL Server e gateway. Per impostazione predefinita, il nome utente del controller è *admin*.

4. Configurare un alias per lo strumento **azdata**.

   ```bash
   source ~/.bashrc
   ```

5. Verificare che l'alias funzioni.

   ```bash
   azdata --version
   ```

## <a name="next-steps"></a>Passaggi successivi

Seguire [questa esercitazione](tutorial-load-sample-data.md) per iniziare a usare il cluster Big Data.
