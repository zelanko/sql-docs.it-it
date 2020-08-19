---
description: sp_replshowcmds (Transact-SQL)
title: sp_replshowcmds (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_replshowcmds
- sp_replshowcmds_TSQL
helpviewer_keywords:
- sp_replshowcmds
ms.assetid: 199f5a74-e08e-4d02-a33c-b8ab0db20f44
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: beb5ba1371c3a3e8748e5a4963106d659e7dd31f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88446823"
---
# <a name="sp_replshowcmds-transact-sql"></a>sp_replshowcmds (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  Restituisce i comandi per le transazioni contrassegnate per la replica in formato leggibile. **sp_replshowcmds** può essere eseguita solo quando le connessioni client (inclusa la connessione corrente) non leggono le transazioni replicate dal log. Questa stored procedure viene eseguita nel database di pubblicazione del server di pubblicazione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_replshowcmds [ @maxtrans = ] maxtrans  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @maxtrans = ] maxtrans` Numero di transazioni per cui si desidera ottenere informazioni. *maxtrans* è di **tipo int**e il valore predefinito è **1**, che specifica il numero massimo di transazioni in attesa di replica per le quali **sp_replshowcmds** restituisce informazioni.  
  
## <a name="result-sets"></a>Set di risultati  
 **sp_replshowcmds** è una procedura di diagnostica che restituisce informazioni sul database di pubblicazione da cui viene eseguita.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**xact_seqno**|**binary(10)**|Numero di sequenza del comando.|  
|**originator_id**|**int**|ID dell'origine del comando, sempre **0**.|  
|**publisher_database_id**|**int**|ID del database del server di pubblicazione, sempre **0**.|  
|**article_id**|**int**|ID dell'articolo.|  
|**type**|**int**|Tipo di comando.|  
|**command**|**nvarchar(1024)**|Comando [!INCLUDE[tsql](../../includes/tsql-md.md)].|  
  
## <a name="remarks"></a>Osservazioni  
 **sp_replshowcmds** viene utilizzata nella replica transazionale.  
  
 Utilizzando **sp_replshowcmds**, è possibile visualizzare le transazioni attualmente non distribuite (le transazioni rimanenti nel log delle transazioni che non sono state inviate al server di distribuzione).  
  
 I client che eseguono **sp_replshowcmds** e **sp_replcmds** all'interno dello stesso database ricevono l'errore 18752.  
  
 Per evitare questo errore, il primo client deve disconnettersi o il ruolo del client come lettore di log deve essere rilasciato eseguendo **sp_replflush**. Una volta che tutti i client sono stati disconnessi dalla lettura log, **sp_replshowcmds** possibile eseguire correttamente.  
  
> [!NOTE]  
>  **sp_replshowcmds** deve essere eseguito solo per la risoluzione dei problemi relativi alla replica.  
  
## <a name="permissions"></a>Autorizzazioni  
 Solo i membri del ruolo predefinito del server **sysadmin** o del ruolo predefinito del database **db_owner** possono eseguire **sp_replshowcmds**.  
  
## <a name="see-also"></a>Vedere anche  
 [Messaggi di errore](../../relational-databases/native-client-odbc-error-messages/error-messages.md)   
 [sp_replcmds &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md)   
 [sp_repldone &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/sp-repldone-transact-sql.md)   
 [sp_replflush &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/sp-replflush-transact-sql.md)   
 [sp_repltrans &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/sp-repltrans-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
