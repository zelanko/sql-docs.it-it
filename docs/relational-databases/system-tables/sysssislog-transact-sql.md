---
title: sysssislog (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysdtslog90_TSQL
- sysdtslog90
dev_langs:
- TSQL
helpviewer_keywords:
- sysssislog system table
ms.assetid: 7fa288a1-81e3-42a0-82f6-8a59019693d0
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: d837049f36e4f7925f8e62a18987f51235f19c14
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68029614"
---
# <a name="sysssislog-transact-sql"></a>sysssislog (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene una riga per ogni voce di log generata da pacchetti o dalle loro attività o contenitori in fase di esecuzione. Questa tabella viene creata nel database msdb al momento dell'installazione di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Se si configura la registrazione nei log in un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] diverso, viene creata una tabella sysssislog con questo formato nel database specificato.  
  
> [!NOTE]  
>  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Scrive le voci di registrazione in questa tabella **soltanto** quando i pacchetti utilizzano il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider di log.  
  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|id|**int**|Identificatore univoco della voce del log.|  
|event|**sysname**|Nome dell'evento che ha generato la voce del log.|  
|computer|**nvarchar**|Computer in cui era in esecuzione il pacchetto al momento della generazione della voce del log.|  
|operator|**nvarchar**|Nome utente della persona che ha eseguito il pacchetto che ha generato la voce del log.|  
|source|**nvarchar**|Nome del file eseguibile nel pacchetto che ha generato la voce del log.|  
|sourceid|**uniqueidentifier**|GUID del file eseguibile nel pacchetto che ha generato la voce del log.|  
|executionid|**uniqueidentifier**|GUID dell'istanza di esecuzione del file eseguibile che ha generato la voce del log.|  
|starttime|**datetime**|Ora di inizio dell'esecuzione del pacchetto.|  
|endtime|**datetime**|Ora del completamento del pacchetto.<br /><br /> Questa funzionalità non è implementata. Il valore nella colonna endtime è sempre uguale al valore nella colonna starttime.|  
|datacode|**int**|Valore intero facoltativo che in genere indica il risultato dell'esecuzione del contenitore o dell'attività:|  
|databytes|**image**|Matrice di byte facoltativa che contiene informazioni aggiuntive.|  
|message|**nvarchar**|Descrizione dell'evento e delle informazioni associate all'evento.|  
  
## <a name="see-also"></a>Vedere anche  
 [Registrazione di Integration Services &#40;SSIS&#41;](../../integration-services/performance/integration-services-ssis-logging.md)   
  
  
