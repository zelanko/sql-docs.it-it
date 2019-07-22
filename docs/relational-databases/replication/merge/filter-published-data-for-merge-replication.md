---
title: Filtrare i dati pubblicati per la replica di tipo merge | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- merge replication [SQL Server replication], filtering published data
- replication [SQL Server], filtering published data
ms.assetid: 46c5023d-7a3b-4455-becc-e159fcb5d6c4
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 1e0d157b6a4f7f08d068dc8da75c42f4ad924044
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68033265"
---
# <a name="filter-published-data-for-merge-replication"></a>Filtro dei dati pubblicati per la replica di tipo merge
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Oltre ai filtri di riga e di colonna statici che è possibile definire con altri tipi di replica, la replica di tipo merge offre filtri di riga con parametri e filtri join. Per altre informazioni sui filtri di riga e di colonna statici, vedere [Filtrare i dati pubblicati](../../../relational-databases/replication/publish/filter-published-data.md).  
  
 La replica di tipo merge viene utilizzata in molte applicazioni che supportano gli utenti mobili. Tali applicazioni hanno in genere un gran numero di sottoscrizioni ognuna delle quali riceve un set di dati univoco. I filtri con parametri combinati con i filtri join consentono a un amministratore di impostare una pubblicazione (o un numero limitato di pubblicazioni) e di fornire set di dati diversi agli utenti, riducendo l'overhead di gestione introdotto con la creazione di più pubblicazioni.  
  
-   I filtri con parametri consentono l'invio di partizioni diverse di dati a Sottoscrittori diversi senza richiedere la creazione di più pubblicazioni. Ad esempio, è possibile filtrare una tabella in modo che i dati di uno specifico rappresentante vengano replicati solo a tale rappresentante. I filtri con parametri hanno una varietà di opzioni che consentono di personalizzare il filtraggio per ottimizzare le prestazioni e adattarsi ai dati e ai requisiti dell'applicazione. Per altre informazioni sui filtri di riga con parametri, vedere [Filtri di riga con parametri](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).  
  
-   I filtri join sono utilizzati insieme ai filtri con parametri per estendere il filtraggio alle tabelle correlate e possono essere utilizzati anche insieme ai filtri statici. Ad esempio, il rappresentante in genere dispone di dati in altre tabelle, ad esempio le tabelle relative a clienti e ordini. Questi dati possono essere filtrati in modo che il rappresentante riceva solo i dati relativi ai clienti e ai rispettivi ordini. Per altre informazioni, vedere [Join Filters](../../../relational-databases/replication/merge/join-filters.md).  
  
 In un filtro non deve essere inclusa la colonna **rowguidcol** utilizzata dalla replica per identificare le righe. Per impostazione predefinita, si tratta della colonna aggiunta al momento dell'impostazione della replica di tipo merge ed è denominata **rowguid**.  
  
## <a name="see-also"></a>Vedere anche  
 [Pubblicare dati e oggetti di database](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  
