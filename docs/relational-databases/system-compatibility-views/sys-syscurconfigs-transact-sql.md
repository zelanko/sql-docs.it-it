---
description: sys.syscurconfigs (Transact-SQL)
title: sys.syscurconfigs (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.syscurconfigs
- sys.syscurconfigs_TSQL
- syscurconfigs
- syscurconfigs_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.syscurconfigs compatibility view
- syscurconfigs system table
ms.assetid: 454ab849-07a5-4b50-ba0a-6b1b14721f77
author: rothja
ms.author: jroth
ms.openlocfilehash: c5c83219c93c24929b257989a034f283cf2ac5b2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88423325"
---
# <a name="syssyscurconfigs-transact-sql"></a>sys.syscurconfigs (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Contiene una voce per ogni opzione di configurazione corrente. Questa vista contiene inoltre quattro voci che descrivono la struttura di configurazione. **syscurconfigs** viene compilato dinamicamente quando viene eseguita una query da un utente. Per ulteriori informazioni, vedere [sys.sysconfigura &#40;&#41;Transact-SQL ](../../relational-databases/system-compatibility-views/sys-sysconfigures-transact-sql.md).  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**value**|**int**|Valore modificabile dall'utente per la variabile. Questo valore viene utilizzato da [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] solo dopo l'esecuzione di RECONFIGURE.|  
|**config**|**smallint**|Numero di variabile di configurazione.|  
|**Commento**|**nvarchar(255)**|Descrizione dell'opzione di configurazione.|  
|**Stato**|**smallint**|Mappa di bit che indica lo stato dell'opzione. I possibili valori sono i seguenti:<br /><br /> 0 = statica. L'impostazione diventa effettiva al riavvio del server.<br /><br /> 1 = dinamica. La variabile diventa attiva quando viene eseguita l'istruzione RECONFIGURE.<br /><br /> 2 = avanzata. La variabile viene visualizzata solo quando è impostata l' **opzione Mostra opzioni avanzate** .<br /><br /> 3 = dinamica e avanzata.|  
  
## <a name="see-also"></a>Vedere anche  
 [Mapping di tabelle di sistema a viste di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Viste della compatibilità &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
