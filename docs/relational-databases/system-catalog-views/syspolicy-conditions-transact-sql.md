---
title: syspolicy_conditions (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- syspolicy_conditions
- syspolicy_conditions_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- syspolicy_conditions view
ms.assetid: af97d26c-4bd5-4b08-be51-8419e3b2832c
author: stevestein
ms.author: sstein
ms.openlocfilehash: ee0f269fcfda93733d36a0b7396fd72d16bc01d9
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "68121175"
---
# <a name="syspolicy_conditions-transact-sql"></a>syspolicy_conditions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Consente di visualizzare una riga per ogni condizione della gestione basata su criteri nell' [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]istanza di. syspolicy_conditions appartiene allo schema dbo nel database msdb. Nella tabella seguente vengono descritte le colonne contenute nella vista syspolicy_conditions.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|condition_id|**int**|Identificatore della condizione. Ogni condizione rappresenta una raccolta di uno o più espressioni di condizione.|  
|name|**sysname**|Nome della condizione.|  
|date_created|**datetime**|Data e ora di creazione della condizione.|  
|description|**nvarchar(max)**|Descrizione della condizione. La colonna della descrizione è facoltativa e il valore può essere NULL.|  
|created_by|**sysname**|Account di accesso che ha creato la condizione.|  
|modified_by|**sysname**|Account di accesso che ha modificato la condizione per ultimo. NULL se non sono state apportate modifiche.|  
|date_modified|**datetime**|Data e ora di creazione della condizione. NULL se non sono state apportate modifiche.|  
|is_name_condition|**smallint**|Specifica se la condizione è una condizione di denominazione.<br /><br /> 0 = l'espressione condizionale non contiene la variabile @Name.<br /><br /> 1 = l'espressione condizionale contiene la variabile @Name.|  
|facet|**nvarchar(max)**|Nome del facet su cui si basa la condizione.|  
|Expression|**nvarchar(max)**|Espressione degli stati del facet.|  
|obj_name|**sysname**|Nome dell'oggetto assegnato a @Name se l'espressione condizionale contiene questa variabile.|  
  
## <a name="remarks"></a>Osservazioni  
 Durante la risoluzione dei problemi relativi alla gestione basata su criteri, eseguire una query sulla vista syspolicy_conditions per determinare l'utente che ha creato o modificato per ultimo la condizione.  
  
## <a name="permissions"></a>Autorizzazioni  
 È necessaria l'appartenenza al ruolo PolicyAdministratorRole nel database msdb.  
  
## <a name="see-also"></a>Vedere anche  
 [Amministrare i server tramite la gestione basata su criteri](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)   
 [Viste di Gestione basata su criteri &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/policy-based-management-views-transact-sql.md)  
  
  
