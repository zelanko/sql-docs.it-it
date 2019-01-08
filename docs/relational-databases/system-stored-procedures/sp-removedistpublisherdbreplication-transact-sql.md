---
title: sp_removedistpublisherdbreplication (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_removedistpublisherdbreplication_TSQL
- sp_removedistpublisherdbreplication
helpviewer_keywords:
- sp_removedistpublisherdbreplication
ms.assetid: 9bfe002a-25b5-4226-bcfb-feb2060d6b4a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d57034b65559e696a9692a1c71e612c7d921661b
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52754643"
---
# <a name="spremovedistpublisherdbreplication-transact-sql"></a>sp_removedistpublisherdbreplication (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Rimuove i metadati di pubblicazione appartenenti a una pubblicazione specifica nel server di distribuzione. La stored procedure viene eseguita nel database di distribuzione del server di distribuzione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_removedistpublisherdbreplication [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
```  
  
## <a name="arguments"></a>Argomenti  
 [  **@publisher=** ] **'***publisher***'**  
 Nome del server di pubblicazione. *server di pubblicazione* viene **sysname**, non prevede alcun valore predefinito.  
  
 [  **@publisher_db=** ] **'***publisher_db***'**  
 Nome del database di pubblicazione. *publisher_db* viene **sysname** non prevede alcun valore predefinito.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 **sp_removedistpublisherdbreplication** utilizzata dalla replica transazionale e snapshot.  
  
 **sp_removedistpublisherdbreplication** viene utilizzato quando sarà necessario creare nuovamente un database pubblicato senza eliminare il database di distribuzione. Vengono rimossi i metadati seguenti:  
  
-   Tutti i metadati della pubblicazione.  
  
-   I metadati di tutti gli articoli che appartengono alla pubblicazione.  
  
-   I metadati di tutte le sottoscrizioni della pubblicazione.  
  
-   I metadati di tutti i processi dell'agente di replica che appartengono alla pubblicazione.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** nel server di distribuzione membri del ruolo predefinito del server di **db_owner** ruolo predefinito del database nel database di distribuzione possono eseguire **sp _ removedistpublisherdbreplication**.  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
