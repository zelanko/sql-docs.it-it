---
title: Destinazione file di eventi | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- event file target
- file target [SQL Server extended events]
- targets [SQL Server extended events], file target
ms.assetid: 4f0ee6ec-a0a8-4c38-aa61-8293ab6ac7fd
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 1a64236b3874543982be5abbd8e60d8169082a1e
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84933061"
---
# <a name="event-file-target"></a>Event File Target
  La destinazione file di eventi è una destinazione che esegue la scrittura di buffer completi sul disco.  
  
 La tabella seguente descrive le opzioni disponibili per configurare un file di eventi usato come destinazione.  
  
|Opzione|Valori consentiti|Description|  
|------------|--------------------|-----------------|  
|filename|Qualsiasi stringa contenente fino a 260 caratteri. Questo valore è obbligatorio.|Percorso del file e nome del file.<br /><br /> È possibile usare qualsiasi estensione per il file.|  
|max_file_size|Qualsiasi valore intero a 64 bit. Questo valore è facoltativo.|Dimensioni massime del file in megabyte (MB). Se l'opzione max_file_size non è specificata, le dimensioni del file aumenteranno fino a quando il disco non è pieno. Il valore delle dimensioni predefinite del file è 1 GB.<br /><br /> Il valore di max_file_size deve essere maggiore delle dimensioni correnti dei buffer della sessione. In caso contrario, il file di destinazione non verrà inizializzato in modo corretto e verrà segnalato che il valore di max_file_size non è valido. Per visualizzare le dimensioni correnti dei buffer, eseguire una query sulla colonna buffer_size nella vista a gestione dinamica [sys.dm_xe_sessions](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-sessions-transact-sql) .<br /><br /> Se le dimensioni predefinite del file sono minori di quelle del buffer della sessione, è consigliabile impostare max_file_size sul valore specificato nella colonna max_memory nella vista del catalogo [sys.server_event_sessions](/sql/relational-databases/system-catalog-views/sys-server-event-sessions-transact-sql) .<br /><br /> Quando l'opzione max_file_size è impostata su dimensioni maggiori di quelle dei buffer della sessione, il valore può essere arrotondato per difetto al multiplo più vicino delle dimensioni dei buffer della sessione. In questo modo è possibile creare un file di destinazione minore del valore specificato di max_file_size. Se il valore delle dimensioni del buffer, ad esempio, è 100 MB e max_file_size è impostato su 150 MB, le dimensioni del file risultante vengono arrotondate per difetto al valore 100 MB perché i 50 MB di spazio non sarebbero sufficienti per il secondo buffer.<br /><br /> Se le dimensioni predefinite del file sono minori di quelle del buffer della sessione, è consigliabile impostare max_file_size sul valore nella colonna max_memory nella vista del catalogo [sys.server_event_sessions](/sql/relational-databases/system-catalog-views/sys-server-event-sessions-transact-sql) .|  
|max_rollover_files|Qualsiasi valore intero a 32 bit. Questo valore è facoltativo.|Numero massimo di file da mantenere nel file system. Il valore predefinito è 5.|  
|increment|Qualsiasi valore intero a 32 bit. Questo valore è facoltativo.|Crescita incrementale del file in megabyte (MB). Se non viene specificato, il valore predefinito per questa opzione è il doppio delle dimensioni del buffer della sessione.|  
  
 La prima volta che viene creata una destinazione del file di evento, il nome del file specificato viene aggiunto con _0\_ e un valore long integer. Il valore integer viene calcolato come numero di millisecondi compresi tra l'1 gennaio 1601 e la data e l'ora di creazione del file. Questo formato viene usato anche da file di rollover successivi. L'analisi del valore long integer consente di determinare il file più recente. Nell'esempio seguente viene illustrato come denominare i file in uno scenario in cui l'opzione relativa al nome di file viene specificata come C:\OutputFiles\MyOutput.xel:  
  
-   primo file creato - C:\OutputFiles\MyOutput_0_128500310259380000.xel  
  
-   primo file di rollover - C:\OutputFiles\MyOutput_0_128505831770890000.xel  
  
-   secondo file di rollover - C:\OutputFiles\MyOutput_0_132410772966237000.xel  
  
## <a name="adding-the-target-to-a-session"></a>Aggiunta della destinazione a una sessione  
 Per aggiungere la destinazione file dell'evento a una sessione di eventi estesi, è necessario includere le istruzioni seguenti quando si crea o si modifica una sessione eventi, sostituendo *file_name* con il nome e il percorso del file desiderati:  
  
```  
ADD TARGET package0.event_file(  
   SET filename='file_name.xel')  
```  
  
## <a name="reviewing-the-target-output"></a>Analisi dell'output di destinazione  
 Per esaminare l'output dalla destinazione file, è necessario usare la funzione sys.fn_xe_file_target_read_file. È consigliabile eseguire il cast dei dati come XML. È possibile usare la sintassi seguente, sostituendo *file_name* con il nome e il percorso del file specificati quando è stata aggiunta la destinazione:  
  
```  
SELECT *, CAST(event_data AS XML) AS 'event_data_XML'  
FROM sys.fn_xe_file_target_read_file('file_name*.xel', NULL, NULL, NULL)  
```  
  
## <a name="see-also"></a>Vedere anche  
 [SQL Server destinazioni degli eventi estesi](../../2014/database-engine/sql-server-extended-events-targets.md)   
 [sys. fn_xe_file_target_read_file &#40;&#41;Transact-SQL](/sql/relational-databases/system-functions/sys-fn-xe-file-target-read-file-transact-sql)   
 [CREARE una sessione eventi &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-event-session-transact-sql)   
 [ALTER EVENT SESSION &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-event-session-transact-sql)  
  
  
