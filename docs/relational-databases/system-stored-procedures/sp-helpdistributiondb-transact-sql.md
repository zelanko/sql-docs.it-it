---
description: sp_helpdistributiondb (Transact-SQL)
title: sp_helpdistributiondb (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpdistributiondb_TSQL
- sp_helpdistributiondb
helpviewer_keywords:
- sp_helpdistributiondb
ms.assetid: a2917020-26d1-4011-99f8-9212d120fd2d
author: markingmyname
ms.author: maghan
ms.openlocfilehash: c79c1ed5bbbbf53be84432e4d542affece0b16a3
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/08/2020
ms.locfileid: "89543319"
---
# <a name="sp_helpdistributiondb-transact-sql"></a>sp_helpdistributiondb (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  Restituisce le proprietà del database di distribuzione specificato. La stored procedure viene eseguita nel database di distribuzione del server di distribuzione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_helpdistributiondb [ [ @database= ] 'database_name' ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @database = ] 'database_name'` Nome del database per il quale vengono restituite le proprietà. *database_name* è di **tipo sysname**e il valore predefinito è **%** per tutti i database associati al server di distribuzione e per i quali l'utente dispone delle autorizzazioni.  
  
## <a name="result-sets"></a>Set di risultati  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**nome**|**sysname**|Nome del database di distribuzione.|  
|**min_distretention**|**int**|Periodo di memorizzazione minimo espresso in ore che deve trascorrere prima dell'eliminazione delle transazioni.|  
|**max_distretention**|**int**|Periodo di memorizzazione massimo espresso in ore trascorso il quale le transazioni vengono eliminate.|  
|**history retention**|**int**|Numero di ore di memorizzazione della cronologia.|  
|**history_cleanup_agent**|**sysname**|Nome dell'agente di pulizia del contenuto della cronologia.|  
|**distribution_cleanup_agent**|**sysname**|Nome dell'agente di pulizia dei riferimenti alla distribuzione.|  
|**Stato**|**int**|Solo per uso interno.|  
|**data_folder**|**nvarchar(255)**|Nome della directory utilizzata per archiviare i file di database.|  
|**data_file**|**nvarchar(255)**|Nome del file di database.|  
|**data_file_size**|**int**|Dimensioni iniziali del file di dati in MB.|  
|**log_folder**|**nvarchar(255)**|Nome della directory per il file di log del database.|  
|**log_file**|**nvarchar(255)**|Nome del file di log.|  
|**log_file_size**|**int**|Dimensioni iniziali del file di log in MB.|  
  
## <a name="return-code-values"></a>Valori del codice restituito  
 **0** (esito positivo) o **1** (esito negativo)  
  
## <a name="remarks"></a>Osservazioni  
 **sp_helpdistributiondb** viene utilizzato in tutti i tipi di replica.  
  
## <a name="permissions"></a>Autorizzazioni  
 I membri del ruolo predefinito del database **db_owner** o del ruolo **replmonitor** in un database di distribuzione e gli utenti nell'elenco di accesso alla pubblicazione di una pubblicazione che utilizza il database di distribuzione possono eseguire **sp_helpdistributiondb** per restituire informazioni correlate ai file. I membri del ruolo **public** possono eseguire **sp_helpdistributiondb** per restituire informazioni non correlate ai file per i database di distribuzione a cui hanno accesso.  
  
## <a name="see-also"></a>Vedere anche  
 [Visualizzare e modificare le proprietà del server di pubblicazione e del database di distribuzione](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [sp_adddistributiondb &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/sp-adddistributiondb-transact-sql.md)   
 [sp_changedistributiondb &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/sp-changedistributiondb-transact-sql.md)   
 [sp_dropdistributiondb &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/sp-dropdistributiondb-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
