---
title: sys. sysconfigures (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.sysconfigures
- sysconfigures
- sys.sysconfigures_TSQL
- sysconfigures_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sysconfigures compatibility view
- sysconfigures system table
ms.assetid: 146bf10a-c898-4676-a2a1-673fb1cee7a2
author: rothja
ms.author: jroth
ms.openlocfilehash: c785ee1c4d3c5382aa42adf48ad9880f00297137
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68089198"
---
# <a name="syssysconfigures-transact-sql"></a>sys.sysconfigures (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene una riga per ogni opzione di configurazione impostata da un utente. **sysconfigures** contiene le opzioni di configurazione definite prima dell'avvio più recente di, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]oltre a tutte le opzioni di configurazione dinamiche impostate da quel momento.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**valore**|**int**|Valore modificabile dall'utente per la variabile. Questo valore viene utilizzato da [!INCLUDE[ssDE](../../includes/ssde-md.md)] solo dopo l'esecuzione di RECONFIGURE.|  
|**config**|**int**|Numero di variabile di configurazione.|  
|**Commento**|**nvarchar(255)**|Descrizione dell'opzione di configurazione.|  
|**stato**|**smallint**|Mappa di bit che indica lo stato dell'opzione. I possibili valori sono i seguenti:<br /><br /> 0 = statica. L'impostazione diventa effettiva al riavvio del server.<br /><br /> 1 = dinamica. La variabile diventa attiva quando viene eseguita l'istruzione RECONFIGURE.<br /><br /> 2 = avanzata. La variabile viene visualizzata solo quando è impostata l' **opzione Mostra opzioni avanzate** . L'impostazione diventa effettiva al riavvio del server.<br /><br /> 3 = dinamica e avanzata.|  
  
## <a name="see-also"></a>Vedere anche  
 [Mapping di tabelle di sistema a viste di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Viste di compatibilità &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
