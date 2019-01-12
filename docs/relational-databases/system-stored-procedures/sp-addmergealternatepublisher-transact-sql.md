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
ms.openlocfilehash: 21d0ea34f3521333976ce00a3f5b823c3fcb816a
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2019
ms.locfileid: "54129301"
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
 [  **@publisher=**] **'**_editore_**'**  
 Nome del server di pubblicazione. *server di pubblicazione* viene **sysname**, non prevede alcun valore predefinito.  
  
 [  **@publisher_db=**] **'**_publisher_db_**'**  
 Nome del database di pubblicazione. *publisher_db* viene **sysname**, non prevede alcun valore predefinito.  
  
 [  **@publication=**] **'**_pubblicazione_**'**  
 Nome della pubblicazione. *pubblicazione* viene **sysname**, non prevede alcun valore predefinito.  
  
 [  **@alternate_publisher=**] **'**_alternate_synchronization_partner_**'**  
 Nome del server di pubblicazione alternativo. *alternate_synchronization_partner* viene **sysname**, non prevede alcun valore predefinito.  
  
 [  **@alternate_publisher_db=**] **'**_alternate_publisher_db_**'**  
 Nome del database di pubblicazione nel server di pubblicazione alternativo. *alternate_publisher_db* viene **sysname**, non prevede alcun valore predefinito.  
  
 [  **@alternate_publication=**] **'**_alternate_synchronization_partner_**'**  
 Nome della pubblicazione nel partner di sincronizzazione alternativo. *alternate_synchronization_partner* viene **sysname**, non prevede alcun valore predefinito.  
  
 [  **@alternate_distributor=**] **'**_alternate_distributor_**'**  
 Nome del server di distribuzione per il partner di sincronizzazione alternativo. *alternate_distributor* viene **sysname**, non prevede alcun valore predefinito.  
  
 [  **@friendly_name=**] **'**_friendly_name_**'**  
 Nome visualizzato utilizzato per identificare un partner di sincronizzazione alternativo determinato dall'associazione del server di pubblicazione, della pubblicazione e del server di distribuzione. *friendly_name* viene **nvarchar(255**, con un valore predefinito è NULL.  
  
 [  **@reserved=**] **'**_riservato_**'**  
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
  
  
