---
title: sys.sp_rda_set_query_mode (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: language-reference
f1_keywords:
- sys.sp_rda_set_query_mode
- sys.sp_rda_set_query_mode_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_rda_set_query_mode stored procedure
ms.assetid: 65a0b390-cf87-4db7-972a-1fdf13456c88
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: aa168f3bbac37e34730d5ee0ab348f5fd7d1743d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65982888"
---
# <a name="syssprdasetquerymode-transact-sql"></a>sys.sp_rda_set_query_mode (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Specifica se le query su database abilitati per l'estensione corrente e le relative tabelle restituiscono dati locali e remoti (predefinito) o solo i dati locali.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_rda_set_query_mode [ @mode = ] @mode   
    [ , [ @force = ]  @force ]  
```  
  
## <a name="arguments"></a>Argomenti  
 [ @mode = ] *@mode*  
 È uno dei valori seguenti.  
  
-   **DISABILITATO** esito negativo di tutte le query sulle tabelle abilitate per l'estensione.  
  
-   **LOCAL_ONLY** query sulle tabelle abilitate per l'estensione restituiscono solo i dati locali.  
  
-   **LOCAL_AND_REMOTE** query sulle tabelle abilitate per l'estensione restituiscono dati locali e remoti. Questo è il comportamento predefinito.  
  
 [ @force = ]  *@force*  
 È un valore di bit facoltativo che è possibile impostare su 1 se si desidera modificare la modalità query senza convalida.  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o > 0 (esito negativo)  
  
## <a name="permissions"></a>Permissions  
 Richiede autorizzazioni db_owner.  
  
## <a name="remarks"></a>Note  
 Le seguenti stored procedure estese anche impostano la modalità query per un database abilitato per Stretch.  
  
-   **sp_rda_deauthorize_db**  
  
     Dopo aver eseguito **sp_rda_deauthorize_db** , tutte le query su tabelle e database abilitati per Stretch esito negativo. Vale a dire, la modalità di query è impostata su DISABILITATO. Per uscire da questa modalità, eseguire una delle operazioni seguenti.  
  
    -   Eseguire [Sys. sp_rda_reauthorize_db &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md) riconnettersi al database di Azure remoto. Questa operazione automaticamente Reimposta la modalità query LOCAL_AND_REMOTE, ovvero il comportamento predefinito per Stretch Database. Vale a dire, le query restituiscono risultati dai dati locali e remoti.  
  
    -   Eseguire [sp_rda_set_query_mode](../../relational-databases/system-stored-procedures/sys-sp-rda-set-query-mode-transact-sql.md) con l'argomento LOCAL_ONLY per consentire le query di continuare a eseguire solo i dati locali.  
  
-   **sp_rda_reauthorize_db**  
  
     Quando si esegue [Sys. sp_rda_reauthorize_db &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md) per la riconnessione al database di Azure remoto, questa operazione automaticamente Reimposta la modalità query LOCAL_AND_REMOTE, ovvero il comportamento predefinito per Stretch Database. Vale a dire, le query restituiscono risultati dai dati locali e remoti.  
  
## <a name="see-also"></a>Vedere anche  
 [sys.sp_rda_deauthorize_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-deauthorize-db-transact-sql.md)   
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  
