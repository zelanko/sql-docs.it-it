---
title: Visualizzare le dimensioni del file sparse di uno snapshot del database (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
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
manager: craigg
ms.openlocfilehash: c2a7e507e45d8429312834911b7bef5ae1e784c8
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52803683"
---
# <a name="view-the-size-of-the-sparse-file-of-a-database-snapshot-transact-sql"></a>Visualizzare le dimensioni del file sparse di uno snapshot del database (Transact-SQL)
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
>  Le dimensioni dei file sparse aumentano con incrementi di 64 kilobyte (KB) e corrispondono quindi sempre a un multiplo di 64 KB.  
  
 Per visualizzare il numero di byte usati nel disco da ogni file sparse di uno snapshot, eseguire una query nella colonna **size_on_disk_bytes** della DMV [sys.dm_io_virtual_file_stats](/sql/relational-databases/system-dynamic-management-views/sys-dm-io-virtual-file-stats-transact-sql) di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Per visualizzare lo spazio su disco usato da un file sparse, fare clic con il pulsante destro del mouse sul file in Microsoft Windows, scegliere **Proprietà** e quindi verificare il valore in **Dimensioni su disco**.  
  
## <a name="find-out-the-maximum-size-of-a-sparse-file"></a>Per rilevare la dimensione massima di un file sparse  
 La dimensione massima consentita per un file sparse equivale alla dimensione del file di database di origine corrispondente al momento della creazione dello snapshot. Per informazioni su tale dimensione, è possibile eseguire una delle operazioni seguenti:  
  
-   Per utilizzare il prompt dei comandi di Windows:  
  
    1.  Usare i comandi **dir** di Windows.  
  
    2.  Selezionare il file sparse, aprire la finestra di dialogo **Proprietà** relativa a tale file in Windows e verificare il valore **Dimensioni** .  
  
-   Nell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
     Selezionare la colonna **size** in **sys.database_files** nello snapshot del database oppure in **sys.master_files**. Il valore della colonna **size** indica lo spazio massimo, espresso in pagine SQL, consentito per lo snapshot. Questo valore equivale al campo **Dimensioni** di Windows, ma viene rappresentato in termini di numero di pagine SQL nel file. La dimensione in byte è:  
  
     ( *numero_di_pagine* * 8192)  
  
## <a name="see-also"></a>Vedere anche  
 [Snapshot del database &#40;SQL Server&#41;](database-snapshots-sql-server.md)   
 [sys.fn_virtualfilestats &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/sys-fn-virtualfilestats-transact-sql)   
 [sys.database_files &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-files-transact-sql)   
 [sys.master_files &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-master-files-transact-sql)  
  
  
