---
title: Filtro righe tabella | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.newpubwizard.filtertablerows.f1
ms.assetid: 005f5c71-0401-490e-8823-adc54a2e9675
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 6974e8c3d07bd1da5fd48a4bbbc8e49c86e2d314
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68128093"
---
# <a name="filter-table-rows"></a>Filtro righe tabella
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  La pagina **Filtro righe tabella** consente di:  
  
-   Applicare filtri di riga statici agli articoli di tabella nelle pubblicazioni snapshot, transazionali e di tipo merge.  
  
-   Applicare filtri di riga con parametri agli articoli di tabella nelle pubblicazioni di tipo merge.  
  
-   Utilizzare filtri join per estendere i filtri degli articoli di tabelle di merge agli articoli di tabelle correlate.  
  
 Per altre informazioni sulle opzioni di filtro, vedere [Filtrare i dati pubblicati](../../relational-databases/replication/publish/filter-published-data.md). È possibile modificare i filtri nella pagina **Filtra righe** della finestra di dialogo **Proprietà pubblicazione** .  
  
 Per ottimizzare le prestazioni dell'applicazione e ridurre la quantità di spazio di archiviazione necessario o per limitare la disponibilità di determinati dati a Sottoscrittori specifici, è consigliabile pubblicare solo i dati necessari. La pubblicazione può includere sia tabelle filtrate che tabelle non filtrate. È possibile ad esempio includere la tabella completa, non filtrata, dei prodotti della società e utilizzare i filtri di riga per generare una tabella filtrata dei clienti di una regione specifica. Tramite l'applicazione di filtri ai dati pubblicati è possibile:  
  
-   Ridurre al minimo la quantità di dati inviati in rete.  
  
-   Ridurre la quantità di spazio di archiviazione necessaria nel Sottoscrittore.  
  
-   Personalizzare le pubblicazioni e le applicazioni in base ai requisiti dei singoli Sottoscrittori.  
  
-   Evitare o limitare i conflitti in caso di aggiornamento dei dati da parte dei Sottoscrittori grazie alla possibilità di inviare partizioni di dati diverse a Sottoscrittori diversi. In due Sottoscrittori pertanto non verranno mai aggiornati gli stessi valori di dati.  
  
-   Evitare la trasmissione di dati riservati. È possibile utilizzare i filtri di riga e di colonna per limitare l'accesso ai dati da parte dei Sottoscrittori. Nella replica di tipo merge è necessario tenere in considerazione alcuni aspetti relativi alla sicurezza se si utilizza un filtro con parametri che include HOST_NAME(). Per ulteriori informazioni, vedere la sezione relativa all'utilizzo dei filtri con HOST_NAME() in [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).  
  
 In un filtro non deve essere inclusa la colonna **rowguidcol** utilizzata dalla replica per identificare le righe. Per impostazione predefinita, si tratta della colonna aggiunta al momento dell'impostazione della replica di tipo merge ed è denominata **rowguid**.  
  
## <a name="options"></a>Opzioni  
 **Tabelle filtrate**  
 Questo riquadro viene popolato di filtri mano a mano che vengono aggiunti agli articoli di tabella nella pubblicazione. Le tabelle con filtri di riga vengono visualizzate nel riquadro come nodi di livello principale. Per le pubblicazioni di tipo merge, le tabelle alle quali sono stati estesi i filtri tramite un filtro di join vengono visualizzate come nodi figlio.  
  
 **Aggiungi**  
 Fare clic su **Aggiungi** per visualizzare una finestra di dialogo che consente di filtrare gli articoli di tabella. Facendo clic su **Aggiungi** per una pubblicazione snapshot o transazionale verrà visualizzata immediatamente una finestra di dialogo. Facendo clic su **Aggiungi** per una pubblicazione di tipo merge verranno visualizzate tre opzioni: **Aggiungi filtro**; **Aggiungi join per estendere il filtro selezionato**; **Genera filtri automaticamente**.  
  
