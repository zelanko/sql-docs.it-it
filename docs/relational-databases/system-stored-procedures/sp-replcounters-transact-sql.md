---
title: sp_replcounters (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_replcounters
- sp_replcounters_TSQL
helpviewer_keywords:
- sp_replcounters
ms.assetid: fe585b1f-edda-421f-81d6-8a03a3a535d2
author: stevestein
ms.author: sstein
ms.openlocfilehash: 12ddbfe11a2b1a29dadaacde845f96e70959bebb
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2019
ms.locfileid: "68770998"
---
# <a name="spreplcounters-transact-sql"></a>sp_replcounters (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Restituisce le statistiche di replica relative a latenza, velocità effettiva e numero delle transazioni per ogni database pubblicato. Questa stored procedure viene eseguita in qualsiasi database del server di pubblicazione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_replcounters  
  
```  
  
## <a name="result-sets"></a>Set di risultati  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**Database**|**sysname**|Nome del database.|  
|**Transazioni replicate**|**int**|Numero di transazioni nel log in attesa di recapito al database di distribuzione.|  
|**Velocità di replica Trans/sec**|**float**|Numero medio di transazioni al secondo recapitate al database di distribuzione.|  
|**Latenza di replica**|**float**|Tempo medio di permanenza delle transazioni nel log prima della distribuzione, espresso in secondi.|  
|**Replbeginlsn**|**binary(10)**|Numero di sequenza del file di log (LSN) corrispondente al punto di troncamento corrente nel log.|  
|**Replnextlsn**|**binary(10)**|LSN del record di commit successivo in attesa di recapito al database di distribuzione.|  
  
## <a name="remarks"></a>Note  
 **sp_replcounters** viene utilizzato nella replica transazionale.  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'appartenenza al ruolo predefinito del database **db_owner** o del ruolo predefinito del server **sysadmin** .  
  
## <a name="see-also"></a>Vedere anche  
 [sp_replcmds &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md)   
 [sp_repldone &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-repldone-transact-sql.md)   
 [sp_replflush &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replflush-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
