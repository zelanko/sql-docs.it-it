---
title: sp_syscollector_set_warehouse_instance_name (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syscollector_set_warehouse_instance_name_TSQL
- sp_syscollector_set_warehouse_instance_name
dev_langs:
- TSQL
helpviewer_keywords:
- data collector [SQL Server], stored procedures
- sp_syscollector_set_warehouse_instance_name
ms.assetid: 5320fcd4-bed1-468f-b784-a5e10fcfaeb6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 11c704413f9668a5da99ded7d269d05b8e3f2c25
ms.sourcegitcommit: 78e32562f9c1fbf2e50d3be645941d4aa457e31f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/08/2019
ms.locfileid: "54100626"
---
# <a name="spsyscollectorsetwarehouseinstancename-transact-sql"></a>sp_syscollector_set_warehouse_instance_name (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Specifica il nome dell'istanza per la stringa di connessione utilizzata per connettersi al data warehouse di gestione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_syscollector_set_warehouse_instance_name [ @instance_name = ] 'instance_name'  
```  
  
## <a name="arguments"></a>Argomenti  
 [ @instance_name =] '*nome_istanza*'  
 Nome dell'istanza. *instance_name* viene **sysname** e i valori predefiniti per l'istanza locale se NULL.  
  
> **Nota:** _nome_istanza_ deve essere il nome, nome completo dell'istanza che include il nome del computer e il nome dell'istanza nel formato *computerName* \\ *instanceName*.    
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 È necessario disabilitare l'agente di raccolta dati prima di modificarne la configurazione. La procedura non ha esito positivo se l'agente di raccolta dati è abilitato.  
  
 Per visualizzare il nome dell'istanza corrente, eseguire una query di [syscollector_config_store](../../relational-databases/system-catalog-views/syscollector-config-store-transact-sql.md) vista di sistema.  
  
## <a name="permissions"></a>Permissions  
 Per eseguire questa procedura, è richiesta l'appartenenza al ruolo predefinito del database dc_admin (con autorizzazione EXECUTE) .  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene illustrato come configurare l'agente di raccolta dati per utilizzare un'istanza del data warehouse di gestione in un server remoto. In questo esempio il server remoto è denominato `RemoteSERVER` e il database è installato sull'istanza predefinita.  
  
```  
USE msdb;  
GO  
EXEC sp_syscollector_set_warehouse_instance_name N'RemoteSERVER'; -- the default instance is assumed on the remote server  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure dell'agente di raccolta dati &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [syscollector_config_store &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-config-store-transact-sql.md)  
  
  
