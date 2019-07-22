---
title: MSSQL_ENG020596 | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG020596 error
ms.assetid: fa33627c-2e99-4be3-9424-52ab83446e07
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 1af7a7e98e9d1f03cd0cc05824ef8d740bdb6186
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68091995"
---
# <a name="mssqleng020596"></a>MSSQL_ENG020596
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="message-details"></a>Dettagli messaggio  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|20596|  
|Origine evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nome simbolico||  
|Testo del messaggio|L'agente anonimo può essere eliminato solo da '%s' e dai membri del ruolo db_owner.|  
  
## <a name="explanation"></a>Spiegazione  
 Non si dispone di autorizzazioni sufficienti per eliminare l'agente della sottoscrizione anonima. L'account di accesso usato per chiamare [sp_dropanonymousagent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropanonymousagent-transact-sql.md) deve essere un membro del ruolo predefinito del server **sysadmin** nel server di distribuzione o del ruolo predefinito del database **db_owner** nel database di distribuzione oppure l'utente deve essere lo stesso che ha avviato la prima esecuzione dell'agente.  
  
## <a name="user-action"></a>Azione dell'utente  
 Accedere con le credenziali appropriate ed eseguire **sp_dropanonymousagent**.  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento a errori ed eventi &#40;replica&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  
