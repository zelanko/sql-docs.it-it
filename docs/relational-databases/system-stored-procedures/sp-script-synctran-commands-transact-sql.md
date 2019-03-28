---
title: sp_script_synctran_commands (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_script_synctran_commands
- sp_script_synctran_commands_TSQL
helpviewer_keywords:
- sp_script_synctran_commands
ms.assetid: f132694a-dd05-405b-9d84-21acce9e564a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a9ee35eb4c5d67ff50f4f08c1cfa29596e27aec2
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58536177"
---
# <a name="spscriptsynctrancommands-transact-sql"></a>sp_script_synctran_commands (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Genera uno script che contiene il **sp_addsynctrigger** chiamate da applicare nei Sottoscrittori per le sottoscrizioni aggiornabili. Eventuale **sp_addsynctrigger** chiamare per ogni articolo nella pubblicazione. Lo script generato contiene anche il **sp_addqueued_artinfo** chiamate che creano le **MSsubsciption_articles** tabella in cui è necessaria per l'elaborazione delle pubblicazioni in coda. Questa stored procedure viene eseguita nel database di pubblicazione del server di pubblicazione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_script_synctran_commands [@publication = ] 'publication'  
    [ , [@article = ] 'article']  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @publication = ] 'publication'` È il nome della pubblicazione da inserire nello script. *pubblicazione* viene **sysname**, non prevede alcun valore predefinito.  
  
`[ @article = ] 'article'` È il nome dell'articolo da inserire nello script. *articolo* viene **sysname**, il valore predefinito è **tutti**, che consente di specificare tutti gli articoli vengono inseriti nello script.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="results-set"></a>Set di risultati  
 **sp_script_synctran_commands** restituisce un set di risultati è costituito da una singola **nvarchar (4000)** colonna. Il set di risultati forma gli script completi necessari per creare entrambe le **sp_addsynctrigger** e **sp_addqueued_artinfo** chiamate da applicare nei Sottoscrittori.  
  
## <a name="remarks"></a>Note  
 **sp_script_synctran_commands** viene utilizzata nella replica snapshot e transazionale.  
  
 **sp_addqueued_artinfo** viene usato per le sottoscrizioni aggiornabili in coda.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server oppure **db_owner** ruolo predefinito del database possono eseguire **sp_script_synctran_commands**.  
  
## <a name="see-also"></a>Vedere anche  
 [sp_addsynctriggers &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsynctriggers-transact-sql.md)   
 [sp_addqueued_artinfo &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addqueued-artinfo-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
