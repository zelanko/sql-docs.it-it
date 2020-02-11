---
title: sp_copymergesnapshot (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_copymergesnapshot
- sp_copymergesnapshot_TSQL
helpviewer_keywords:
- sp_copymergesnapshot
ms.assetid: eaecd6e0-8486-4e5d-ace7-8ae75768c0a8
author: stevestein
ms.author: sstein
ms.openlocfilehash: d51f29399487ee156210e96fe598c38288755913
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "72381705"
---
# <a name="sp_copymergesnapshot-transact-sql"></a>sp_copymergesnapshot (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Copia la cartella snapshot della pubblicazione specificata nella cartella elencata nel ** \@destination_folder**. Questa stored procedure viene eseguita nel database di pubblicazione del server di pubblicazione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_copymergesnapshot [ @publication = ] 'publication', [ @destination_folder = ] 'destination_folder'  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @publication = ] 'publication'`Nome della pubblicazione di cui si desidera copiare il contenuto dello snapshot. *Publication* è di **tipo sysname**e non prevede alcun valore predefinito.  
  
`[ @destination_folder = ] 'destination_folder'`Nome della cartella in cui verrà copiato il contenuto dello snapshot di pubblicazione. *destination_folder*è di **tipo nvarchar (255)** e non prevede alcun valore predefinito. Il *destination_folder* può essere un percorso alternativo, ad esempio in un altro server, in un'unità di rete o su un supporto rimovibile, ad esempio CD-ROM o dischi rimovibili.  
  
## <a name="return-code-values"></a>Valori del codice restituito  
 **0** (esito positivo) o **1** (esito negativo)  
  
## <a name="remarks"></a>Osservazioni  
 **sp_copymergesnapshot** viene utilizzata nella replica di tipo merge. I Sottoscrittori che eseguono [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] la versione 7,0 e versioni precedenti non possono utilizzare la posizione alternativa dello snapshot.  
  
## <a name="permissions"></a>Autorizzazioni  
 Solo i membri del ruolo predefinito del server **sysadmin** o del ruolo predefinito del database **db_owner** possono eseguire **sp_copymergesnapshot**.  
  
## <a name="see-also"></a>Vedere anche  
 [Percorsi alternativi cartella snapshot](../../relational-databases/replication/snapshot-options.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
