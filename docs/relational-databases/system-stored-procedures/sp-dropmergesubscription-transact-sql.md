---
description: sp_dropmergesubscription (Transact-SQL)
title: sp_dropmergesubscription (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_dropmergesubscription_TSQL
- sp_dropmergesubscription
helpviewer_keywords:
- sp_dropmergesubscription
ms.assetid: 34244ae6-bd98-4a6a-bbd3-85f50edfcdc0
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 8d1b10deb11751ba8a8d2c5ee49cda293e695d50
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/08/2020
ms.locfileid: "89538943"
---
# <a name="sp_dropmergesubscription-transact-sql"></a>sp_dropmergesubscription (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Elimina una sottoscrizione di una pubblicazione di tipo merge e l'agente di merge corrispondente. Questa stored procedure viene eseguita nel database di pubblicazione del server di pubblicazione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_dropmergesubscription [ [ @publication= ] 'publication' ]   
    [ , [ @subscriber= ] 'subscriber'    
    [ , [ @subscriber_db= ] 'subscriber_db' ]   
    [ , [ @subscription_type= ] 'subscription_type' ]   
    [ , [ @ignore_distributor = ] ignore_distributor ]   
    [ , [ @reserved = ] reserved ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @publication = ] 'publication'` Nome della pubblicazione. *Publication* è di **tipo sysname**e il valore predefinito è null. È necessario che la pubblicazione esista già e che sia conforme alle regole per gli identificatori.  
  
`[ @subscriber = ] 'subscriber'` Nome del Sottoscrittore. *Subscriber* è di **tipo sysname**e il valore predefinito è null.  
  
`[ @subscriber_db = ] 'subscriber_db'` Nome del database di sottoscrizione. *subscription_database*è di **tipo sysname**e il valore predefinito è null.  
  
`[ @subscription_type = ] 'subscription_type'` Tipo di sottoscrizione. *subscription_type*è di **tipo nvarchar (15)**. i possibili valori sono i seguenti.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|**tutti**|Sottoscrizioni push, pull e anonime.|  
|**Anonimo**|Sottoscrizione anonima.|  
|**push**|Sottoscrizione push.|  
|**tirare**|Sottoscrizione pull.|  
|**both** (impostazione predefinita)|Sottoscrizione sia push che pull.|  
  
`[ @ignore_distributor = ] ignore_distributor` Indica se questo stored procedure viene eseguito senza connettersi al server di distribuzione. *ignore_distributor* è di **bit**e il valore predefinito è **0**. È possibile utilizzare questo parametro per eliminare una sottoscrizione senza eseguire attività di pulizia dei dati nel server di distribuzione. Risulta inoltre utile se è stato necessario reinstallare il server di distribuzione.  
  
`[ @reserved = ] reserved` È riservato per usi futuri. *riservato* è di **bit**e il valore predefinito è **0**.  
  
## <a name="return-code-values"></a>Valori del codice restituito  
 **0** (esito positivo) o **1** (esito negativo)  
  
## <a name="remarks"></a>Osservazioni  
 **sp_dropmergesubscription** viene utilizzata nella replica di tipo merge.  
  
## <a name="example"></a>Esempio  
 [!code-sql[HowTo#sp_dropmergesubscription](../../relational-databases/replication/codesnippet/tsql/sp-dropmergesubscription_1.sql)]  
  
## <a name="permissions"></a>Autorizzazioni  
 Solo i membri del ruolo predefinito del server **sysadmin** o del ruolo predefinito del database **db_owner** possono eseguire **sp_dropmergesubscription**.  
  
## <a name="see-also"></a>Vedere anche  
 [Eliminare una sottoscrizione push](../../relational-databases/replication/delete-a-push-subscription.md)   
 [Eliminare una sottoscrizione pull](../../relational-databases/replication/delete-a-pull-subscription.md)   
 [sp_addmergesubscription &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md)   
 [sp_changemergesubscription &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/sp-changemergesubscription-transact-sql.md)   
 [sp_helpmergesubscription &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/sp-helpmergesubscription-transact-sql.md)  
  
  
