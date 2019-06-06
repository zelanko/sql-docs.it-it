---
title: Informazioni sui cursori | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- cursors [ADO], about cursors
ms.assetid: 596eb4b6-c22f-4cde-b23f-172dd66c3161
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 9ad683af9cea8ca4f5bc1736a48f0662656b6ef1
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66704520"
---
# <a name="what-is-a-cursor"></a>Informazioni sui cursori
Nei database relazionali le operazioni vengono eseguite su set di righe completi. Il set di righe restituito da un'istruzione SELECT include tutte le righe che soddisfano le condizioni specificate nella clausola WHERE dell'istruzione. Il set di righe completo restituito dall'istruzione è noto come set di risultati. Le applicazioni, specialmente quelle che sono interattivi e online, non sono sempre funziona in modo efficace con l'intero set di risultati come un'unità. In tali applicazioni deve essere pertanto disponibile un meccanismo per l'elaborazione di una riga singola o di un blocco di righe di dimensioni ridotte. I cursori sono un'estensione dei set di risultati che implementano appunto tale meccanismo.  
  
 Un cursore viene implementato in una libreria di cursori. Una libreria di cursori è un software, spesso implementata come parte di un sistema di database o un'API, accesso ai dati che viene usato per gestire gli attributi dei dati restituiti da un'origine dati (un set di risultati). Questi attributi includono la gestione della concorrenza, la posizione nel set di risultati, numero di righe restituite e indica se è possibile spostare in avanti o indietro (o entrambi) tramite il risultato impostato (funzionalità di scorrimento).  
  
 Un cursore tiene traccia della posizione nel set di risultati e consente di eseguire più operazioni riga per riga in un set di risultati, con o senza dover tornare alla tabella originale. In altre parole, i cursori concettualmente restituiscono un set di risultati basato su tabelle all'interno dei database. Il cursore viene così chiamato perché indica la posizione corrente nel set di risultati, esattamente come il cursore su uno schermo indica la posizione corrente.  
  
 È importante acquisire familiarità con il concetto di cursori prima di passare a informazioni specifiche del loro utilizzo in ADO.  
  
 Utilizzo di cursori, è possibile:  
  
-   Specificare il posizionamento su righe specifiche del set di risultati.  
  
-   Recuperare una riga o un blocco di righe basato sulla posizione corrente del set di risultati.  
  
-   Modificare i dati nelle righe in corrispondenza della posizione corrente nel set di risultati.  
  
-   Definire diversi livelli di sensibilità alle modifiche dei dati apportate da altri utenti.  
  
 Ad esempio, si consideri un'applicazione che visualizza un elenco dei prodotti disponibili per un potenziale acquirente. L'aggregazione buyer scorre l'elenco per visualizzare i costi e i dettagli sul prodotto e quindi seleziona un prodotto per l'acquisto. Lo scorrimento aggiuntiva e la selezione avviene per il resto dell'elenco. Per quanto riguarda l'aggregazione buyer, i prodotti vengono visualizzati uno alla volta, ma l'applicazione usa un cursore scorrevole per esplorare il set di risultati su e giù.  
  
 È possibile utilizzare i cursori in diversi modi:  
  
-   Senza righe affatto.  
  
-   Con alcune o tutte le righe in una singola tabella.  
  
-   Con alcune o tutte le righe delle tabelle unite in join in modo logico.  
  
-   Di sola lettura o aggiornabili a livello di campo o del cursore.  
  
-   Di tipo forward-only o scorrevole completamente.  
  
-   Con i keyset del cursore che si trova nel server.  
  
-   Sensibile alle modifiche della tabella sottostante causate da altre applicazioni (ad esempio l'appartenenza, ordinamento, inserimenti, aggiornamenti ed eliminazioni).  
  
-   Esistenti nel server o client.  
  
 I cursori di sola lettura consentono agli utenti di esplorare il set di risultati e i cursori possono implementare gli aggiornamenti di singole righe di lettura/scrittura. I cursori complessi possono essere definiti con i keyset che puntano alle righe della tabella di base. Anche se alcuni cursori sono di sola lettura in avanti, altri utenti possono spostarsi avanti e indietro e fornire un aggiornamento dinamico del set di risultati in base alle modifiche che stanno effettuando altre applicazioni al database.  
  
 Non tutte le applicazioni devono utilizzare cursori per l'accesso o l'aggiornamento dati. Alcune query non richiedono infatti l'aggiornamento diretto delle righe utilizzando un cursore. I cursori devono essere una delle tecniche ultimo si sceglie di recuperare i dati, e quindi è consigliabile scegliere il cursore con impatto più basso possibile. Quando si crea un set di risultati, utilizzando una stored procedure, il set di risultati non è aggiornabile tramite cursore modificare o aggiornare i metodi.  
  
## <a name="concurrency"></a>Concorrenza  
 In alcune applicazioni multiutente è molto importante per i dati presentati all'utente finale per essere aggiornati come possibili. Un classico esempio di un sistema di questo tipo è un sistema di prenotazione delle compagnie aeree, in cui molti utenti potrebbero avere scelto lo stesso prenotazione posto sul volo specificato (e pertanto un singolo record). In casi come questo, la progettazione dell'applicazione deve gestire operazioni simultanee in un singolo record.  
  
 In altre applicazioni, la concorrenza non è importante. In questi casi, non può essere giustificata la spesa interessati a mantenere che i dati correnti in qualsiasi momento.  
  
## <a name="position"></a>Posizione  
 Un cursore tiene anche traccia della posizione corrente in un set di risultati. Considerare la posizione del cursore come un puntatore al record corrente, allo stesso modo una matrice di indice fa riferimento al valore in un percorso specifico nella matrice.  
  
## <a name="scrollability"></a>Scorrimento  
 Il tipo di cursore utilizzato dall'applicazione interessa anche la possibilità di spostarsi avanti e indietro tra le righe in un set di risultati. Ciò è talvolta detta supporto dello scorrimento. La possibilità di proseguire *e* con le versioni precedenti attraverso il risultato di un set aumenta la complessità del cursore e pertanto è più costoso implementare. Per questo motivo, è consigliabile richiedere un cursore con questa funzionalità solo quando necessario.
