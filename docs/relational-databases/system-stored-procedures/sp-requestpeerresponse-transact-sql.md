---
description: sp_requestpeerresponse (Transact-SQL)
title: sp_requestpeerresponse (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_requestpeerresponse_TSQL
- sp_requestpeerresponse
helpviewer_keywords:
- sp_requestpeerresponse
ms.assetid: cbe13c22-4d7d-4a36-b194-7a13ce68ef27
author: markingmyname
ms.author: maghan
ms.openlocfilehash: d07204928403d8ba99aa49688e51239dfdf08804
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/08/2020
ms.locfileid: "89543110"
---
# <a name="sp_requestpeerresponse-transact-sql"></a>sp_requestpeerresponse (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Quando viene eseguita da un nodo in una topologia peer-to-peer, questa procedura richiede una risposta da ogni altro nodo della topologia. Tramite l'esecuzione di questa procedura e l'analisi delle risposte corrispondenti è possibile verificare che tutti i precedenti comandi siano stati recapitati ai nodi che inviano una risposta. Questa stored procedure viene eseguita in qualsiasi database del nodo richiedente.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_requestpeerresponse [ @publication = ] 'publication'  
    [ , [ @description = ] 'description'  
    [ , [ @request_id = ] request_id OUTPUT ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @publication = ] 'publication'` Nome della pubblicazione in una topologia peer-to-peer per la quale è in corso la verifica dello stato. *Publication* è di **tipo sysname**e non prevede alcun valore predefinito.  
  
`[ @description = ] 'description'` Informazioni definite dall'utente che possono essere utilizzate per identificare le singole richieste di stato. *Description* è di **tipo nvarchar (4000)** e il valore predefinito è null.  
  
`[ @request_id = ] request_id` Restituisce l'ID della nuova richiesta. *request_id* è di **tipo int** ed è un parametro di output. Questo valore può essere utilizzato durante l'esecuzione di [sp_helppeerresponses &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/sp-helppeerresponses-transact-sql.md) per visualizzare tutte le risposte a una richiesta di stato.  
  
## <a name="return-code-values"></a>Valori del codice restituito  
 **0** (esito positivo) o **1** (esito negativo)  
  
## <a name="remarks"></a>Osservazioni  
 **sp_requestpeerresponse** viene utilizzata nella replica transazionale peer-to-peer.  
  
 **sp_requestpeerresponse** viene utilizzato per garantire che tutti i comandi siano stati ricevuti da tutti gli altri nodi prima del ripristino di un database pubblicato in una topologia peer-to-peer. Inoltre, viene utilizzata durante la replica di modifiche DDL (Data Definition Language) apportate mentre un nodo era offline per stimare quando tali modifiche verranno recapitate agli altri nodi.  
  
 Impossibile eseguire **sp_requestpeerresponse** in una transazione definita dall'utente.  
  
## <a name="permissions"></a>Autorizzazioni  
 Solo i membri del ruolo predefinito del server **sysadmin** o del ruolo predefinito del database **db_owner** possono eseguire **sp_requestpeerresponse**.  
  
## <a name="see-also"></a>Vedere anche  
 [sp_deletepeerrequesthistory &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/sp-deletepeerrequesthistory-transact-sql.md)   
 [sp_helppeerrequests &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/sp-helppeerrequests-transact-sql.md)  
  
  
