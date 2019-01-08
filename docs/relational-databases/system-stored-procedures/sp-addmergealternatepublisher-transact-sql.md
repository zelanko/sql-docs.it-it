---
title: sp_addmergealternatepublisher (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addmergealternatepublisher_TSQL
- sp_addmergealternatepublisher
helpviewer_keywords:
- sp_addmergealternatepublisher
ms.assetid: de46e0b1-d946-4021-bff6-2d8e3187656d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: caaf907b0db55306ebd341ed727174f3531c947f
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52777739"
---
# <a name="spaddmergealternatepublisher-transact-sql"></a>sp_addmergealternatepublisher (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Consente a un Sottoscrittore di utilizzare un partner di sincronizzazione alternativo. È necessario che le proprietà della pubblicazione consentano ai Sottoscrittori di eseguire la sincronizzazione con altri server di pubblicazione. Questa stored procedure viene eseguita nel database di sottoscrizione del Sottoscrittore.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_addmergealternatepublisher [ @publisher= ] 'publisher'  
          , [ @publisher_db= ] 'publisher_db'  
          , [ @publication= ] 'publication'  
          , [ @alternate_publisher= ] 'alternate_synchronization_partner'  
          , [ @alternate_publisher_db= ] 'alternate_publisher_db'  
          , [ @alternate_publication= ] 'alternate_synchronization_partner'  
     , [ @alternate_distributor= ] 'alternate_distributor'   
    [ , [ @friendly_name= ] 'friendly_name' ]   
    [ , [ @reserved= ] 'reserved' ]  
```  
  
## <a name="arguments"></a>Argomenti  
 [  **@publisher=**] **'***publisher***'**  
 Nome del server di pubblicazione. *server di pubblicazione* viene **sysname**, non prevede alcun valore predefinito.  
  
 [ **@publisher_db=**] **'***publisher_db***'**  
 Nome del database di pubblicazione. *publisher_db* viene **sysname**, non prevede alcun valore predefinito.  
  
 [  **@publication=**] **'***pubblicazione***'**  
 Nome della pubblicazione. *pubblicazione* viene **sysname**, non prevede alcun valore predefinito.  
  
 [  **@alternate_publisher=**] **'***alternate_synchronization_partner***'**  
 Nome del server di pubblicazione alternativo. *alternate_synchronization_partner* viene **sysname**, non prevede alcun valore predefinito.  
  
 [  **@alternate_publisher_db=**] **'***alternate_publisher_db***'**  
 Nome del database di pubblicazione nel server di pubblicazione alternativo. *alternate_publisher_db* viene **sysname**, non prevede alcun valore predefinito.  
  
 [  **@alternate_publication=**] **'***alternate_synchronization_partner***'**  
 Nome della pubblicazione nel partner di sincronizzazione alternativo. *alternate_synchronization_partner* viene **sysname**, non prevede alcun valore predefinito.  
  
 [  **@alternate_distributor=**] **'***alternate_distributor***'**  
 Nome del server di distribuzione per il partner di sincronizzazione alternativo. *alternate_distributor* viene **sysname**, non prevede alcun valore predefinito.  
  
 [  **@friendly_name=**] **'***friendly_name***'**  
 Nome visualizzato utilizzato per identificare un partner di sincronizzazione alternativo determinato dall'associazione del server di pubblicazione, della pubblicazione e del server di distribuzione. *friendly_name* viene **nvarchar(255**, con un valore predefinito è NULL.  
  
 [  **@reserved=**] **'***riservato***'**  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 **sp_addmergealternatepublisher** viene utilizzata nella replica di tipo merge.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server oppure **db_owner** ruolo predefinito del database possono eseguire **sp_addmergealternatepublisher**.  
  
## <a name="see-also"></a>Vedere anche  
 [sp_dropmergealternatepublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergealternatepublisher-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
