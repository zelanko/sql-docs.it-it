---
title: sp_dropmergealternatepublisher (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_dropmergealternatepublisher
- sp_dropmergealternatepublisher_TSQL
helpviewer_keywords:
- sp_dropmergealternatepublisher
ms.assetid: a7dee4e2-2a60-41da-9d1d-6f991d7e2c5e
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1cc29de8227cab3fc9045e7d98d9453146965008
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52773853"
---
# <a name="spdropmergealternatepublisher-transact-sql"></a>sp_dropmergealternatepublisher (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Rimuove un server di pubblicazione alternativo da una pubblicazione di tipo merge. Questa stored procedure viene eseguita nel database di sottoscrizione del Sottoscrittore.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_dropmergealaternatepublisher [ @publisher = ] 'publisher'    , [ @publisher_db = ] 'publisher_db'    , [ @publication = ] 'publication'    , [ @alternate_publisher = ] 'alternate_publisher'    , [ @alternate_publisher_db = ] 'alternate_publisher_db'    , [ @alternate_publication = ] 'alternate_publication'  
```  
  
## <a name="arguments"></a>Argomenti  
 [  **@publisher=**] **'***publisher***'**  
 Nome del server di pubblicazione corrente. *server di pubblicazione*viene **sysname**, non prevede alcun valore predefinito.  
  
 [ **@publisher_db=**] **'***publisher_db***'**  
 Nome del database di pubblicazione corrente. *publisher_db*viene **sysname**, non prevede alcun valore predefinito.  
  
 [  **@publication =**] **'***pubblicazione***'**  
 Nome della pubblicazione corrente. *pubblicazione* viene **sysname**, non prevede alcun valore predefinito.  
  
 [  **@alternate_publisher=**] **'***alternate_publisher***'**  
 Nome del server di pubblicazione alternativo da eliminare come partner alternativo per la sincronizzazione. *alternate_publisher*viene **sysname**, non prevede alcun valore predefinito.  
  
 [  **@alternate_publisher_db=**] **'***alternate_publisher_db***'**  
 Nome del database di pubblicazione da eliminare come database del partner alternativo per la sincronizzazione. *alternate_publisher_db*viene **sysname**, non prevede alcun valore predefinito.  
  
 [  **@alternate_publication=**] **'***alternate_publication***'**  
 Nome della pubblicazione da eliminare come pubblicazione del partner alternativo per la sincronizzazione. *alternate_publication*viene **sysname**, non prevede alcun valore predefinito.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 **sp_dropmergealternatepublisher** viene utilizzata nella replica di tipo merge.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server o il **db_owner** ruolo predefinito del database possono eseguire **sp_dropmergealternatepublisher**.  
  
## <a name="see-also"></a>Vedere anche  
 [sp_addmergealternatepublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergealternatepublisher-transact-sql.md)  
  
  
