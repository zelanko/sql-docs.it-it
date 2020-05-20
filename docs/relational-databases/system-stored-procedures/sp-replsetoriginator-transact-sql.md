---
title: sp_replsetoriginator (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_replsetoriginator
- sp_replsetoriginator_TSQL
helpviewer_keywords:
- sp_replsetoriginator
ms.assetid: 030e5226-0585-439f-b8cd-36f48367d86d
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 5e1f29f06d7a840ed6628ecd4dc193a4f1c54b82
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/05/2020
ms.locfileid: "82817071"
---
# <a name="sp_replsetoriginator-transact-sql"></a>sp_replsetoriginator (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Utilizzata per richiamare il rilevamento e la gestione di loopback nella replica transazionale bidirezionale. Questa stored procedure viene eseguita nel database di pubblicazione del server di pubblicazione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_replsetoriginator [ @server_name= ] 'server_name'   
    , [ @database_name= ] 'database_name'  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @server_name = ] 'server_name'`Nome del server in cui viene applicata la transazione. *originating_server* è di **tipo sysname**e non prevede alcun valore predefinito.  
  
`[ @database_name = ] 'database_name'`Nome del database in cui viene applicata la transazione. *originating_db* è di **tipo sysname**e non prevede alcun valore predefinito.  
  
## <a name="return-code-values"></a>Valori del codice restituito  
 **0** (esito positivo) o **1** (esito negativo)  
  
## <a name="remarks"></a>Osservazioni  
 **sp_replsetoriginator** viene eseguito dal agente di distribuzione per registrare l'origine delle transazioni applicate dalla replica. Queste informazioni vengono utilizzate per richiamare il rilevamento di loopback per le sottoscrizioni transazionali bidirezionali per cui è stata impostata la proprietà di loopback.  
  
## <a name="permissions"></a>Autorizzazioni  
 Solo i membri del ruolo predefinito del server **sysadmin** nel server di pubblicazione, i membri del ruolo predefinito del database **db_owner** nel database di pubblicazione oppure gli utenti nell'elenco di accesso alla pubblicazione possono eseguire **sp_replsetoriginator**.  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
