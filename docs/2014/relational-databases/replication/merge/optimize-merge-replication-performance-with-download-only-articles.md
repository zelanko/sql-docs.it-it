---
title: Ottimizzare le prestazioni della replica di tipo merge con gli articoli di solo download | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- merge replication [SQL Server replication], download-only articles
- articles [SQL Server replication], download-only
- download-only articles
ms.assetid: 8851faa6-e6df-4ea5-a6ea-2a3471680fa3
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5ca661105c28cab2bf3e881cf262922e95da5eed
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63250372"
---
# <a name="optimize-merge-replication-performance-with-download-only-articles"></a>Ottimizzazione delle prestazioni della replica di tipo merge con gli articoli di solo download
  La replica di tipo merge offre due tipi di articoli differenti per soddisfare le diverse esigenze applicative. Le pubblicazioni possono contenere uno o più di questi tipi di articoli in base al tipo di applicazione:  
  
-   Articoli standard  
  
-   articoli di solo download  
  
 Gli articoli di solo download sono vantaggiosi in termini di prestazioni rispetto agli articoli standard e se ne consiglia l'utilizzo laddove possibile.  
  
> [!NOTE]  
>  Per utilizzare questo tipo di articoli è necessario che il livello di compatibilità della pubblicazione sia impostato almeno su 90RTM.  
  
## <a name="standard-articles"></a>Articoli standard  
 Gli articoli standard sono quelli predefiniti e offrono l'intera gamma di funzionalità della replica di tipo merge, tra cui il rilevamento e la risoluzione dei conflitti. Sono inoltre adatti per le tabelle che vengono aggiornate da più Sottoscrittori. Oggetti diversi dalle tabelle, come stored procedure e viste, vengono sempre pubblicati come articoli standard.  
  
## <a name="download-only-articles"></a>articoli di solo download  
 Gli articoli di solo download sono progettati per le applicazioni contenenti dati che non vengono aggiornati nei Sottoscrittori, ad esempio un set di articoli contenuti in un catalogo prodotti. Un catalogo prodotti viene generalmente aggiornato nel server di pubblicazione, ma non nei Sottoscrittori. Poiché non è possibile aggiornare gli articoli di solo download nel Sottoscrittore, i metadati di rilevamento non vengono inviati ai Sottoscrittori. Ciò può comportare uno spazio di archiviazione ridotto sui Sottoscrittori e un vantaggio in termini di prestazioni, soprattutto se la connessione di rete è lenta.  
  
 Gli articoli di solo download operano insieme ai sottoscrittori client, ovvero se un articolo è progettato come di solo download, non è possibile inserire, aggiornare o eliminare righe per tale articolo nei Sottoscrittori che utilizzano sottoscrizioni client. I server di pubblicazione e i Sottoscrittori che utilizzano il tipo di sottoscrizione server (generalmente Sottoscrittori che ripubblicano dati in altri Sottoscrittori) possono inserire, aggiornare ed eliminare dati. Per altre informazioni sulle sottoscrizioni client, vedere [Sottoscrivere le pubblicazioni](../subscribe-to-publications.md).  
  
 Per specificare che un articolo è di solo download, vedere [Impostazione del tipo solo download per un articolo di tabella di merge](../publish/specify-merge-replication-properties.md#download-only).  
  
## <a name="using-different-article-types-in-your-applications"></a>Utilizzo di tipi di articolo differenti nelle applicazioni  
 Se si analizzano i requisiti dell'applicazione in uso, è possibile valutare la soluzione migliore tra massima flessibilità e prestazioni ottimali. Le applicazioni caratterizzate da numerosi conflitti e modifiche sia nel server di pubblicazione che nei Sottoscrittori utilizzeranno, ad esempio, una pubblicazione costituita da articoli standard. Alcune applicazioni, come quelle di automazione della forza vendita (SFA), possono contenere articoli potenzialmente soggetti a conflitti e altri articoli che fungono da tabelle di ricerca e che possono essere specificati come di solo download. Le applicazioni di immissione dati, ad esempio i sistemi POS (Point Of Sales) e le applicazioni di automazione del personale esterno (FFA), spesso partizionano i dati in modo da eliminare i conflitti e non consentirne il passaggio da un Sottoscrittore all'altro. In queste situazioni una combinazione di partizioni non sovrapposte, di articoli di solo download e di partizioni pre-calcolate garantisce prestazioni e scalabilità massime. Per ulteriori informazioni sulle partizioni non sovrapposte e pre-calcolate, vedere [Filtri di riga parametrizzati](parameterized-filters-parameterized-row-filters.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Opzioni degli articoli per la replica di tipo merge](article-options-for-merge-replication.md)   
 [Ottimizzare le prestazioni della replica di tipo merge con il rilevamento condizionale delle eliminazioni](optimize-merge-replication-performance-with-conditional-delete-tracking.md)  
  
  
