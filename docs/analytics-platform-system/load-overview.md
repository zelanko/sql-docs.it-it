---
title: Caricamento dei dati
description: È possibile caricare o inserire dati in SQL Server Parallel data warehouse (PDW) usando Integration Services, l'utilità bcp, dwloader o l'istruzione SQL INSERT.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: fd161820fd53d45642848697bce9589a98dec4ca
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401043"
---
# <a name="loading-data-into-parallel-data-warehouse"></a>Caricamento dei dati in parallelo data warehouse
È possibile caricare o inserire dati in SQL Server Parallel data warehouse (PDW) usando Integration Services, l' [utilità bcp](../tools/bcp-utility.md), il caricatore da riga di comando **dwloader** o l'istruzione SQL INSERT.  

## <a name="loading-environment"></a>Caricamento dell'ambiente  
Per caricare i dati, sono necessari uno o più server di caricamento. È possibile utilizzare il proprio ETL o altri server esistenti oppure è possibile acquistare nuovi server. Per altre informazioni, vedere [acquisire e configurare un server di caricamento](acquire-and-configure-loading-server.md). Queste istruzioni includono un [foglio](loading-server-capacity-planning-worksheet.md) di disegno per la pianificazione della capacità del server per facilitare la pianificazione della soluzione corretta per il caricamento.  
  
## <a name="load-with-dwloader"></a>Caricare con dwloader  
L'uso del [caricatore da riga di comando dwloader](dwloader.md) rappresenta il modo più rapido per caricare i dati in PDW.  
  
![Processo di caricamento](media/loading-process.png "Processo di caricamento")  
  
dwloader carica i dati direttamente nei nodi di calcolo senza passare i dati attraverso il nodo di controllo. Per caricare i dati, dwloader comunica innanzitutto con il nodo di controllo per ottenere le informazioni di contatto per i nodi di calcolo. dwloader configura un canale di comunicazione con ogni nodo di calcolo e quindi invia blocchi 256 KB di dati ai nodi di calcolo in modo round robin.  
  
In ogni nodo di calcolo, il servizio di spostamento dei dati (DMS) riceve ed elabora i blocchi di dati. L'elaborazione dei dati include la conversione di ogni riga in SQL Server formato nativo e il calcolo dell'hash di distribuzione per determinare il nodo di calcolo a cui appartiene ogni riga.  
  
Dopo l'elaborazione delle righe, DMS usa uno spostamento casuale per trasferire ogni riga nel nodo di calcolo e nell'istanza di SQL Server corretti. Quando SQL Server riceve le righe, le invia in batch in base al parametro di dimensioni batch **-b** impostato in dwloader, quindi esegue il caricamento bulk del batch.  

## <a name="load-with-prepared-statements"></a>Caricare con le istruzioni preparate

È possibile utilizzare le istruzioni preparate per caricare dati in tabelle distribuite e replicate. Quando i dati di input non corrispondono al tipo di dati di destinazione, viene eseguita una conversione implicita. Le conversioni implicite supportate dalle istruzioni preparate PDW sono un subset di conversioni supportate da SQL Server. Ovvero è supportato solo un subset di conversioni, ma le conversioni supportate corrispondono SQL Server le conversioni implicite. Indipendentemente dal fatto che la tabella di destinazione da caricare sia definita come tabella distribuita o replicata, le conversioni implicite vengono applicate (se necessario) a tutte le colonne presenti nella tabella di destinazione. 

<!-- MISSING LINK
For more information, see [Prepared statements](prepared-statements.md).
-->
  
## <a name="related-tasks"></a>Related Tasks  
  
|Attività|Description|  
|--------|---------------|  
|Creare il database di gestione temporanea.|[Creare il database di gestione temporanea](staging-database.md)|  
|Caricare con Integration Services.|[Caricare con Integration Services](load-with-ssis.md)|  
|Informazioni sulle conversioni di tipi per dwloader.|[Regole di conversione del tipo di dati per dwloader](dwloader-data-type-conversion-rules.md)|  
|Caricare i dati con dwloader.|[Caricatore da riga di comando dwloader](dwloader.md)|  
|Informazioni sulle conversioni di tipi per INSERT.|[Caricare i dati con INSERT](load-with-insert.md)|  
 
<!-- MISSING LINKS
## See Also  
[Grant permissions to load data](grant-permissions-to-load-data.md)  
[Common metadata query examles](metadata-query-examples.md)  
  
-->
