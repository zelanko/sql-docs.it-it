---
title: Filtrare i dati pubblicati per la replica di tipo merge | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- merge replication [SQL Server replication], filtering published data
- replication [SQL Server], filtering published data
ms.assetid: 46c5023d-7a3b-4455-becc-e159fcb5d6c4
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 463a9385f4622f85cd1cbd5666517464be3cffd4
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52780843"
---
# <a name="filter-published-data-for-merge-replication"></a>Filtro dei dati pubblicati per la replica di tipo merge
  Oltre ai filtri di riga e di colonna statici che è possibile definire con altri tipi di replica, la replica di tipo merge offre filtri di riga con parametri e filtri join. Per altre informazioni sui filtri di riga e di colonna statici, vedere [Filtrare i dati pubblicati](../publish/filter-published-data.md).  
  
 La replica di tipo merge viene utilizzata in molte applicazioni che supportano gli utenti mobili. Tali applicazioni hanno in genere un gran numero di sottoscrizioni ognuna delle quali riceve un set di dati univoco. I filtri con parametri combinati con i filtri join consentono a un amministratore di impostare una pubblicazione (o un numero limitato di pubblicazioni) e di fornire set di dati diversi agli utenti, riducendo l'overhead di gestione introdotto con la creazione di più pubblicazioni.  
  
-   I filtri con parametri consentono l'invio di partizioni diverse di dati a Sottoscrittori diversi senza richiedere la creazione di più pubblicazioni. Ad esempio, è possibile filtrare una tabella in modo che i dati di uno specifico rappresentante vengano replicati solo a tale rappresentante. I filtri con parametri hanno una varietà di opzioni che consentono di personalizzare il filtraggio per ottimizzare le prestazioni e adattarsi ai dati e ai requisiti dell'applicazione. Per altre informazioni sui filtri di riga con parametri, vedere [Filtri di riga con parametri](parameterized-filters-parameterized-row-filters.md).  
  
-   I filtri join sono utilizzati insieme ai filtri con parametri per estendere il filtraggio alle tabelle correlate e possono essere utilizzati anche insieme ai filtri statici. Ad esempio, il rappresentante in genere dispone di dati in altre tabelle, ad esempio le tabelle relative a clienti e ordini. Questi dati possono essere filtrati in modo che il rappresentante riceva solo i dati relativi ai clienti e ai rispettivi ordini. Per altre informazioni, vedere [Join Filters](join-filters.md).  
  
 In un filtro non deve essere inclusa la colonna `rowguidcol` utilizzata dalla replica per identificare le righe. Per impostazione predefinita, si tratta della colonna aggiunta al momento dell'impostazione della replica di tipo merge ed è denominata **rowguid**.  
  
## <a name="see-also"></a>Vedere anche  
 [Pubblicare dati e oggetti di database](../publish/publish-data-and-database-objects.md)  
  
  
