---
title: Opzione di configurazione del server Common Criteria Compliance Enabled | Microsoft Docs
ms.custom: ''
ms.date: 08/21/2018
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- common criteria compliance
helpviewer_keywords:
- CC (common criteria) [Database Engine]
- common criteria compliance [Database Engine]
- Risidual Information Protection [Database Engine]
- RIP (Residual Information Protection)
ms.assetid: 61766eea-c450-408d-af33-fbe7ef8c9ff2
author: rothja
ms.author: jroth
ms.openlocfilehash: 47c7e7dc3b557085bb1f5a06e86de747579df007
ms.sourcegitcommit: 4b5919e3ae5e252f8d6422e8e6fddac1319075a1
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/09/2020
ms.locfileid: "83001121"
---
# <a name="common-criteria-compliance-enabled-server-configuration"></a>Opzione di configurazione del server Common Criteria Compliance Enabled
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

L'opzione Common Criteria Compliance Enabled attiva gli elementi seguenti, necessari per [Common Criteria for Information Technology Security Evaluation](https://www.commoncriteriaportal.org/) (Criteri comuni per la valutazione della sicurezza IT).  
  
|Criteri|Descrizione|  
|--------------|-----------------|  
|Protezione delle informazioni residuali (RIP, Residual Information Protection)|RIP richiede la sovrascrittura di una allocazione di memoria con uno schema di bit noto prima che la memoria venga riallocata a una nuova risorsa. La conformità allo standard RIP consente una maggior sicurezza, ma la sovrascrittura dell'allocazione di memoria può rallentare le prestazioni. La sovrascrittura viene eseguita dopo l'attivazione dell'opzione common criteria compliance enabled.|  
|Possibilità di visualizzare le statistiche relative agli accessi|Dopo l'attivazione dell'opzione common criteria compliance enabled, viene attivato il controllo degli accessi. Ogni volta che un utente accede a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vengono rese disponibili le informazioni su data e ora dell'ultimo accesso riuscito, su data e ora dell'ultimo accesso non riuscito e sul numero di tentativi eseguiti tra l'ultimo accesso riuscito e l'accesso corrente. Queste statistiche di accesso possono essere visualizzate eseguendo una query sulla vista a gestione dinamica [sys.dm_exec_sessions](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md) .|  
|La colonna `GRANT` non deve eseguire l'override della tabella `DENY`|Dopo l'attivazione dell'opzione common criteria compliance enabled, un'istruzione `DENY` a livello di tabella ha la precedenza su un'istruzione `GRANT` a livello di colonna. Se l'opzione non è abilitata, un'istruzione `GRANT` a livello di colonna ha la precedenza su un'istruzione `DENY` a livello di tabella.|  
  
 L'opzione Common Criteria Compliance Enabled è un'opzione avanzata. I criteri comuni vengono valutati e certificati solo per l'edizione Enterprise e l'edizione Datacenter. Per lo stato più aggiornato della certificazione con criteri comuni, vedere il sito Web [Criteri comuni per Microsoft SQL Server](https://go.microsoft.com/fwlink/?LinkId=616319) .  
  
> [!IMPORTANT]  
>  Oltre ad attivare l'opzione common criteria compliance enabled, è necessario scaricare ed eseguire uno script che completi la configurazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per la conformità al livello di garanzia di valutazione 4+ (EAL4+) dei criteri comuni. È possibile scaricare questo script dal sito Web relativo ai [criteri comuni per Microsoft SQL Server](https://go.microsoft.com/fwlink/?LinkId=616319) .  
  
 Se si utilizza la stored procedure di sistema `sp_configure` per modificare l'impostazione, è possibile modificare common criteria compliance enabled solo quando il valore di show advanced options è impostato su 1. L'impostazione diventa effettiva dopo il riavvio del server. I possibili valori sono 0 e 1:  
  
-   0 indica che la conformità ai criteri comuni non è abilitata. Questa è la modalità predefinita.  
  
-   1 indica che la conformità ai criteri comuni è abilitata.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene abilitata la conformità ai criteri comuni.  
  
```  
sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE;  
GO  
sp_configure 'common criteria compliance enabled', 1;  
GO  
RECONFIGURE WITH OVERRIDE; 
GO  
```  

Riavviare [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].
  
## <a name="see-also"></a>Vedere anche  
 [Opzioni di configurazione del server &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)
