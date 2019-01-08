---
title: Attività Pig di Azure HDInsight | Microsoft Docs
ms.custom: ''
ms.date: 02/28/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.afppigtask.f1
- sql11.dts.designer.afppigtask.f1
ms.assetid: 26f34f64-f344-486e-9190-acf71aef29a8
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 30340a873846e20911a7f14694f9602c17d960e8
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52749413"
---
# <a name="azure-hdinsight-pig-task"></a>Attività Pig di Azure HDInsight
Usare l' **attività Pig di Azure HDInsight** per eseguire uno script Pig in un cluster di Azure HDInsight.
     
Per aggiungere un' **attività Pig di Azure HDInsight**, trascinare l'attività in Progettazione SSIS e farvi doppio clic oppure clic con il pulsante destro del mouse, quindi scegliere **Modifica** per visualizzare la finestra di dialogo seguente relativa all' **editor dell'attività Pig di Azure HDInsight** .  
  
 L'elenco seguente contiene i campi di questa finestra di dialogo.  
  
1.  Per il campo **HDInsightConnection** selezionare un'istanza di Gestione connessione Azure HDInsight esistente oppure creare una nuova istanza che faccia riferimento al cluster HDInsight di Azure usato per eseguire lo script.
  
2.  Per il campo **AzureStorageConnection** selezionare un'istanza di Gestione connessione Archiviazione di Azure esistente oppure creare una nuova istanza che faccia riferimento all'account di archiviazione di Azure associato al cluster. Questa operazione è necessaria solo se si vuole scaricare l'output dell'esecuzione dello script e i log degli errori.
 
3.  Per il campo **BlobContainer** specificare il nome del contenitore di archiviazione associato al cluster. Questa operazione è necessaria solo se si vuole scaricare l'output dell'esecuzione dello script e i log degli errori.
  
4.  Per il campo **LocalLogFolder** specificare la cartella in cui verranno scaricati l'output dell'esecuzione dello script e i log degli errori. Questa operazione è necessaria solo se si vuole scaricare l'output dell'esecuzione dello script e i log degli errori.   
  
5.  È possibile specificare due modalità di esecuzione dello script Pig:
  
    1.  **Script inline**: Specificare il **Script** campo digitando inline script da eseguire nel **Immetti Script** nella finestra di dialogo.
  
    2.  **File di script**: Caricare il file di script in archiviazione Blob di Azure e specificare il **BlobName** campo. Se il BLOB non è presente nell'account di archiviazione o nel contenitore predefinito associato al cluster HDInsight, è necessario specificare i campi **ExternalStorageAccountName** e **ExternalBlobContainer**. Per un BLOB esterno, assicurarsi che sia configurato come accessibile pubblicamente.  
  
     Se vengono specificati entrambi, verrà usato il file script e lo script inline verrà ignorato.
