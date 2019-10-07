---
title: Visualizzare le dimensioni del file sparse di uno snapshot del database (Transact-SQL) | Microsoft Docs
ms.date: 07/28/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.custom: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- snapshots [SQL Server database snapshots], sparse files
- space [SQL Server], sparse files
- sparse files [SQL Server]
- size [SQL Server], sparse files
- maximum sparse file size
- database snapshots [SQL Server], sparse files
- space [SQL Server], database snapshots
ms.assetid: 1867c5f8-d57c-46d3-933d-3642ab0a8e24
author: stevestein
ms.author: sstein
ms.openlocfilehash: e2e66a523fbc82d163c24b52f8c2289cdd38fd6f
ms.sourcegitcommit: ffb87aa292fc9b545c4258749c28df1bd88d7342
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/02/2019
ms.locfileid: "71816728"
---
# <a name="view-the-size-of-the-sparse-file-of-a-database-snapshot-transact-sql"></a>Visualizzare le dimensioni del file sparse di uno snapshot del database (Transact-SQL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  In questo argomento si descrive come utilizzare [!INCLUDE[tsql](../../includes/tsql-md.md)] per verificare che un file di database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sia un file sparse e per conoscere le dimensioni effettive e massime. I file sparse, che sono una funzionalità del file system NTFS, vengono utilizzati dagli snapshot di database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!NOTE]  
>  Durante la creazione dello snapshot di database, i file sparse vengono generati utilizzando i nomi di file specificati nell'istruzione CREATE DATABASE. Questi nomi di file sono archiviati in **sys.master_files** nella colonna **physical_name** . In **sys.database_files** , sia nel database di origine sia nello snapshot, nella colonna **physical_name** sono sempre inclusi i nomi dei file del database di origine.  
  
## <a name="verify-that-a-database-file-is-a-sparse-file"></a>Verificare che un file di database sia un file sparse  
  
1.  Nell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  

     Selezionare la colonna **is_sparse** in **sys.database_files** nello snapshot di database oppure in **sys.master_files**. Tramite il valore viene indicato se il file è di tipo sparse, come segue:  
  
     1 = il file è di tipo sparse.  
  
     0 = il file non è di tipo sparse.  
  
## <a name="find-out-the-actual-size-of-a-sparse-file"></a>Conoscere le dimensioni effettive di un file sparse  
  
> [!NOTE]  
>  Le dimensioni dei file sparse aumentano con incrementi di 64 kilobyte (KB) e corrispondono quindi sempre a un multiplo di 64 KB.  
  
 Per visualizzare il numero di byte usati nel disco da ogni file sparse di uno snapshot, eseguire una query nella colonna **size_on_disk_bytes** della DMV [sys.dm_io_virtual_file_stats](../../relational-databases/system-dynamic-management-views/sys-dm-io-virtual-file-stats-transact-sql.md) di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Per visualizzare lo spazio su disco usato da un file sparse, fare clic con il pulsante destro del mouse sul file in Microsoft Windows, scegliere **Proprietà**e quindi verificare il valore in **Dimensioni su disco** .  
  
## <a name="find-out-the-maximum-size-of-a-sparse-file"></a>Per rilevare la dimensione massima di un file sparse  
 La dimensione massima consentita per un file sparse equivale alla dimensione del file di database di origine corrispondente al momento della creazione dello snapshot. Per informazioni su tale dimensione, è possibile eseguire una delle operazioni seguenti:  
  
-   Per utilizzare il prompt dei comandi di Windows:  
  
    1.  Usare i comandi **dir** di Windows.  
  
    2.  Selezionare il file sparse, aprire la finestra di dialogo **Proprietà** relativa a tale file in Windows e verificare il valore **Dimensioni** .  
  
-   Nell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
     Selezionare la colonna **size** in **sys.database_files** nello snapshot del database oppure in **sys.master_files**. Il valore della colonna **size** indica lo spazio massimo, espresso in pagine SQL, consentito per lo snapshot. Questo valore equivale al campo **Dimensioni** di Windows, ma viene rappresentato in termini di numero di pagine SQL nel file. La dimensione in byte è:  
  
     ( *numero_di_pagine* * 8192)  

## <a name="example"></a>Esempio
Lo script seguente mostra le dimensioni su disco in KB per ogni file sparse.  Lo script visualizza anche le dimensioni massime in megabyte che un file sparse può raggiungere.  Eseguire lo script Transact-SQL in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].

```sql
SELECT  DB_NAME(sd.source_database_id) AS [SourceDatabase], 
        sd.name AS [Snapshot],
        mf.name AS [Filename], 
        size_on_disk_bytes/1024 AS [size_on_disk (KB)],
        mf2.size/128 AS [MaximumSize (MB)]
FROM sys.master_files mf
JOIN sys.databases sd
    ON mf.database_id = sd.database_id
JOIN sys.master_files mf2
    ON sd.source_database_id = mf2.database_id
    AND mf.file_id = mf2.file_id
CROSS APPLY sys.dm_io_virtual_file_stats(sd.database_id, mf.file_id)
WHERE mf.is_sparse = 1
AND mf2.is_sparse = 0
ORDER BY 1;
```
  
## <a name="see-also"></a>Vedere anche  
 [Snapshot del database &#40;SQL Server&#41;](../../relational-databases/databases/database-snapshots-sql-server.md)   
 [sys.fn_virtualfilestats &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-virtualfilestats-transact-sql.md)   
 [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [sys.master_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)  
  
  
