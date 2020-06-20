---
title: MSSQL_ENG004929 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG004929 error
ms.assetid: 1d9b1d88-1fbf-4089-b392-687d3b0220ca
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: b202b28eabe1feb1ed180bda0d58d2e84c7d10d4
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85049265"
---
# <a name="mssql_eng004929"></a>MSSQL_ENG004929
    
## <a name="message-details"></a>Dettagli messaggio  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|4929|  
|Origine evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nome simbolico||  
|Testo del messaggio|Impossibile modificare %S_MSG '%.*ls' perché è in corso di pubblicazione per la replica.|  
  
## <a name="explanation"></a>Spiegazione  
 Questo errore si verifica in genere quando si tenta di eliminare il vincolo di chiave primaria di una tabella pubblicata per la replica transazionale. Nella replica transazionale è necessaria una chiave primaria per ogni tabella pubblicata, pertanto il vincolo non può essere eliminato.  
  
## <a name="user-action"></a>Azione dell'utente  
 Per eliminare il vincolo, eliminare innanzitutto l'articolo associato alla tabella. Per altre informazioni, vedere [Aggiungere ed eliminare articoli in pubblicazioni esistenti](publish/add-articles-to-and-drop-articles-from-existing-publications.md). Se questo errore si verifica in un database non replicato, eseguire [sp_removedbreplication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql) per verificare che gli oggetti nel database non siano contrassegnati come replicati.  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento a errori ed eventi &#40;replica&#41;](errors-and-events-reference-replication.md)  
  
  
