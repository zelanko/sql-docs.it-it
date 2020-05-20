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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 0e714018ed35a7b6c12c0c00bd8eeffda5630b67
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/05/2020
ms.locfileid: "82833255"
---
# <a name="sp_get_distributor-transact-sql"></a>sp_get_distributor (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Determina se in un server è installato un server di distribuzione. Questa stored procedure viene eseguita in qualsiasi database del computer in cui viene cercato il server di distribuzione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_get_distributor   
```  
  
## <a name="result-sets"></a>Set di risultati  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**installato**|**int**|**0** = No; **1** = Sì|  
|**server di distribuzione**|**sysname**|Nome del server di distribuzione|  
|**database di distribuzione installato**|**int**|**0** = No; **1** = Sì|  
|**is distribution publisher**|**int**|**0** = No; **1** = Sì|  
|**con server di pubblicazione di distribuzione remoto**|**int**|**0** = No; **1** = Sì|  
  
## <a name="remarks"></a>Osservazioni  
 **sp_get_distributor** viene utilizzata principalmente da [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] nella replica snapshot, transazionale e di tipo merge.  
  
## <a name="permissions"></a>Autorizzazioni  
 Qualsiasi utente può eseguire **sp_get_distributor**. Un set di risultati non NULL viene restituito quando questo stored procedure viene eseguito dai membri dei ruoli predefiniti del database **db_owner** o **replmonitor** nel database di distribuzione o dai membri del ruolo predefinito del database **db_owner** in almeno un database pubblicato. Un set di risultati non NULL viene restituito anche quando questo stored procedure viene eseguito dagli utenti nell'elenco di accesso alla pubblicazione di almeno un database pubblicato o nell'elenco di accesso alla pubblicazione del database di distribuzione per un server di pubblicazione non SQL Server, può anche eseguire **sp_get_distributor**.  
  
## <a name="see-also"></a>Vedere anche  
 [Configurare la pubblicazione e la distribuzione](../../relational-databases/replication/configure-publishing-and-distribution.md)   
 [Script di distribuzione e informazioni sul server di pubblicazione](../../relational-databases/replication/administration/distributor-and-publisher-information-script.md)   
 [Stored procedure per la replica &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
