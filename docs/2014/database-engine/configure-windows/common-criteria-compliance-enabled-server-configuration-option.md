---
title: Opzione di configurazione del server common criteria compliance enabled | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 8fef699da6e63c534d19e0d66bfa076f85348d29
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62786640"
---
# <a name="common-criteria-compliance-enabled-server-configuration-option"></a>Opzione di configurazione del server common criteria compliance enabled
  L'opzione Attiva conformità criteri comuni attiva gli elementi seguenti, necessari per i criteri comuni.  
  
|Criteri|Descrizione|  
|--------------|-----------------|  
|Protezione delle informazioni residuali (RIP, Residual Information Protection)|RIP richiede la sovrascrittura di una allocazione di memoria con uno schema di bit noto prima che la memoria venga riallocata a una nuova risorsa. La conformità allo standard RIP consente una maggior sicurezza, ma la sovrascrittura dell'allocazione di memoria può rallentare le prestazioni. La sovrascrittura viene eseguita dopo l'attivazione dell'opzione common criteria compliance enabled.|  
|Possibilità di visualizzare le statistiche relative agli accessi|Dopo l'attivazione dell'opzione common criteria compliance enabled, viene attivato il controllo degli accessi. Ogni volta che un utente accede a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vengono rese disponibili le informazioni su data e ora dell'ultimo accesso riuscito, su data e ora dell'ultimo accesso non riuscito e sul numero di tentativi eseguiti tra l'ultimo accesso riuscito e l'accesso corrente. Queste statistiche di accesso possono essere visualizzate eseguendo una query sulla vista a gestione dinamica [sys.dm_exec_sessions](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql) .|  
|La colonna GRANT non deve eseguire l'override della tabella DENY|Dopo l'attivazione dell'opzione common criteria compliance enabled, un'istruzione DENY a livello di tabella ha la precedenza su un'istruzione GRANT a livello di colonna. Se l'opzione non è abilitata, un'istruzione GRANT a livello di colonna ha la precedenza su un'istruzione DENY a livello di tabella.|  
  
 L'opzione Common Criteria Compliance Enabled è un'opzione avanzata. I criteri comuni vengono valutati e certificati solo per l'edizione Enterprise e l'edizione Datacenter. Per lo stato più aggiornato della certificazione con criteri comuni, vedere il sito Web [Criteri comuni per Microsoft SQL Server](https://go.microsoft.com/fwlink/?LinkId=616319) .  
  
> [!IMPORTANT]  
>  Oltre ad attivare l'opzione common criteria compliance enabled, è necessario scaricare ed eseguire uno script che completi la configurazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per la conformità al livello di garanzia di valutazione 4+ (EAL4+) dei criteri comuni. È possibile scaricare questo script dal sito Web relativo ai [criteri comuni per Microsoft SQL Server](https://go.microsoft.com/fwlink/?LinkId=616319) .  
  
 Se si utilizza la stored procedure di sistema sp_configure per modificare l'impostazione, è possibile modificare common criteria compliance enabled solo quando il valore di show advanced options è impostato su 1. L'impostazione diventa effettiva dopo il riavvio del server. I possibili valori sono 0 e 1:  
  
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
RECONFIGURE  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Opzioni di configurazione del server &#40;SQL Server&#41;](server-configuration-options-sql-server.md)  
  
  
