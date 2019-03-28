---
title: sp_resetsnapshotdeliveryprogress (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_resetsnapshotdeliveryprogress
- sp_resetsnapshotdeliveryprogress_TSQL
helpviewer_keywords:
- sp_resetsnapshotdeliveryprogress
ms.assetid: 5df7d86b-d343-4d9b-88b1-74429ed092e6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c791fedcd483024c2bc6d564ce3f774fa2fded77
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58530193"
---
# <a name="spresetsnapshotdeliveryprogress-transact-sql"></a>sp_resetsnapshotdeliveryprogress (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Reimposta il processo di recapito degli snapshot per una sottoscrizione pull in modo che il recapito degli snapshot possa essere riavviato. Questa stored procedure viene eseguita nel database di sottoscrizione del Sottoscrittore.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_resetsnapshotdeliveryprogress [ [ @verbose_level = ] verbose_level ]  
    [ , [ @drop_table = ] 'drop_table' ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @verbose_level = ] verbose_level` Specifica la quantità di informazioni restituite. *verbose_level*viene **int**, il valore predefinito è **1**. Un valore pari **1** significa che un errore viene restituito se non è possibile ottenere i blocchi necessari nella **MSsnapshotdeliveryprogress** tabella, e **0** significa che viene restituito alcun errore.  
  
`[ @drop_table = ] 'drop_table'` Indica se eliminare o troncare la tabella contenente le informazioni sullo stato di avanzamento dello snapshot. *drop_table* viene **nvarchar(5**, il valore predefinito è **FALSE**. FALSE indica che la tabella viene troncata, mentre TRUE indica che la tabella è stata eliminata.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 **sp_resetsnapshotdeliveryprogress** rimuove tutte le righe di **MSsnapshotdeliveryprogress** tabella. Vengono effettivamente rimossi tutti i metadati rimasti nel database di sottoscrizione in seguito alle precedenti fasi dei processi di recapito degli snapshot.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server o il **db_owner** ruolo predefinito del database possono eseguire **sp_resetsnapshotdeliveryprogress**.  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure per la replica &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