-   Selezionare l'opzione **Aggiungi filtro** per visualizzare la finestra di dialogo **Aggiungi filtro** , che consente di applicare i filtri di riga a un articolo di tabella. Nella finestra di dialogo **Aggiungi filtro** è possibile, ad esempio, specificare che una tabella contenente dati sui clienti possa contenere solo dati sui clienti francesi quando viene replicata nei Sottoscrittori.  
  
-   Selezionare **Aggiungi join per estendere il filtro selezionato** per visualizzare la finestra di dialogo **Aggiungi join** , La finestra di dialogo **Aggiungi join** consente di estendere un filtro di riga in modo che filtri i dati delle tabelle correlate alla tabella con il filtro di riga. Se, ad esempio, una tabella clienti viene filtrata in modo che contenga solo dati relativi ai clienti francesi ed esiste una tabella correlata per gli ordini dei clienti, è possibile definire un join tra le due tabelle in modo che la tabella degli ordini includa solo gli ordini dei clienti francesi.  
  
    > [!NOTE]  
    >  Questa opzione è disponibile solo selezionando prima la tabella di base del join nel riquadro dei filtri.  
  
-   Selezionare **Genera filtri automaticamente** per visualizzare la finestra di dialogo **Genera filtri** , che consente di definire un filtro di riga su una tabella in una pubblicazione di tipo merge che viene automaticamente esteso dalla replica ad altre tabelle correlate tramite relazioni di chiave esterna. Ad esempio, una pubblicazione può includere tre tabelle: una tabella dei clienti, una tabella degli ordini con una chiave esterna alla tabella dei clienti e una tabella dei dettagli degli ordini con una chiave esterna alla tabella degli ordini. Definendo un filtro di riga sulla tabella dei clienti, la replica lo estenderà alle altre tabelle.  
  
    > [!NOTE]  
    >  Se i filtri vengono generati automaticamente dalla replica, qualsiasi filtro esistente per la pubblicazione viene eliminato. Per includere sia i filtri generati automaticamente che i filtri specificati manualmente, generare i filtri prima di specificarne altri. È possibile specificare un solo set di filtri generati automaticamente per ogni pubblicazione.  
  
 **Modifica**  
 Selezionare un filtro di riga o un filtro join nel riquadro dei filtri e fare clic su **Modifica** per visualizzare la finestra di dialogo **Modifica filtro** o **Modifica join** .  
  
 **Elimina**  
 Selezionare un filtro di riga o un filtro join nel riquadro dei filtri e fare clic su **Elimina** per eliminare il filtro.  
  
 **Trova tabella**  
 Solo per pubblicazioni di tipo merge con filtri join. Fare clic su **Trova tabella** per trovare una tabella in un'albero di filtro complesso. In un database con relazioni complesse una tabella può essere unita in join a più tabelle e pertanto può apparire in più posizioni all'interno dell'albero di filtro.  
  
 La tabella effettiva appare solo in una posizione all'interno dell'albero, mentre nelle altre posizioni è rappresentata da un collegamento. Un collegamento a una tabella è semplicemente un riferimento alla tabella e non ne visualizza i nodi figlio. Un nodo collegamento è contrassegnato dalla freccia di collegamento ed espandendo tale nodo viene visualizzato il testo **Fare clic su Trova tabella per vedere la tabella per \<nometabella>** .  
  
 Selezionare un nodo di collegamento nel riquadro e fare clic su **Trova tabella**. Il riquadro viene esteso e la tabella evidenziata. Se si fa clic su **Trova tabella** senza aver selezionato un nodo collegamento verrà visualizzata la finestra di dialogo **Trova tabella** .  
  
 **Filter**  
 Contiene la definizione [!INCLUDE[tsql](../../includes/tsql-md.md)] del filtro selezionato nel riquadro dei filtri.  
  
## <a name="see-also"></a>Vedere anche  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [Visualizzare e modificare le proprietà della pubblicazione](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [Filtrare i dati pubblicati](../../relational-databases/replication/publish/filter-published-data.md)   
 [Join Filters](../../relational-databases/replication/merge/join-filters.md)   
 [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)   
 [Pubblicare dati e oggetti di database](../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  
