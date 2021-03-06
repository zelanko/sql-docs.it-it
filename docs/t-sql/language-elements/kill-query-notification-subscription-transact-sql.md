---
title: KILL QUERY NOTIFICATION SUBSCRIPTION
description: Rimuovere le sottoscrizioni di notifica delle query da un'istanza. Questa istruzione può rimuovere una sottoscrizione specifica oppure tutte le sottoscrizioni.
titleSuffix: SQL Server (Transact-SQL)
ms.custom: seo-lt-2019
ms.date: 07/27/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- KILL QUERY NOTIFICATION SUBSCRIPTION
- KILL_QUERY_NOTIFICATION_SUBSCRIPTION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- KILL QUERY NOTIFICATION SUBSCRIPTION statement
- removing subscriptions
- subscriptions [SQL Server query notifications], stopping
- query notifications [SQL Server], subscriptions
ms.assetid: 8aeadf51-286c-4748-bef2-d25858b250bf
author: rothja
ms.author: jroth
ms.openlocfilehash: 0434642595fb334c138e1c3d1764384760a38407
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/19/2020
ms.locfileid: "92193371"
---
# <a name="kill-query-notification-subscription-transact-sql"></a>KILL QUERY NOTIFICATION SUBSCRIPTION (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Rimuove le sottoscrizioni di notifica delle query dall'istanza. Questa istruzione può rimuovere una sottoscrizione specifica oppure tutte le sottoscrizioni.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```syntaxsql
KILL QUERY NOTIFICATION SUBSCRIPTION   
   { ALL | subscription_id }  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argomenti
 ALL  
 Rimuove tutte le sottoscrizioni nell'istanza.  
  
 *subscription_id*  
 Rimuove la sottoscrizione associata all'ID sottoscrizione definito da *subscription_id*.  
  
## <a name="remarks"></a>Osservazioni  
 L'istruzione KILL QUERY NOTIFICATION SUBSCRIPTION rimuove le sottoscrizioni di notifica delle query senza generare un messaggio di notifica.  
  
 *subscription_id* corrisponde all'ID della sottoscrizione visualizzato nella vista a gestione dinamica [sys.dm_qn_subscriptions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/query-notifications-sys-dm-qn-subscriptions.md).  
  
 Se l'ID sottoscrizione specificato non esiste, l'istruzione genera un errore.  
  
## <a name="permissions"></a>Autorizzazioni  
 L'autorizzazione di esecuzione per questa istruzione è limitata ai membri del ruolo predefinito del server **sysadmin**.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-removing-all-query-notification-subscriptions-in-the-instance"></a>R. Rimozione di tutte le sottoscrizioni di notifica delle query nell'istanza  
 Nell'esempio seguente vengono rimosse tutte le sottoscrizioni di notifica delle query nell'istanza.  
  
```sql  
KILL QUERY NOTIFICATION SUBSCRIPTION ALL ;  
```  
  
### <a name="b-removing-a-single-query-notification-subscription"></a>B. Rimozione di una sottoscrizione di notifica delle query  
 Nell'esempio seguente viene rimossa la sottoscrizione di notifica delle query associata all'ID `73`.  
  
```sql  
KILL QUERY NOTIFICATION SUBSCRIPTION 73 ;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [sys.dm_qn_subscriptions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/query-notifications-sys-dm-qn-subscriptions.md)  
  
  
