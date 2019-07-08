---
title: Vincoli di arco del grafo | Microsoft Docs
ms.custom: ''
ms.date: 06/21/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- edge constraints [SQL Server]
- CONNECTION constraints
- edge constraints [Azure SQL Database]
- graph edge constraints
- SQL Graph
author: shkale-msft
ms.author: shkale
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current||=azuresqldb-current'
ms.openlocfilehash: aa73858e6df29c814821ee9e24923cbfc0fbd4a2
ms.sourcegitcommit: 630f7cacdc16368735ec1d955b76d6d030091097
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/24/2019
ms.locfileid: "67343889"
---
# <a name="edge-constraints"></a>Vincoli di arco

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md.md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

I vincoli di arco possono essere usati per imporre l'integrità dei dati e semantica specifica per le tabelle archi nel database a grafo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

##  <a name="Connection"></a> Vincoli di arco
 Nella prima versione delle funzionalità relative ai grafi, le tabelle archi non imponevano alcun vincolo per le estremità dell'arco. Questo significa che un arco in un database a grafo poteva connettere qualsiasi nodo a qualsiasi altro nodo, indipendentemente dal tipo. 

 In questa versione sono stati introdotti i vincoli di arco, che consentono agli utenti di aggiungere vincoli alle tabelle archi, per imporre una semantica specifica e mantenere l'integrità dei dati. Quando si aggiunge un nuovo arco a una tabella archi con vincoli di arco, il [!INCLUDE[ssDE](../../includes/ssde-md.md)] impone che i nodi a cui tenta di connettersi l'arco esistano nelle tabelle nodi appropriate. Questi vincoli possono anche assicurare che un nodo non possa essere eliminato se un arco vi fa ancora riferimento. 

 ### <a name="edge-constraint-clauses"></a>Clausole dei vincoli di arco
 Ogni vincolo di arco è costituito da una o più clausole. Una clausola del vincolo di arco corrisponde alla coppia di nodi DA e A che l'arco specificato potrebbe connettere. 

 Si supponga che il grafico contenga i nodi `Product` e `Customer` e di usare l'arco `Bought` per la connessione di questi nodi. La clausola del vincolo di arco specifica la coppia di nodi DA e A e la direzione dell'arco. In questo caso la clausola del vincolo di arco sarà DA `Customer` A `Product`. Ovvero sarà consentito l'inserimento di un arco `Bought` che va da `Customer` a `Product`. I tentativi di inserire un arco che va da `Product` a `Customer` avranno esito negativo. 
  
- Una clausola del vincolo di arco contiene una coppia di tabelle nodi DA e A a cui viene applicato il vincolo di arco. 
  
- Gli utenti possono specificare più clausole per ogni vincolo di arco, che verranno applicate in forma disgiunta.

- Se vengono creati più vincoli di arco vengono per una singola tabella archi, gli archi devono soddisfare TUTTI i vincoli per essere consentiti.
  
### <a name="indexes-on-edge-constraints"></a>Indici sui vincoli di arco
 La creazione di un vincolo di arco non determina automaticamente la creazione di un indice corrispondente sulle colonne `$from_id` e `$to_id` nella tabella archi. La creazione manuale di un indice per una coppia `$from_id`, `$to_id` è consigliata in presenza di query di ricerca di punti o carichi di lavoro OLTP. 

##  <a name="Tasks"></a> Attività correlate  
 Nella tabella seguente vengono elencate le attività comuni associate ai vincoli di arco.  
  
|Attività|Articolo|  
|----------|-----------|  
|Viene descritto come creare vincoli di arco.|[Creare vincoli di arco](../../relational-databases/tables/create-edge-constraints.md)|  
|Viene descritto come eliminare un vincolo di arco.|[Eliminare vincoli di arco](../../relational-databases/tables/delete-edge-constraint.md)|  
|Viene descritto come modificare un vincolo di arco.|[Modificare vincoli di arco](../../relational-databases/tables/modify-edge-constraint.md)|  
|Viene descritto come visualizzare le proprietà dei vincoli di arco.|[Visualizzare le proprietà di un vincolo di arco](../../relational-databases/tables/view-edge-constraint-properties.md)|  
| Panoramica della tecnologia Graph in SQL Server | [Elaborazione di grafi con SQL Server e il database SQL di Azure](../graphs/sql-graph-overview.md) |
| &nbsp; | &nbsp; |
