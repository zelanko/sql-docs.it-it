---
title: sp_removedbreplication (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_removedbreplication
- sp_removedbreplication_TSQL
helpviewer_keywords:
- sp_removedbreplication
ms.assetid: cb98d571-d1eb-467b-91f7-a6e091009672
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0965c656c5c6b0cef690bb3fbaa7bbc2a7965104
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52747693"
---
# <a name="spremovedbreplication-transact-sql"></a>sp_removedbreplication (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Questa stored procedure rimuove tutti gli oggetti di replica nel database di pubblicazione dell'istanza del server di pubblicazione di SQL Server nel database di sottoscrizione dell'istanza del sottoscrittore di SQL Server. Avviare l'esecuzione nel database appropriato oppure, se l'esecuzione è nel contesto di un altro database nella stessa istanza, specificare il database in cui gli oggetti di replica devono essere rimossi. Questa procedura non rimuove gli oggetti di altri database, ad esempio il database di distribuzione.  
  
> [!NOTE]  
>  È consigliabile utilizzare questa procedura solo se gli altri metodi di rimozione degli oggetti di replica hanno esito negativo.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_removedbreplication [ [ @dbname = ] 'dbname' ]  
    [ , [ @type = ] type ]   
```  
  
## <a name="arguments"></a>Argomenti  
 [  **@dbname=**] **'***dbname***'**  
 Nome del database. *dbname* è di tipo **sysname**e il valore predefinito è NULL. Quando è NULL, viene utilizzato il database corrente.  
  
 [ **@type** =] *tipo*  
 Tipo di replica per cui gli oggetti del database vengono rimossi. *tipo di* viene **nvarchar(5** e può essere uno dei valori seguenti.  
  
|||  
|-|-|  
|**TRAN**|Rimuove gli oggetti di pubblicazione correlati alla replica transazionale.|  
|**merge**|Rimuove gli oggetti di pubblicazione correlati alla replica di tipo merge.|  
|**entrambi** (impostazione predefinita)|Rimuove tutti gli oggetti di pubblicazione correlati alla replica.|  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 **sp_removedbreplication** viene utilizzata in tutti i tipi di replica.  
  
 **sp_removedbreplication** è utile quando si ripristina un database replicato che non è presenti oggetti di replica che devono essere ripristinati.  
  
 **sp_removedbreplication** non può essere usato su un database contrassegnato come di sola lettura.  
  
## <a name="example"></a>Esempio  
 [!code-sql[HowTo#sp_removedbreplication](../../relational-databases/replication/codesnippet/tsql/sp-removedbreplication-t_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server possono eseguire **sp_removedbreplication**.  
  
## <a name="example"></a>Esempio  
  
```  
-- Remove replication objects from the subscription database on MYSUB.  
DECLARE @subscriptionDB AS sysname  
SET @subscriptionDB = N'AdventureWorksReplica'  
  
-- Remove replication objects from a subscription database (if necessary).  
USE master  
EXEC sp_removedbreplication @subscriptionDB  
GO  
  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Disabilitare la pubblicazione e la distribuzione](../../relational-databases/replication/disable-publishing-and-distribution.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
