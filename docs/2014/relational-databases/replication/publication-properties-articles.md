---
title: Proprietà pubblicazione, Articoli | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.newpubwizard.pubproperties.articles.f1
ms.assetid: bdeea318-a153-44b8-9e51-9155f3bad18b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f46fbc99145f9a372a2c1bf5d40919b87c782454
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "63021671"
---
# <a name="publication-properties-articles"></a>Proprietà pubblicazione, Articoli
  La pagina **Articoli** della finestra di dialogo **Proprietà pubblicazione** contiene informazioni sugli articoli contenuti in una pubblicazione e consente di aggiungere o rimuovere articoli da pubblicazioni esistenti, nonché di modificare i filtri delle colonne e le proprietà degli articoli.  
  
> [!NOTE]  
>  Dopo la creazione di una pubblicazione, per alcune modifiche delle proprietà è necessario un nuovo snapshot. Se la pubblicazione dispone di sottoscrizioni, per alcune modifiche è inoltre necessario reinizializzare tutte le sottoscrizioni. Per altre informazioni, vedere [Modificare le proprietà di pubblicazioni e articoli](publish/change-publication-and-article-properties.md) e [Aggiungere ed eliminare articoli in pubblicazioni esistenti](publish/add-articles-to-and-drop-articles-from-existing-publications.md).  
  
 Se si pubblica un oggetto di database che dipende da uno o più oggetti di database diversi, è necessario pubblicare tutti gli oggetti a cui si fa riferimento. Se ad esempio si pubblica una vista che dipende da una tabella, sarà necessario pubblicare anche la tabella.  
  
 Accanto agli oggetti che non possono essere pubblicati viene visualizzata un'icona rossa con una spiegazione nel pannello informativo nella parte inferiore della pagina della procedura guidata. Non è possibile pubblicare gli oggetti seguenti:  
  
-   Oggetti crittografati.  
  
-   Viste indicizzate contenenti colonne che consentono l'uso di valori NULL.  
  
-   Le tabelle prive di chiavi primarie non possono essere pubblicate nelle pubblicazioni transazionali.  
  
-   Le tabelle non possono essere pubblicate in una pubblicazione di tipo merge né in una pubblicazione transazionale abilitata per le sottoscrizioni ad aggiornamento in coda. Per altre informazioni sulla pubblicazione di un articolo in più pubblicazioni, vedere la sezione "Pubblicazione di tabelle in più pubblicazioni" in [Pubblicare dati e oggetti di database](publish/publish-data-and-database-objects.md).  
  
## <a name="oracle-publishers"></a>Server di pubblicazione Oracle  
 Per i server di pubblicazione Oracle, sono disponibili indicazioni aggiuntive:  
  
-   Per un elenco di oggetti che possono essere pubblicati da Oracle, vedere [Design Considerations and Limitations for Oracle Publishers](non-sql/design-considerations-and-limitations-for-oracle-publishers.md). Gli oggetti che non possono essere pubblicati non vengono visualizzati.  
  
-   Per un elenco di tipi di dati che possono essere pubblicati, vedere [Data Type Mapping for Oracle Publishers](non-sql/data-type-mapping-for-oracle-publishers.md). Le colonne contenenti tipi di dati che non possono essere pubblicati non vengono visualizzate.  
  
## <a name="column-filters"></a>Filtri colonne  
 Applicare un filtro alle colonne in questa pagina espandendo una tabella nel riquadro **Oggetti da pubblicare** e quindi selezionando solo le colonne necessarie. Le righe possono essere filtrate nella pagina **Filtro righe tabella** di questa procedura guidata. L'applicazione di un filtro alle colonne è utile per diversi motivi, inclusi motivi di sicurezza, ovvero per impedire la replica dei dati sensibili, e di prestazione, ad esempio per evitare la replica di colonne contenenti dati BLOB (Binary Large Object). Per altre informazioni sul filtro di colonne, incluso un elenco di tipi di colonne a cui non è possibile applicare un filtro, vedere [Filtrare i dati pubblicati](publish/filter-published-data.md).  
  
## <a name="options"></a>Opzioni  
 Il riquadro **Oggetti da pubblicare** consente di:  
  
-   Visualizzare tutti gli oggetti disponibili per la replica.  
  
