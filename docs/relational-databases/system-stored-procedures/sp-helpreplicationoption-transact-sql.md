---
title: sp_helpreplicationoption (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpreplicationoption
- sp_helpreplicationoption_TSQL
helpviewer_keywords:
- sp_helpreplicationoption
ms.assetid: ef988dbc-dd0b-4132-80ab-81eebec1cffe
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 14357c7700980a1e3cc241d2e6b300e830aa4319
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52818893"
---
# <a name="sphelpreplicationoption-transact-sql"></a>sp_helpreplicationoption (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Visualizza i tipi di opzioni di replica attivate per un server. Questa stored procedure viene eseguita in qualsiasi database di qualsiasi server.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_helpreplicationoption [ [ @optname =] 'option_name' ]  
```  
  
## <a name="arguments"></a>Argomenti  
 [  **@optname =**] **'***option_name***'**  
 Nome dell'opzione di replica per cui si desidera eseguire una query. *option_name* viene **sysname**, con un valore predefinito è NULL.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**Transazionale**|Viene restituito un set di risultati quando è attivata la replica transazionale.|  
|**merge**|Viene restituito un set di risultati quando è attivata la replica di tipo merge.|  
|NULL (predefinito)|Non viene restituito un set di risultati.|  
  
## <a name="result-sets"></a>Set di risultati  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**optname**|**sysname**|Nome dell'opzione di replica. I possibili valori sono i seguenti:<br /><br /> **Transazionale**<br /><br /> **merge**|  
|**Valore**|**bit**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**versione_principale**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**versione_secondaria**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**revisione**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**install_failures**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 **sp_helpreplicationoption** viene usato per ottenere informazioni sulle opzioni di replica abilitato in un server specifico. Per ottenere informazioni su un database specifico, usare **sp_helpreplicationdboption**.  
  
## <a name="permissions"></a>Permissions  
 Le autorizzazioni di esecuzione vengono assegnate per impostazione predefinita al ruolo **public** .  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
