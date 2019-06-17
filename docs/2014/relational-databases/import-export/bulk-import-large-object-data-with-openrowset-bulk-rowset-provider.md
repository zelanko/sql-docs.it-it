---
title: Importazione BULK LOB tramite il Provider di set di righe OPENROWSET Bulk (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: f6fe945ea90a150397abecfd83f0ce1c945f217c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66012106"
---
# <a name="bulk-import-large-object-data-by-using-the-openrowset-bulk-rowset-provider-sql-server"></a>Importazione bulk di dati di tipo LOB tramite il provider di set di righe con lettura bulk OPENROWSET (SQL Server)
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
 [Importazione di dati per operazioni bulk utilizzando BULK INSERT o OPENROWSET&#40;BULK...&#41; &#40;SQL Server&#41;](import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md)   
 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)   
 [Mantenimento dei valori Null o utilizzo dei valori predefiniti durante un'importazione bulk &#40;SQL Server&#41;](keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)   
 [Utilità bcp](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)  
  
  
