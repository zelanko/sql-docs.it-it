---
title: Caricamento di dati in Parallel Data Warehouse | Microsoft Docs
description: È possibile caricare o inserire dati in SQL Server Parallel Data Warehouse (PDW) utilizzando Integration Services, utilità bcp, dwloader o l'istruzione SQL INSERT.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: b046839b7c4932b43230d28cc106db1e2ea5d5a7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67960697"
---
# <a name="loading-data-into-parallel-data-warehouse"></a>Caricamento di dati in Parallel Data Warehouse
È possibile caricare o inserire dati in SQL Server Parallel Data Warehouse (PDW) utilizzando servizi di integrazione [utilità bcp](../tools/bcp-utility.md), **dwloader** Loader della riga di comando o l'istruzione SQL INSERT.  

## <a name="loading-environment"></a>Caricamento dell'ambiente  
Per caricare i dati, è necessario uno o più server di caricamento. È possibile usare il proprio ETL esistenti o ad altri server o è possibile acquistare nuovi server. Per altre informazioni, vedere [acquisire e configurare un Server di caricamento](acquire-and-configure-loading-server.md). Queste istruzioni includono una [caricamento capacità pianificazione foglio di lavoro Server](loading-server-capacity-planning-worksheet.md) per pianificare la soluzione ideale per il caricamento.  
  
## <a name="load-with-dwloader"></a>Caricare i dati con dwloader  
Usando il [caricatore della riga di comando dwloader](dwloader.md) è il modo più rapido caricare i dati in PDW.  
  
![Processo di caricamento](media/loading-process.png "processo di caricamento")  
  
dwloader carica i dati direttamente ai nodi di calcolo senza passare i dati tramite il nodo di controllo. Per caricare i dati, dwloader innanzitutto comunica con il nodo di controllo per ottenere informazioni di contatto per i nodi di calcolo. dwloader configura un canale di comunicazione con ogni nodo di calcolo e quindi invia i blocchi di 256KB di dati ai nodi di calcolo in modo round robin.  
  
In ogni nodo di calcolo, Data Movement Service (DMS) riceve ed elabora blocchi di dati. L'elaborazione di dati include la conversione di ogni riga in formato nativo di SQL Server e il calcolo dell'hash di distribuzione per determinare il nodo di calcolo a cui appartiene ogni riga.  
  
Dopo l'elaborazione delle righe, servizio migrazione del database utilizza uno spostamento casuale per il trasferimento di ogni riga per il corretto del nodo di calcolo e l'istanza di SQL Server. Dato che SQL Server riceve le righe, li inserisce in batch in base al **-b** imposta il parametro batch size in dwloader e quindi il caricamento bulk del batch.  

## <a name="load-with-prepared-statements"></a>Caricare i dati con le istruzioni preparate

È possibile utilizzare le istruzioni preparate per caricare dati in tabelle replicate e distribuite. Quando i dati di input non corrisponde al tipo di dati di destinazione, viene eseguita una conversione implicita. Le conversioni implicite supportate da PDW istruzioni preparate sono un subset delle conversioni supportate da SQL Server. Vale a dire, sono supportati solo un subset di conversioni, ma le conversioni supportate corrispondono conversioni implicite di SQL Server. Indipendentemente dal fatto che la tabella di destinazione deve essere caricato sia definita come una tabella distribuita o replicata, le conversioni implicite vengono applicate a tutte le colonne esistenti nella tabella di destinazione (se necessario). 

<!-- MISSING LINK
For more information, see [Prepared statements](prepared-statements.md).
-->
  
## <a name="related-tasks"></a>Attività correlate  
  
|Attività|Descrizione|  
|--------|---------------|  
|Creare il database di gestione temporanea.|[Creare il database di gestione temporanea](staging-database.md)|  
|Caricare con Integration Services.|[Caricare con Integration Services](load-with-ssis.md)|  
|Comprendere le conversioni di tipo per dwloader.|[Regole di conversione del tipo di dati per dwloader](dwloader-data-type-conversion-rules.md)|  
|Caricare dati con dwloader.|[Caricatore della riga di comando dwloader](dwloader.md)|  
|Comprendere le conversioni di tipo per l'inserimento.|[Caricare i dati con INSERT](load-with-insert.md)|  
 
<!-- MISSING LINKS
## See Also  
[Grant permissions to load data](grant-permissions-to-load-data.md)  
[Common metadata query examles](metadata-query-examples.md)  
  
-->
