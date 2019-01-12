---
title: sp_copysnapshot (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_copysnapshot
- sp_copysnapshot_TSQL
helpviewer_keywords:
- sp_copysnapshot
ms.assetid: a012a32f-6f26-45bf-8046-b51cd7fec455
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d3c8037bdccc0b04e2c11399f09e5a99c109df65
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2019
ms.locfileid: "54134111"
---
# <a name="spcopysnapshot-transact-sql"></a>sp_copysnapshot (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Copia la cartella snapshot della pubblicazione specificata nella cartella indicata nel **@destination_folder**. Questa stored procedure viene eseguita nel database di pubblicazione del server di pubblicazione. Risulta utile per la copia di uno snapshot su supporti rimovibili, quali un CD-ROM.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_copysnapshot [ @publication = ] 'publication', [ @destination_folder = ] 'destination_folder' ]  
    [ , [ @subscriber = ] 'subscriber' ]  
    [ , [ @subscriber_db = ] 'subscriber_db' ]  
```  
  
## <a name="arguments"></a>Argomenti  
 [  **@publication=**] **'**_pubblicazione_**'**  
 Nome della pubblicazione di cui si desidera copiare la cartella snapshot. *pubblicazione* viene **sysname**, non prevede alcun valore predefinito.  
  
 [  **@destination_folder=**] **'**_destination_folder_**'**  
 Nome della cartella in cui si desidera copiare il contenuto della cartella snapshot della pubblicazione. *destination_folder*viene **nvarchar(255**, non prevede alcun valore predefinito. Il *destination_folder* può essere un percorso alternativo, ad esempio in un altro server, in un'unità di rete o su supporti rimovibili (ad esempio CD-ROM o un disco rimovibile).  
  
 [  **@subscriber=**] **'**_sottoscrittore_**'**  
 Nome del Sottoscrittore. *Sottoscrittore* is sysname con valore predefinito è NULL.  
  
 [  **@subscriber_db=**] **'**_subscriber_db_**'**  
 Nome del database di sottoscrizione. *subscriber_db* is sysname con valore predefinito è NULL.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 **sp_copysnapshot** viene utilizzata in tutti i tipi di replica. I sottoscrittori che eseguono [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 e versioni precedenti non è possibile usare la posizione dello snapshot alternativo.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server oppure **db_owner** ruolo predefinito del database possono eseguire **sp_copysnapshot**.  
  
## <a name="see-also"></a>Vedere anche  
 [Posizioni alternative della cartella snapshot](../../relational-databases/replication/snapshot-options.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
