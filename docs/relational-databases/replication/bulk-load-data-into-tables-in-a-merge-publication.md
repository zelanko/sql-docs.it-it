---
title: Caricamento bulk dei dati nelle tabelle in una pubblicazione di tipo merge | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- bulk load [SQL Server replication]
- merge replication bulk loading [SQL Server replication]
- sp_addtabletocontents
ms.assetid: 16e6498a-b449-4051-aec4-ea814a2ad993
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 44c3549b04bd2bf534e626764bbc56c688b3ca5f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68085845"
---
# <a name="bulk-load-data-into-tables-in-a-merge-publication"></a>Caricamento bulk dei dati nelle tabelle in una pubblicazione di tipo merge
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Quando i dati vengono caricati nelle tabelle utilizzando [bcp Utility](../../tools/bcp-utility.md) o il comando [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) , per impostazione predefinita, i trigger della replica di tipo merge che gestiscono i dati di rilevamento nella tabella di sistema [MSmerge_contents](../../relational-databases/system-tables/msmerge-contents-transact-sql.md) non vengono attivati. È possibile forzare l'attivazione dei trigger della replica di tipo merge al momento del caricamento dei dati o inserire i metadati di replica generati a livello di programmazione dopo l'operazione di copia bulk utilizzando le stored procedure di replica.  
  
### <a name="to-bulk-load-data-into-tables-published-by-merge-replication-using-the-bcp-utility"></a>Per eseguire il caricamento bulk dei dati nelle tabelle pubblicate mediante la replica di tipo merge utilizzando l'utilità bcp  
  
1.  Nel server di pubblicazione o nel Sottoscrittore eseguire l' [bcp Utility](../../tools/bcp-utility.md) o [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) per inserire i dati in una tabella pubblicata mediante la replica di tipo merge.  
  
2.  Utilizzare uno dei metodi seguenti per assicurarsi che i metadati di replica vengano generati per i dati inseriti.  
  
    -   Eseguire la copia bulk utilizzando l'opzione FIRE_TRIGGERS.  
  
    -   Nel database in cui sono stati inseriti i dati eseguire [sp_addtabletocontents &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addtabletocontents-transact-sql.md). Specificare il nome della tabella nella quale sono stati inseriti i dati per **@table_name** .  
  
  
