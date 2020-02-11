---
title: sys. Configurations (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.configurations_TSQL
- configurations
- sys.configurations
- configurations_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.configurations catalog view
ms.assetid: c4709ed1-bf88-4458-9e98-8e9b78150441
author: stevestein
ms.author: sstein
ms.openlocfilehash: 9eb9ced4e010001f42e106ce8b1903e029f2f1c4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68109563"
---
# <a name="sysconfigurations-transact-sql"></a>sys.configurations (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene una riga per ciascun valore di un'opzione di configurazione valida per l'intero server impostata nel sistema.  

|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**configuration_id**|**int**|ID univoco del valore di configurazione.|  
|**nome**|**nvarchar (35)**|Nome dell'opzione di configurazione.|  
|**valore**|**sql_variant**|Valore configurato per l'opzione.|  
|**minimo**|**sql_variant**|Valore minimo dell'opzione di configurazione.|  
|**massimo**|**sql_variant**|Valore massimo dell'opzione di configurazione.|  
|**value_in_use**|**sql_variant**|Valore corrente dell'opzione.|  
|**Descrizione**|**nvarchar(255)**|Descrizione dell'opzione di configurazione.|  
|**is_dynamic**|**bit**|1 = La variabile viene applicata quando viene eseguita l'istruzione RECONFIGURE.|  
|**is_advanced**|**bit**|1 = la variabile viene visualizzata solo quando è impostato il **advancedoption di visualizzazione** .|  
  
 Per un elenco di tutte le opzioni di configurazione del server, vedere [Opzioni di configurazione del server &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md).  
  
> [!NOTE]  
>  Per le opzioni di configurazione a livello di database, vedere [ALTER database scoped configuration &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md). Per configurare Soft-NUMA, vedere [&#41;Soft-numa &#40;SQL Server ](../../database-engine/configure-windows/soft-numa-sql-server.md).  
  
## <a name="permissions"></a>Autorizzazioni  
 È richiesta l'appartenenza al ruolo **public** . Per altre informazioni, vedere [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Viste del catalogo di configurazione a livello di server &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/server-wide-configuration-catalog-views-transact-sql.md)   
 [Viste del catalogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
