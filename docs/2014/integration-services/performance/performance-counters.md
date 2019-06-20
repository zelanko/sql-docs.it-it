---
title: Contatori delle prestazioni | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- logs [Integration Services], performance counters
- performance counters [Integration Services]
- data flow [Integration Services], performance
- counters [Integration Services]
- data flow engine [Integration Services]
ms.assetid: 11e17f4e-72ed-44d7-a71d-a68937a78e4c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 79c9e433a6b5bcf9babee0060fdf028775e0e8a4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62889836"
---
# <a name="performance-counters"></a>Contatori delle prestazioni
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] installa un set di contatori delle prestazioni che è possibile usare per monitorare le prestazioni del motore flusso di dati. Ad esempio controllando il contatore "Buffer con spooling" è possibile stabilire se i buffer dei dati vengano scritti temporaneamente sul disco mentre il pacchetto è in esecuzione. Lo swapping riduce le prestazioni e indica che la memoria del computer è insufficiente.  
  
> [!NOTE]  
>  Se [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] viene installato in un computer che esegue [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] e tale computer viene aggiornato a [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)], il processo di aggiornamento rimuove i contatori delle prestazioni [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] dal computer. Per ripristinare i contatori delle prestazioni [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] nel computer, eseguire il programma di installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in modalità di ripristino.  
  
 Nella tabella seguente sono descritti i contatori delle prestazioni disponibili.  
  
|Contatore delle prestazioni|Descrizione|  
|-------------------------|-----------------|  
|Byte BLOB letti|Numero di byte dei dati BLOB (oggetto binario di grandi dimensioni) letti dal motore flusso di dati in tutte le origini.|  
|Byte BLOB scritti|Numero di byte dei dati BLOB scritti dal motore flusso di dati in tutte le destinazioni.|  
|File BLOB in uso|Il numero di file BLOB attualmente utilizzati dal motore flusso di dati per lo spooling.|  
|Memoria buffer|Quantità di memoria in uso. Può includere sia memoria fisica che virtuale. Se questo numero è maggiore della quantità di memoria fisica, il valore di **Buffer con spooling** aumenta, per indicare che lo swapping di memoria è in aumento. Un incremento del swapping di memoria influisce negativamente sulle prestazioni del motore flusso di dati.|  
|Buffer in uso|Numero di oggetti buffer, di qualsiasi tipo, attualmente utilizzati dal motore e da tutti i componenti flusso di dati.|  
|Buffer con spooling|Numero di buffer attualmente scritti sul disco. Se la quantità di memoria fisica del motore flusso di dati è insufficiente, i buffer non in uso vengono scritti su disco e quindi ricaricati quando risultano necessari.|  
|Memoria lineare buffer|Quantità totale di memoria lineare, in byte, utilizzata da tutti i buffer. I buffer memoria lineare sono blocchi di memoria utilizzati da un componente per l'archiviazione di dati. Un buffer di memoria lineare è costituito da un blocco di byte di grandi dimensioni di cui l'accesso viene eseguito un byte alla volta.|  
|Buffer memoria lineare in uso|Numero di buffer di memoria lineare utilizzati dal motore flusso di dati. Tutti i buffer memoria lineare sono buffer privati.|  
|Memoria buffer privati|Quantità totale di memoria utilizzata da tutti i buffer privati. Un buffer non è privato quando viene creato dal motore flusso di dati per il supporto del flusso di dati. Un buffer privato è un buffer utilizzato da una trasformazione esclusivamente per un'attività temporanea. Un esempio è la trasformazione Aggregazione.|  
|Buffer privati in uso|Numero di buffer utilizzati dalle trasformazioni.|  
|Righe lette|Numero di righe prodotte da un'origine. Sono escluse le righe lette in tabelle di riferimento dalla trasformazione Ricerca.|  
|Righe scritte|Numero di righe offerte a una destinazione. Sono escluse le righe scritte nell'archivio dati di destinazione.|  
  
 Lo snap-in MMC (Microsoft Management Console) Prestazioni consente di creare un registro in cui vengono inclusi i contatori delle prestazioni.  
  
 Per informazioni sull'ottimizzazione delle prestazioni, vedere [Funzionalità delle prestazioni del flusso di dati](../data-flow/data-flow-performance-features.md).  
  
## <a name="obtain-performance-counter-statistics"></a>Ottenere statistiche del contatore delle prestazioni  
 Per i progetti [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] distribuiti nel server [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] è possibile ottenere statistiche del contatore delle prestazioni usando la funzione [dm_execution_performance_counters &#40;SSISDB Database&#41;](/sql/integration-services/functions-dm-execution-performance-counters).  
  
 Nell'esempio seguente la funzione restituisce le statistiche di un'esecuzione in corso con ID 34.  
  
```  
select * from [catalog].[dm_execution_performance_counters] (34)  
```  
  
 Nell'esempio seguente la funzione restituisce le statistiche di tutte le esecuzioni in corso nel server [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
```  
select * from [catalog].[dm_execution_performance_counters] (NULL)  
  
```  
  
> [!IMPORTANT]  
>  Se si è un membro del ruolo del database `ssis_admin`, vengono restituite le statistiche sulle prestazioni per tutte le esecuzioni in corso.  Se non si è un membro del ruolo del database `ssis_admin`, vengono restituite le statistiche sulle prestazioni per le esecuzioni in corso per cui si dispone delle autorizzazioni di lettura.  
  
## <a name="related-content"></a>Contenuto correlato  
  
-   Strumento nella [SSIS Performance Visualization for Business Intelligence Development Studio (CodePlex Project)](https://go.microsoft.com/fwlink/?LinkId=146626) (Visualizzazione delle prestazione di SSIS per Business Intelligence Development Studio (progetto CodePlex)) nel sito codeplex.com.  
  
-   Video [Measuring and Understanding the Performance of Your SSIS Packages in the Enterprise (SQL Server Video)](https://go.microsoft.com/fwlink/?LinkId=150497) (Misurazione e comprensione delle prestazioni dei pacchetti SSIS nell'organizzazione (video di SQL Server)) nel sito msdn.microsoft.com.  
  
-   Articolo di supporto [The SSIS performance counter is no longer available in the Performance Monitor after you upgrade to Windows Server 2008](https://go.microsoft.com/fwlink/?LinkId=235319) (Mancata disponibilità del contatore delle prestazioni di SSIS in Performance Monitor dopo l'aggiornamento a Windows Server 2008) nel sito support.microsoft.com.  
  
## <a name="see-also"></a>Vedere anche  
 [Esecuzione di progetti e pacchetti](../packages/run-integration-services-ssis-packages.md)  
  
  