-   Aggiungere un articolo a una pubblicazione selezionando la casella di controllo accanto a tale oggetto.  
  
-   Rimuovere un articolo da una pubblicazione deselezionando la casella di controllo accanto a tale oggetto. Per informazioni sull'eliminazione di articoli, vedere [Aggiungere ed eliminare articoli in pubblicazioni esistenti](publish/add-articles-to-and-drop-articles-from-existing-publications.md).  
  
-   Includere tutti gli oggetti di un determinato tipo, quale una tabella, nella pubblicazione selezionando la casella di controllo accanto a tale tipo di oggetto, ad esempio **Tabelle**.  
  
-   Espandere tutti i nodi della tabella per visualizzarne le relative colonne.  
  
-   Escludere tramite un filtro le colonne della tabella dalla pubblicazione deselezionando la casella di controllo accanto alla colonna oppure includere le colonne non pubblicate selezionando la casella di controllo.  
  
-   Fare clic con il pulsante destro del mouse su un oggetto nel riquadro per visualizzare un menu di comandi per tale oggetto.  
  
 **Proprietà articolo**  
 Fare clic su **Proprietà articolo** e quindi su una delle opzioni seguenti:  
  
-   Fare clic su **Imposta proprietà dell'articolo di \<TipoOggetto> evidenziato** per aprire la finestra di dialogo **Proprietà articolo - \<NomeOggetto>** . Le modifiche apportate alle proprietà in questa finestra di dialogo vengono applicate solo all'oggetto evidenziato nel riquadro degli oggetti nella pagina **Articoli**.  
  
-   Fare clic su **Imposta proprietà di tutti gli articoli di \<TipoOggetto>** per aprire la finestra di dialogo **Proprietà di tutti gli articoli \<TipoOggetto>** . Le modifiche apportate alle proprietà in questa finestra di dialogo vengono applicate a tutti gli oggetti del tipo indicato nel riquadro degli oggetti all'interno della pagina **Articoli**, inclusi quelli non ancora selezionati per la pubblicazione.  
  
    > [!NOTE]  
    >  Le modifiche apportate alle proprietà nella finestra di dialogo **Proprietà di tutti gli articoli \<TipoOggetto>** sostituiscono tutte le modifiche eseguite precedentemente nella finestra di dialogo **Proprietà articolo - \<NomeOggetto>** . Se ad esempio si desidera impostare alcuni valori predefiniti per tutti gli articoli di un tipo di oggetto e, al contempo, alcune proprietà per singoli oggetti, è necessario impostare innanzitutto i valori predefiniti per tutti gli articoli, quindi le proprietà relative ai singoli oggetti.  
  
 **La tabella evidenziata è di tipo solo download**  
 Solo per la replica di tipo merge. Solo [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versioni successive. Selezionare questa opzione per indicare che non è possibile apportare modifiche nel Sottoscrittore se si utilizza una sottoscrizione client. Poiché non è possibile aggiornare gli articoli di solo download nel Sottoscrittore, i metadati di rilevamento non vengono inviati ai Sottoscrittori. Ciò può comportare uno spazio di archiviazione ridotto sui Sottoscrittori e un vantaggio in termini di prestazioni, soprattutto se la connessione di rete è lenta. Questa opzione corrisponde all'impostazione dell'opzione **Direzione sincronizzazione** sul valore **Solo download sul Sottoscrittore, non consentire modifiche del Sottoscrittore** nella finestra di dialogo **Proprietà articolo** . Per altre informazioni, vedere [Ottimizzare le prestazioni della replica di tipo merge con gli articoli di solo download](merge/optimize-merge-replication-performance-with-download-only-articles.md).  
  
 **Mostra solo oggetti selezionati nell'elenco**  
 Selezionare questa casella di controllo per visualizzare solo gli articoli selezionati nel riquadro degli oggetti.  
  
## <a name="see-also"></a>Vedere anche  
 [Create a Publication](publish/create-a-publication.md)   
 [Visualizzare e modificare le proprietà della pubblicazione](publish/view-and-modify-publication-properties.md)   
 [Creare e applicare lo snapshot iniziale](create-and-apply-the-initial-snapshot.md)   
 [Reinizializzare una sottoscrizione](reinitialize-a-subscription.md)   
 [Pubblicare dati e oggetti di database](publish/publish-data-and-database-objects.md)  
  
  
