---
title: Usare il widget Insight per monitorare i server e database
titleSuffix: Azure Data Studio
description: Informazioni su widget insight in Azure Data Studio
ms.custom: seodec18
ms.date: 09/24/2018
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: conceptual
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7fa7317d048d2bb9e19b6e82f5323a3b8ed15751
ms.sourcegitcommit: 189a28785075cd7018c98e9625c69225a7ae0777
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/07/2018
ms.locfileid: "53030195"
---
# <a name="manage-servers-and-databases-with-insight-widgets-in-includename-sosincludesname-sos-shortmd"></a>Gestire server e database con i widget di Insight in [!INCLUDE[name-sos](../includes/name-sos-short.md)]

I widget di Insight trasformano le query Transact-SQL (T-SQL) utilizzate per monitorare i server e i database in visualizzazioni dettagliate. 

Gli insight sono grafici personalizzabili da aggiungere ai dashboard di monitoraggio di server e database. Con essi è possibile visualizzare informazioni generali sui server e sui database, esaminare ulteriori dettagli ed eseguire azioni di gestione definite dall'utente. 

È possibile costruire accattivanti dashboard di gestione server e database simili all'esempio seguente:

![dashboard del database](media/insight-widgets/database-dashboard.png)


Per iniziare a comprendere e creare i tipi diversi di widget Insight, vedere le esercitazioni seguenti:


- [Costruire un widget Insight personalizzato](tutorial-build-custom-insight-sql-server.md)
- *Abilitare widget insight predefiniti*
   - [Abilitare l'insight di monitoraggio delle prestazioni](tutorial-qds-sql-server.md)
   - [Abilitare l'insight di spazio utilizzato dalle tabelle](tutorial-table-space-sql-server.md)


## <a name="sql-queries"></a>Query SQL 

[!INCLUDE[name-sos](../includes/name-sos-short.md)] cerca di evitare l'introduzione di un nuovo linguaggio e di un'interfaccia complessa, lasciando spazio alla scrittura T-SQL e a configurazioni minimali basate su JSON. La configurazione dei widget Insight tramite T-SQL sfrutta le innumerevoli utili query T-SQL che possono essere convertite in widget dettagliati.

I wdget Insight sono costituiti da una o due query T-SQL:
* La *query del widget Insight* è obbligatoria ed è la query che restituisce i dati visualizzati all'interno del widget.
* La *query del dettaglio del widget Insight* è richiesta solo se si sta creando una pagina di dettaglio

Una query di widget insight definisce un set di dati che viene presentata sotto forma di un numero o di un grafico. Una query di dettaglio del widget insight viene utilizzata per elencare le informazioni dettagliate rilevanti in un formato tabulare nel riquadro dei dettagli del widget. 

[!INCLUDE[name-sos](../includes/name-sos-short.md)] esegue la query del widget insight ed effettua il mapping dei risultati al set dei dati del grafico, quindi ne esegue il rendering. Quando gli utenti richiedono i dettagli, esegue la query del dettaglio del widget e presenta il risultato in una visualizzazione a griglia nella finestra di dialogo.

L'idea di base consiste pertanto nello scrivere una query T-SQL da utilizzare come set di dati di un conteggio o di un grafico. 

## <a name="summary"></a>Riepilogo

La query T-SQL e il relativo set di risultati determinano il comportamento del widget di Insight. Scrivere una query per un particolare tipo di grafico o determinare il miglior tipo di grafico da mappare a una query esistente è la chiave per costruire un widget di Insight efficace.



## <a name="additional-resources"></a>Risorse aggiuntive
- [Editor query](tutorial-sql-editor.md)

