---
title: MSSQLSERVER_601 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- "601"
helpviewer_keywords:
- 601 (Database Engine error)
ms.assetid: 2039cc0a-9a43-4369-a04a-935e384388b6
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9aebe73ac73ee09ed2ba6de9162877d0e70bc7e6
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62867730"
---
# <a name="mssqlserver_601"></a>MSSQLSERVER_601
    
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|601|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico||  
|Testo del messaggio|A causa di uno spostamento di dati, non è possibile continuare l'analisi tramite NOLOCK.|  
  
## <a name="explanation"></a>Spiegazione  
 Il [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] non è in grado di continuare l'esecuzione della query perché sta tentando di leggere dati che sono stati aggiornati o eliminati da un'altra transazione. La query sta utilizzando l'hint di blocco NOLOCK o il livello di isolamento della transazione READ UNCOMMITTED.  
  
 L'accesso a dati in corso di modifica da parte di un'altra transazione viene in genere negato perché i dati risultano bloccati. L'hint di blocco NOLOCK e il livello di isolamento della transazione READ UNCOMMITTED consentono tuttavia a una query di leggere dati bloccati da un'altra transazione. Tale lettura è definita lettura dirty perché consente la lettura di valori di cui non è ancora stato eseguito il commit e che sono soggetti a modifica.  
  
## <a name="user-action"></a>Azione dell'utente  
 L'errore annulla la query. Eseguire nuovamente la query o rimuovere l'hint di blocco NOLOCK.  
  
## <a name="see-also"></a>Vedere anche  
 [MSSQLSERVER_605](mssqlserver-605-database-engine-error.md)   
 [Hint di tabella &#40;Transact-SQL&#41;](/sql/t-sql/queries/hints-transact-sql-table)   
 [SELECT &#40;Transact-SQL&#41;](/sql/t-sql/queries/select-transact-sql)   
 [SET TRANSACTION ISOLATION LEVEL &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-transaction-isolation-level-transact-sql)  
  
  
