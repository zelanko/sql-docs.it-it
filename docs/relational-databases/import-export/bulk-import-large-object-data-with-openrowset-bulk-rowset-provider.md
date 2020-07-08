---
title: Importazione bulk di dati di tipo LOB tramite il provider bulk per set di righe OPENROWSET
description: Il provider bulk per set di righe OPENROWSET di SQL Server consente di eseguire un'importazione bulk di dati di grandi dimensioni (LOB, Large Object). I tipi supportati sono varbinary(max), varchar(max) e nvarchar(max).
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- SINGLE_NCLOB option
- bulk rowset providers [SQL Server]
- bulk importing [SQL Server], data formats
- OPENROWSET function, bulk importing large data
- SINGLE_CLOB option
- data formats [SQL Server], large-object data
- large data, bulk imports
- SINGLE_BLOB option
ms.assetid: 171cdd5c-1e47-4bd7-b99a-4f0fd4e10526
author: MashaMSFT
ms.author: mathoma
ms.custom: seo-lt-2019
ms.openlocfilehash: 3c998b1efeb6fff7726161ffb02e240e8a8847f1
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85640705"
---
# <a name="bulk-import-large-object-data-with-openrowset-bulk-rowset-provider-sql-server"></a>Importazione bulk di dati di tipo LOB tramite il provider bulk per set di righe OPENROWSET (SQL Server)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Il provider di set di righe con lettura bulk OPENROWSET di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consente di eseguire un'importazione bulk di un file di dati come dati di grandi dimensioni (LOB, Large Object).  
  
 I tipi di dati LOB (Large Object) supportati dal provider di tipo bulk per set di righe OPENROWSET sono **varbinary**(max) o **image**, **varchar**(max) o **text**e **nvarchar**(max) o **ntext**.  
  
> [!NOTE]  
>  I tipi di dati **image**, **text** e **ntext** sono deprecati.  
  
 La clausola OPENROWSET BULK supporta tre opzioni per l'importazione del contenuto di un file di dati sotto forma di set di righe caratterizzato da una sola riga e una sola colonna. È possibile specificare una di queste opzioni relative ai dati di tipo LOB, invece di utilizzare un file di formato. Le opzioni disponibili sono le seguenti:  
  
 SINGLE_BLOB  
 Legge il contenuto di *data_file* come un'unica riga e restituisce il contenuto come set di righe di tipo **varbinary(max)** con una sola colonna.  
  
 SINGLE_CLOB  
 Legge il contenuto del file di dati specificato come caratteri e restituisce il contenuto come set di righe di tipo **varchar(max)** con una sola riga e una sola colonna, usando le regole di confronto del database corrente, ad esempio un documento di testo o di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Word.  
  
 SINGLE_NCLOB  
 Legge il contenuto del file di dati specificato come Unicode e restituisce il contenuto come set di righe di tipo **nvarchar(max)** con una sola riga e una sola colonna, usando le regole di confronto del database corrente.  
  
## <a name="see-also"></a>Vedere anche  
 [Importazione di dati per operazioni bulk utilizzando BULK INSERT o OPENROWSET&#40;BULK...&#41; &#40;SQL Server&#41;](../../relational-databases/import-export/import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md)   
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [Mantenimento dei valori Null o utilizzo dei valori predefiniti durante un'importazione bulk &#40;SQL Server&#41;](../../relational-databases/import-export/keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)   
 [Utilità bcp](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)  
  
  
