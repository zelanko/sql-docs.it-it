---
title: Compatibilità con le versioni precedenti di SQL Server 2017 Analysis Services | Microsoft Docs
ms.date: 01/09/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 411fa78bada76c79d4a869d68c94abf752b8466a
ms.sourcegitcommit: 1c01af5b02fe185fd60718cc289829426dc86eaa
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/10/2019
ms.locfileid: "54185077"
---
# <a name="analysis-services-backward-compatibility-sql-2017"></a>Compatibilità con le versioni precedenti di Analysis Services (SQL 2017)
[!INCLUDE[ssas-appliesto-sql2017](../includes/ssas-appliesto-sql2017.md)]

Questo articolo descrive le modifiche nel comportamento tra la versione corrente e quella precedente e disponibilità delle funzionalità.

## <a name="deprecated-features"></a>Funzionalità deprecate
Oggetto *funzionalità deprecata* verrà sospeso dal prodotto in una versione futura, ma è ancora supportata e inclusa nella versione corrente per garantire la compatibilità con le versioni precedenti. È consigliabile che interrompere l'uso di funzionalità deprecate in progetti nuovi ed esistenti per mantenere la compatibilità con le versioni future. La documentazione non viene aggiornata per le funzionalità deprecate.

Le funzionalità seguenti sono deprecate in questa versione:
  
|||  
|-|-|  
|**Modalità/categoria**|**Funzionalità**|
|Multidimensionale|Data Mining|
|Multidimensionale|Gruppi di misure collegati remoti|
|Tabella|Modelli a livello di compatibilità 1100 e 1103|
|Tabella|Proprietà modello a oggetti tabulare: Column.IsDefaultImage Column.TableDetailPosition, Column.IsDefaultLabel,|
|Strumenti|SQL Server Profiler per l'acquisizione della traccia<br /><br /> La sostituzione prevede l'uso del profiler di eventi estesi incorporato in SQL Server Management Studio.  <br /> Vedere [Monitorare Analysis Services con eventi estesi di SQL Server](../analysis-services/instances/monitor-analysis-services-with-sql-server-extended-events.md).|  
|Strumenti|Server Profiler per la riproduzione della traccia <br />Sostituzione. Non è prevista alcuna sostituzione.|  
|Trace Management Objects e API di traccia|Oggetti Microsoft.AnalysisServices.Trace (contiene le API per gli oggetti Analysis Services Trace e Replay). La sostituzione è multiparte:<br /><br /> -Configurazione della traccia: Microsoft.SqlServer.Management.XEvent<br />-Lettura della traccia: Microsoft.SqlServer.XEvent.Linq<br />-Riproduzione della traccia: None|  


## <a name="discontinued-features"></a>Funzionalità non più supportate
Oggetto *funzionalità non più disponibile* è stata deprecata in una versione precedente. È possibile continuare a essere incluso nella versione corrente, ma non è più supportato. Funzionalità obsolete potrebbe essere rimosso completamente in un futuro rilascio o aggiornare.

Le funzionalità seguenti sono state deprecate in una versione precedente e non sono più supportate in questa versione.
  
|||  
|-|-|  
|**Modalità/categoria**|**Funzionalità**|  
|Tabella|Valore della proprietà VertipaqPagingPolicy memoria (2), abilitare il paging su disco utilizzando memoria file mappati.|
|Multidimensionale|Partizioni remote|  
|Multidimensionale|Gruppi di misure collegati remoti|  
|Multidimensionale|Writeback dimensionale|  
|Multidimensionale|Dimensioni collegate|


## <a name="breaking-changes"></a>Modifiche di rilievo
Oggetto *modifica di rilievo* fa sì che una funzionalità, modello di dati, il codice dell'applicazione o script funzionamento non corretto dopo l'aggiornamento alla versione corrente.

Sono state apportate modifiche importanti in questa versione.

## <a name="behavior-changes"></a>Modifiche del comportamento
Oggetto *modifica del comportamento* influisce sul funzionamento la stessa funzionalità nella versione corrente rispetto alla versione precedente. Vengono descritte solo le modifiche di comportamento significativo. Le modifiche apportate nell'interfaccia utente non sono incluse.

Modifiche a MDSCHEMA_MEASUREGROUP_DIMENSIONS e DISCOVER_CALC_DEPENDENCY, descritti in dettaglio nel [nuove funzionalità di SQL Server 2017 CTP 2.1 per Analysis Services](https://blogs.msdn.microsoft.com/analysisservices/2017/05/18/whats-new-in-sql-server-2017-ctp-2-1-for-analysis-services/) annuncio.


## <a name="see-also"></a>Vedere anche
[Compatibilità con le versioni precedenti di Analysis Services (SQL Server 2016)](analysis-services-backward-compatibility.md)
