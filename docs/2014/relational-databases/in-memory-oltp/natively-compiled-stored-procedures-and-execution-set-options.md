---
title: Stored procedure compilate in modo nativo e opzioni SET di esecuzione | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: c1869cf7-9030-4d18-85d6-0e419a4e9af7
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: eaf7057130cc3d13c0025b92b207efbace339e74
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63131479"
---
# <a name="natively-compiled-stored-procedures-and-execution-set-options"></a>Stored procedure compilate in modo nativo e opzioni SET di esecuzione
  Le opzioni di sessione sono fisse nei blocchi atomici. L'esecuzione di una stored procedure non è interessata dalle opzioni SET di una sessione. Tuttavia, alcune opzioni SET quali SET NOEXEC e SET SHOWPLAN_XML impediscono l'esecuzione delle stored procedure, incluse quelle compilate in modo nativo.  
  
 Quando una stored procedure compilata in modo nativo viene eseguita con una qualsiasi opzione STATISTICS attivata, le statistiche vengono raccolte per la stored procedure completa e non per istruzione. Per altre informazioni, vedere [SET STATISTICS IO &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-statistics-io-transact-sql), [SET STATISTICS PROFILE &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-statistics-profile-transact-sql), [SET STATISTICS TIME &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-statistics-time-transact-sql) e [SET STATISTICS XML &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-statistics-xml-transact-sql). Per ottenere statistiche di esecuzione a livello di singola istruzione in stored procedure compilate in modo nativo, utilizzare una sessione Evento esteso in un evento sp_statement_completed, che viene attivato al completamento di ciascuna singola query nell'esecuzione di una stored procedure. Per altre informazioni sulla creazione di sessioni di evento estesi, vedere [CREATE EVENT SESSION &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-event-session-transact-sql).  
  
 `SHOWPLAN_XML` è supportato per le stored procedure compilate in modo nativo. Le opzioni `SHOWPLAN_ALL` e `SHOWPLAN_TEXT` non sono supportate con le stored procedure compilate in modo nativo.  
  
 L'opzione `SET FMTONLY` non è supportata con le stored procedure compilate in modo nativo. Usare invece [sp_describe_first_result_set &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql).  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure compilate in modo nativo](natively-compiled-stored-procedures.md)  
  
  
