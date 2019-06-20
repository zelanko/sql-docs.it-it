---
title: sp_dbmmonitordropalert (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_dbmmonitordropalert_TSQL
- sp_dbmmonitordropalert
dev_langs:
- TSQL
helpviewer_keywords:
- database mirroring [SQL Server], monitoring
- sp_dbmmonitordropalert
ms.assetid: fe4a134b-25bf-464e-a5c4-358de215b65a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d21b966df55cc796fb97c3994e37b87ba62501d2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62715804"
---
# <a name="spdbmmonitordropalert-transact-sql"></a>sp_dbmmonitordropalert (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Elimina l'avviso per una metrica delle prestazioni specificata tramite l'impostazione della soglia su NULL.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_dbmmonitordropalert database_name   
    [ , alert_id ]   
```  
  
## <a name="arguments"></a>Argomenti  
 *database_name*  
 Specifica il database per cui eliminare la soglia degli avvisi specificata.  
  
 *alert_id*  
 Valore intero che identifica l'avviso da eliminare. Se questo argomento viene omesso, vengono eliminati tutti gli avvisi nel database. Per eliminare l'avviso per una determinata misurazione delle prestazioni, specificare uno dei valori seguenti:  
  
|Value|Misurazione delle prestazioni|Valore soglia avvisi|  
|-----------|------------------------|-----------------------|  
|1|Transazione non inviata meno recente|Specifica la quantità di transazioni, espressa in minuti, che può accumularsi nella coda di invio prima che venga generato un avviso nell'istanza del server principale. Questo avviso consente di quantificare il rischio potenziale di perdita dei dati in termini di tempo ed è particolarmente rilevante per la modalità a prestazioni elevate. L'avviso risulta tuttavia utile anche per la modalità a sicurezza elevata quando il mirroring viene sospeso in seguito alla disconnessione dei partner.|  
|2|Log non inviato|Specifica la quantità di log non inviati, espressa in kilobyte (KB), che può accumularsi prima che venga generato un avviso nell'istanza del server principale. Questo avviso consente di quantificare il rischio potenziale di perdita dei dati in termini di KB ed è particolarmente rilevante per la modalità a prestazioni elevate. L'avviso risulta tuttavia utile anche per la modalità a sicurezza elevata quando il mirroring viene sospeso in seguito alla disconnessione dei partner.|  
|3|Log non ripristinato|Specifica la quantità di log non ripristinati, espressa in kilobyte (KB), che può accumularsi prima che venga generato un avviso nell'istanza del server mirror. Questo avviso consente di misurare il tempo di failover. Il*tempo di failover* corrisponde essenzialmente al tempo necessario al server mirror precedente per eseguire il rollforward di tutti i log rimanenti nella propria coda di rollforward, più un breve tempo aggiuntivo.|  
|4|Overhead commit mirror|Specifica il ritardo medio per transazione, espresso in millisecondi, che è consentito prima che venga generato un avviso nell'istanza del server principale. Questo ritardo rappresenta la quantità di overhead generato mentre l'istanza del server principale è in attesa che l'istanza del server mirror scriva il record di log della transazione nella coda di rollforward. Questo valore è rilevante solo nella modalità a sicurezza elevata.|  
|5|Periodo di memorizzazione|Metadati che controllano per quanto tempo vengono conservate le righe della tabella dello stato di mirroring del database.|  
  
> [!NOTE]  
>  Questa procedura consente di eliminare le soglie di avviso, indipendentemente dal fatto che sono stati specificati usando **sp_dbmmonitorchangealert** o monitoraggio mirroring del Database.  
  
 Per informazioni sull'ID evento corrispondenti agli avvisi, vedere [le soglie di avviso di utilizzo e gli avvisi sulle metriche delle prestazioni del mirroring del &#40;SQL Server&#41;](../../database-engine/database-mirroring/use-warning-thresholds-and-alerts-on-mirroring-performance-metrics-sql-server.md).  
  
## <a name="return-code-values"></a>Valori restituiti  
 None  
  
## <a name="result-sets"></a>Set di risultati  
 None  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'appartenenza al ruolo predefinito del server **sysadmin** .  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene eliminata l'impostazione del periodo di memorizzazione del database [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
```  
EXEC sp_dbmmonitordropalert AdventureWorks2012, 5;  
```  
  
 Nell'esempio seguente vengono eliminati tutte le soglie degli avvisi e il periodo di memorizzazione del database [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
```  
EXEC sp_dbmmonitordropalert AdventureWorks2012 ;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Monitoraggio del mirroring del database &#40;SQL Server&#41;](../../database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md)   
 [sp_dbmmonitorchangealert &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorchangealert-transact-sql.md)  
  
  
