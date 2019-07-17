---
title: sp_browsesnapshotfolder (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_browsesnapshotfolder
- sp_browsesnapshotfolder_TSQL
helpviewer_keywords:
- sp_browsesnapshotfolder
ms.assetid: 0872edf2-4038-4bc1-a68d-05ebfad434d2
author: stevestein
ms.author: sstein
ms.openlocfilehash: a9418970d893eb7423f844582474b5d2f5791dfd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68045971"
---
# <a name="spbrowsesnapshotfolder-transact-sql"></a>sp_browsesnapshotfolder (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce il percorso completo per l'ultimo snapshot generato per una pubblicazione. Questa stored procedure viene eseguita nel database di pubblicazione del server di pubblicazione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_browsesnapshotfolder [@publication= ] 'publication'  
    { [ , [ @subscriber = ] 'subscriber' ]  
 [ , [ @subscriber_db = ] 'subscriber_db' ] }  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @publication = ] 'publication'` È il nome della pubblicazione che contiene l'articolo. *pubblicazione* viene **sysname**, non prevede alcun valore predefinito.  
  
`[ @subscriber = ] 'subscriber'` È il nome del sottoscrittore. *Sottoscrittore* viene **sysname**, con un valore predefinito è NULL.  
  
`[ @subscriber_db = ] 'subscriber_db'` È il nome del database di sottoscrizione. *subscriber_db* viene **sysname**, con un valore predefinito è NULL.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="result-sets"></a>Set di risultati  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**snapshot_folder**|**nvarchar(512)**|Percorso completo della directory snapshot.|  
  
## <a name="remarks"></a>Note  
 **sp_browsesnapshotfolder** viene utilizzata nella replica snapshot e transazionale.  
  
 Se il *sottoscrittore* e *subscriber_db* campi sono NULL, la stored procedure restituisce la cartella snapshot dello snapshot più recente disponibile per la pubblicazione. Se il *sottoscrittore* e *subscriber_db* i campi vengono specificati, la stored procedure restituisce la cartella snapshot per la sottoscrizione specificata. Se per la pubblicazione non è stato generato uno snapshot, viene restituito un set di risultati vuoto.  
  
 Se la pubblicazione è configurata per la generazione di file di snapshot sia nella directory di lavoro che nella cartella snapshot del server di pubblicazione, il set dei risultati include due righe. La prima riga contiene la cartella snapshot della pubblicazione e la seconda la directory di lavoro del server di pubblicazione. **sp_browsesnapshotfolder** è utile per determinare la directory in cui vengono generati i file di snapshot.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server oppure **db_owner** ruolo predefinito del database possono eseguire **sp_browsesnapshotfolder**.  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
