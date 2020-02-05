---
title: MSSQL_ENG014005 | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG014005 error
ms.assetid: f168f0d6-cb11-45d4-9781-c374d7f388ee
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 8888d5f2b00115be6cc86fe5484135e82851d574
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "76286297"
---
# <a name="mssql_eng014005"></a>MSSQL_ENG014005
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
    
## <a name="message-details"></a>Dettagli messaggio  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|14005|  
|Origine evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nome simbolico||  
|Testo del messaggio|Impossibile eliminare la pubblicazione. Vi è associata una sottoscrizione.|  
  
## <a name="explanation"></a>Spiegazione  
 Si è tentato di eliminare una pubblicazione alla quale sono associate una o più sottoscrizioni. È possibile eliminare una pubblicazione solo se non vi sono sottoscrizioni associate.  
  
## <a name="user-action"></a>Azione dell'utente  
 Eliminare le sottoscrizioni prima di eliminare la pubblicazione. Se si utilizza [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] per eliminare la pubblicazione, si potrà scegliere di eliminare automaticamente tutte le sottoscrizioni associate prima di eliminare la pubblicazione. Se si utilizzano stored procedure, è necessario prima eliminare esplicitamente le sottoscrizioni. Per ulteriori informazioni, vedere [Delete a Push Subscription](../../relational-databases/replication/delete-a-push-subscription.md) e [Delete a Pull Subscription](../../relational-databases/replication/delete-a-pull-subscription.md).  
  
 Se apparentemente non vi sono sottoscrizioni associate alla pubblicazione o se viene visualizzato questo errore durante la creazione di una pubblicazione, potrebbe esserci una sottoscrizione precedente che non è stata eliminata completamente dopo la rimozione. Eseguire [sp_removedbreplication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md) sul database per rimuovere tutti gli oggetti e le impostazioni inerenti alla replica.  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento a errori ed eventi &#40;replica&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  
