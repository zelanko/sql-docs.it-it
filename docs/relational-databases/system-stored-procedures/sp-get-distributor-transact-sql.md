---
title: sp_get_distributor (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_get_distributor
- sp_get_distributor_TSQL
helpviewer_keywords:
- sp_get_distributor
ms.assetid: f0134448-bc17-4f2f-bd81-619351ce56ac
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ccdc8529bb62e4e1db15f0a5ea85a64c5b679abf
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62520995"
---
# <a name="spgetdistributor-transact-sql"></a>sp_get_distributor (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Determina se in un server è installato un server di distribuzione. Questa stored procedure viene eseguita in qualsiasi database del computer in cui viene cercato il server di distribuzione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_get_distributor   
```  
  
## <a name="result-sets"></a>Set di risultati  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**installed**|**int**|**0** = No. **1** = Sì|  
|**server di distribuzione**|**sysname**|Nome del server di distribuzione|  
|**database di distribuzione installato**|**int**|**0** = No. **1** = Sì|  
|**è autore di distribuzione**|**int**|**0** = No. **1** = Sì|  
|**con server di pubblicazione di distribuzione remoto**|**int**|**0** = No. **1** = Sì|  
  
## <a name="remarks"></a>Note  
 **sp_get_distributor** viene usato principalmente dai [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] in snapshot, transazionale e di tipo merge.  
  
## <a name="permissions"></a>Permissions  
 Qualsiasi utente può eseguire **sp_get_distributor**. Un set di risultati non NULL viene restituito quando la stored procedure viene eseguita dai membri del **db_owner** oppure **replmonitor** ruoli predefiniti del database nel database di distribuzione o i membri del  **db_owner** ruolo predefinito del database su almeno un database pubblicato. Un set di risultati non NULL viene restituito anche quando questa stored procedure viene eseguita dagli utenti nell'elenco di accesso (PAL) di almeno un database pubblicato o nell'elenco di accesso del database di distribuzione per un Server di pubblicazione non SQL, possono anche eseguire **sp _get_distributor**.  
  
## <a name="see-also"></a>Vedere anche  
 [Configurare la pubblicazione e la distribuzione](../../relational-databases/replication/configure-publishing-and-distribution.md)   
 [Script di informazioni su database di distribuzione e server di pubblicazione](../../relational-databases/replication/administration/distributor-and-publisher-information-script.md)   
 [Stored procedure per la replica &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
