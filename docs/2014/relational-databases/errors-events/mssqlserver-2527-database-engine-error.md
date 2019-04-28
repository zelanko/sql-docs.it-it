---
title: MSSQLSERVER_2527 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 2527 (Database Engine error)
ms.assetid: 1cef90ef-9c39-44e6-bc7f-316c8f53c10c
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f1d2bd9bd3ee1cc26c0bd488af0dd7891d2a8741
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62868862"
---
# <a name="mssqlserver2527"></a>MSSQLSERVER_2527
    
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|2527|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|DBCC_INDEX_FILEGROUP_IS_OFFLINE|  
|Testo del messaggio|Impossibile elaborare l'indice I_NAME della tabella O_NAME perché il filegroup F_NAME è offline.|  
  
## <a name="explanation"></a>Spiegazione  
 Questo messaggio informativo indica che non è possibile verificare l'indice perché uno dei filegroup che archivia i dati dell'indice è offline. Lo stato dei file di un filegroup determina la disponibilità dell'intero filegroup. Un filegroup è disponibile se tutti i file in esso inclusi sono online. In assenza di altri problemi, tutti gli altri indici dello stesso oggetto verranno verificati.  
  
## <a name="user-action"></a>Azione dell'utente  
 Per visualizzare lo stato dei file per il filegroup specificato, eseguire una query sulla vista del catalogo **sys.database_files** o **sys.master_files**.  
  
 Ripristinare il file offline da un backup.  
  
## <a name="see-also"></a>Vedere anche  
 [sys.database_files &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-files-transact-sql)   
 [sys.master_files &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-master-files-transact-sql)   
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)  
  
  
