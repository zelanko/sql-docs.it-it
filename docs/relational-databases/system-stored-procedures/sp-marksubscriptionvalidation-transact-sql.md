---
title: sp_marksubscriptionvalidation (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_marksubscriptionvalidation
- sp_marksubscriptionvalidation_TSQL
helpviewer_keywords:
- sp_marksubscriptionvalidation
ms.assetid: e68fe0b9-5993-4880-917a-b0f661f8459b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: aad2574457285208b47af26d0729c725a22c05b0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62629186"
---
# <a name="spmarksubscriptionvalidation-transact-sql"></a>sp_marksubscriptionvalidation (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contrassegna la transazione aperta corrente come transazione di convalida a livello di sottoscrizione per il Sottoscrittore specificato. Questa stored procedure viene eseguita nel database di pubblicazione del server di pubblicazione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_marksubscriptionvalidation [ @publication = ] 'publication'  
        , [ @subscriber = ] 'subscriber'  
        , [ @destination_db = ] 'destination_db'  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @publication = ] 'publication'` È il nome della pubblicazione. *pubblicazione* viene **sysname**, non prevede alcun valore predefinito.  
  
`[ @subscriber = ] 'subscriber'` È il nome del sottoscrittore. *Sottoscrittore* è di tipo sysname e non prevede alcun valore predefinito.  
  
`[ @destination_db = ] 'destination_db'` È il nome del database di destinazione. *destination_db* viene **sysname**, non prevede alcun valore predefinito.  
  
`[ @publisher = ] 'publisher'` Specifica un non - [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] server di pubblicazione. *server di pubblicazione* viene **sysname**, con un valore predefinito è NULL.  
  
> [!NOTE]  
>  *server di pubblicazione* non deve essere utilizzato per una pubblicazione a cui appartiene un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] server di pubblicazione.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 **sp_marksubscriptionvalidation** viene utilizzata nella replica transazionale.  
  
 **sp_marksubscriptionvalidation** nepodporuje non [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sottoscrittori.  
  
 Per non - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] i server di pubblicazione non è possibile eseguire **sp_marksubscriptionvalidation** all'interno di una transazione esplicita. perché le transazioni esplicite non sono supportate attraverso la connessione al server collegato utilizzata per l'accesso al server di pubblicazione.  
  
 **sp_marksubscriptionvalidation** deve essere usata in combinazione con [sp_article_validation &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md), specificando il valore **1** per  *subscription_level*e può essere usato con altre chiamate a **sp_marksubscriptionvalidation** per contrassegnare la transazione aperta corrente per altri sottoscrittori.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server oppure **db_owner** ruolo predefinito del database possono eseguire **sp_marksubscriptionvalidation**.  
  
## <a name="example"></a>Esempio  
 È possibile applicare la query seguente al database di pubblicazione per inviare comandi di convalida a livello di sottoscrizione. Tali comandi vengono quindi intercettati dagli agenti di distribuzione dei Sottoscrittori specificati. Si noti che la prima transazione convalida l'articolo '**art1**', mentre la seconda transazione convalida'**art2**'. Si noti anche che le chiamate a **sp_marksubscriptionvalidation** e [sp_article_validation &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md) sono state inserite in una transazione. È consigliabile solo una chiamata a [sp_article_validation &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md) per ogni transazione. Infatti [sp_article_validation &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md) mantiene un blocco condiviso sulla tabella di origine per la durata della transazione. Le transazioni brevi consentono di ottenere la massima concorrenza.  
  
```  
begin tran  
  
exec sp_marksubscriptionvalidation @publication = 'pub1',  
 @subscriber = 'Sub', @destination_db = 'SubDB'  
  
exec sp_marksubscriptionvalidation @publication = 'pub1',  
 @subscriber = 'Sub2', @destination_db = 'SubDB'  
  
exec sp_article_validation @publication = 'pub1', @article = 'art1',  
 @rowcount_only = 0, @full_or_fast = 0, @shutdown_agent = 0,  
 @subscription_level = 1  
  
commit tran  
  
begin tran  
  
exec sp_marksubscriptionvalidation @publication = 'pub1',  
 @subscriber = 'Sub', @destination_db = 'SubDB'  
  
exec sp_marksubscriptionvalidation @publication = 'pub1',  
 @subscriber = 'Sub2', @destination_db = 'SubDB'  
  
exec sp_article_validation @publication = 'pub1', @article = 'art2',  
 @rowcount_only = 0, @full_or_fast = 0, @shutdown_agent = 0,  
 @subscription_level = 1  
  
commit tran  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Convalidare i dati replicati](../../relational-databases/replication/validate-data-at-the-subscriber.md)  
  
  
