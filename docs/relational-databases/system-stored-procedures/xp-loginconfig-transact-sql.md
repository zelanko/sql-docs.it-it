---
title: xp_loginconfig (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- xp_loginconfig_TSQL
- xp_loginconfig
dev_langs:
- TSQL
helpviewer_keywords:
- xp_loginconfig
ms.assetid: d380e799-2857-408a-bcbf-5e73a8e6aa5a
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 7abf136187b4f45a03cebc92fd23ee544dddb117
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68116692"
---
# <a name="xploginconfig-transact-sql"></a>xp_loginconfig (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce la configurazione di sicurezza dell'account di accesso di un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
xp_loginconfig ['config_name']  
```  
  
## <a name="arguments"></a>Argomenti  
 **«** *config_name* **»**  
 Valore di configurazione da visualizzare. Se *config_name* viene omesso, vengono segnalati tutti i valori di configurazione. *config_name* viene **sysname**, con un valore predefinito è NULL, i possibili valori sono i seguenti.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**modalità di accesso**|Modalità di sicurezza dell'account di accesso. I valori possibili sono **Mixed** e **l'autenticazione di Windows**.<br /><br /> Sostituito da:<br /><br /> `SELECT SERVERPROPERTY('IsIntegratedSecurityOnly'); GO`|  
|**account di accesso predefinito**|Nome dell'ID di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] predefinito per gli utenti autorizzati su connessioni trusted (ovvero gli utenti che non dispongono di un nome di account di accesso corrispondente). Account di accesso predefinito è **guest**. Questo valore è disponibile per compatibilità con le versioni precedenti.|  
|**Dominio predefinito**|Nome del dominio di Windows predefinito per gli utenti di rete su connessioni trusted. Il dominio predefinito è il dominio del computer in cui sono in esecuzione Windows e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Questo valore è disponibile per compatibilità con le versioni precedenti.|  
|**livello di controllo**|Livello di controllo. I valori possibili sono **none**, **successo**, **errore**, e **tutti**. I controlli vengono scritti nel log degli errori e nel Visualizzatore eventi di Windows.|  
|**Nome set di host**|Indica se il nome dell'host proveniente dal record dell'account di accesso del client viene sostituito con il nome utente di rete di Windows. I valori possibili sono **true** oppure **false**. Se è impostato, il nome utente di rete viene visualizzato nell'output dal **sp_who**.|  
|**eseguire il mapping di _**|Restituisce i caratteri speciali di Windows sui quali viene eseguito il mapping al carattere di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] valido _ (sottolineatura). I valori possibili sono **separatore dominio** (impostazione predefinita), **spazio**, **null**, qualsiasi carattere singolo. Questo valore è disponibile per compatibilità con le versioni precedenti.|  
|**eseguire il mapping di $**|Restituisce i caratteri speciali di Windows sui quali viene eseguito il mapping al carattere di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] valido $ (segno di dollaro). I valori possibili sono **separatore dominio**, **spazio**, **null**, qualsiasi carattere singolo. Il valore predefinito è **spazio**. Questo valore è disponibile per compatibilità con le versioni precedenti.|  
|**eseguire il mapping di &**|Restituisce i caratteri speciali di Windows sui quali viene eseguito il mapping al carattere di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] valido # (simbolo di cancelletto). I valori possibili sono **separatore dominio**, **spazio**, **null**, qualsiasi carattere singolo. Il valore predefinito è il segno meno. Questo valore è disponibile per compatibilità con le versioni precedenti.|  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o 1 (esito negativo)  
  
## <a name="result-sets"></a>Set di risultati  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Valore di configurazione|  
|**valore di configurazione**|**sysname**|Impostazione del valore di configurazione|  
  
## <a name="remarks"></a>Note  
 **xp_loginconfig** non può essere utilizzato per impostare i valori di configurazione.  
  
 Per impostare la modalità di accesso e il livello di controllo, utilizzare [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
## <a name="permissions"></a>Permissions  
 Richiede l'autorizzazione CONTROL sul **master** database.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-how-to-report-all-configuration-values"></a>R. Visualizzazione di tutti i valori di configurazione  
 Nell'esempio seguente vengono visualizzate tutte le impostazioni correnti.  
  
```  
EXEC xp_loginconfig;  
GO  
```  
  
### <a name="b-how-to-report-a-specific-configuration-value"></a>B. Modalità di segnalazione di un valore di configurazione specifico  
 Nell'esempio seguente viene visualizzata l'impostazione relativa alla modalità di accesso.  
  
```  
EXEC xp_loginconfig 'login mode';  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [sp_denylogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-denylogin-transact-sql.md)   
 [sp_grantlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sp_revokelogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revokelogin-transact-sql.md)   
 [xp_logininfo &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/xp-logininfo-transact-sql.md)  
  
  
