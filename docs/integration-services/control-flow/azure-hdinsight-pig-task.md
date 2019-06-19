---
title: Attività Pig di Azure HDInsight | Microsoft Docs
ms.custom: ''
ms.date: 02/28/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.afppigtask.f1
- sql14.dts.designer.afppigtask.f1
ms.assetid: 26f34f64-f344-486e-9190-acf71aef29a8
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 3b07d792d2b73b6fd400835bbfe656bb02db8e18
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65727947"
---
# <a name="azure-hdinsight-pig-task"></a>Attività Pig di Azure HDInsight

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


Usare l' **attività Pig di Azure HDInsight** per eseguire uno script Pig in un cluster di Azure HDInsight.
     
Per aggiungere un' **attività Pig di Azure HDInsight**, trascinare l'attività in Progettazione SSIS e farvi doppio clic oppure clic con il pulsante destro del mouse, quindi scegliere **Modifica** per visualizzare la finestra di dialogo seguente relativa all' **editor dell'attività Pig di Azure HDInsight** .  
  
L'**attività Pig di Azure HDInsight** è un componente del [Feature Pack di SQL Server Integration Services (SSIS) per Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).
  
 L'elenco seguente contiene i campi di questa finestra di dialogo.  
  
1.  Per il campo **HDInsightConnection** selezionare un'istanza di Gestione connessione Azure HDInsight esistente oppure creare una nuova istanza che faccia riferimento al cluster HDInsight di Azure usato per eseguire lo script.
  
2.  Per il campo **AzureStorageConnection** selezionare un'istanza di Gestione connessione Archiviazione di Azure esistente oppure creare una nuova istanza che faccia riferimento all'account di archiviazione di Azure associato al cluster. Questa operazione è necessaria solo se si vuole scaricare l'output dell'esecuzione dello script e i log degli errori.
 
3.  Per il campo **BlobContainer** specificare il nome del contenitore di archiviazione associato al cluster. Questa operazione è necessaria solo se si vuole scaricare l'output dell'esecuzione dello script e i log degli errori.
  
4.  Per il campo **LocalLogFolder** specificare la cartella in cui verranno scaricati l'output dell'esecuzione dello script e i log degli errori. Questa operazione è necessaria solo se si vuole scaricare l'output dell'esecuzione dello script e i log degli errori.   
  
5.  È possibile specificare due modalità di esecuzione dello script Pig:
  
    1.  **Script inline**: specificare il campo **Script** digitando lo script inline da eseguire nella finestra di dialogo **Immetti script**.
  
    2.  **File script**: caricare il file script in Archiviazione BLOB di Azure e specificare il campo **BlobName**. Se il BLOB non è presente nell'account di archiviazione o nel contenitore predefinito associato al cluster HDInsight, è necessario specificare i campi **ExternalStorageAccountName** e **ExternalBlobContainer**. Per un BLOB esterno, assicurarsi che sia configurato come accessibile pubblicamente.  
  
     Se vengono specificati entrambi, verrà usato il file script e lo script inline verrà ignorato.
