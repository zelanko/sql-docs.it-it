---
title: Attività di eliminazione cluster di Azure HDInsight | Microsoft Docs
ms.custom: ''
ms.date: 02/28/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.afpdelcltask.f1
- sql11.dts.designer.afpdelcltask.f1
ms.assetid: e298776e-d18a-4393-a8e6-65ee3d555749
author: chugugrace
ms.author: chugu
ms.openlocfilehash: db0a15aaea37c6d18c1d3c2136e0fd0c94eb7506
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/26/2020
ms.locfileid: "85433898"
---
# <a name="azure-hdinsight-delete-cluster-task"></a>Attività di eliminazione cluster di Azure HDInsight
L'**attività di eliminazione cluster di Azure HDInsight** consente a un pacchetto di SSIS di eliminare un cluster Azure HDInsight nel gruppo di risorse e nella sottoscrizione di Azure specificati.
  
> [!NOTE]
> L'eliminazione di un cluster HDInsight può richiedere da 10 a 20 minuti circa.  
  
Per aggiungere un' **attività di eliminazione cluster di Azure HDInsight**, trascinare l'attività in Progettazione SSIS e farvi doppio clic oppure clic con il pulsante destro del mouse, quindi scegliere **Modifica** per visualizzare la finestra di dialogo seguente relativa all' **editor dell'attività di eliminazione cluster di Azure HDInsight** .  
  
La tabella seguente fornisce una descrizione dei campi della finestra di dialogo.  
  
|||  
|-|-|  
|**Campo**|**Descrizione**|  
|AzureResourceManagerConnection|Selezionare un'istanza di Gestione connessioni esistente per Azure Resource Manager oppure creare una nuova istanza che verrà usata per eliminare il cluster HDInsight.|
|SubscriptionId|Specificare l'ID della sottoscrizione del cluster HDInsight.|
|ResourceGroup|Specificare il gruppo di risorse di Azure in cui si trova il cluster HDInsight.|
|ClusterName|Consente di specificare il nome del cluster da eliminare.|  
|FailIfNotExists|Consente di indicare se l'attività deve avere esito negativo se il cluster non esiste.|
