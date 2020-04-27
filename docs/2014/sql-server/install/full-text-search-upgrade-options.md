---
title: Opzioni di aggiornamento della ricerca full-text | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- Full-Text Search
- Upgrade options, Full-Text Search
ms.assetid: 16c9376b-5fbb-4495-a429-06a2493849c9
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 575105d61446f2fd272e4087457e7762c1abb2e8
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66095092"
---
# <a name="full-text-search-upgrade-options"></a>Opzioni di aggiornamento della ricerca full-text
  Utilizzare la pagina Opzioni di aggiornamento della ricerca full-text dell'Installazione guidata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per selezionare l'opzione di aggiornamento della ricerca full-text da utilizzare per l'aggiornamento dei database.  
  
 In [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ogni indice full-text risiede in un catalogo full-text che appartiene a un filegroup, dispone di un percorso fisico e viene considerato un file di database. A questo punto, un catalogo full-text è un concetto logico, ovvero un oggetto virtuale, che fa riferimento a un gruppo di indici full-text. Pertanto, un nuovo catalogo full-text non viene considerato un file di database con un percorso fisico. Tuttavia, durante l'aggiornamento di un catalogo full-text contenente file di dati viene creato un nuovo filegroup nello stesso disco mantenendo in questo modo il vecchio comportamento I/O su disco dopo l'aggiornamento. Tutti gli indici full-text di quel catalogo vengono posizionati nel nuovo filegroup se esiste il percorso radice. Se il vecchio percorso del catalogo full-text non è valido, l'indice full-text rimane nello stesso filegroup della tabella di base o nel filegroup primario nel caso di una tabella partizionata.  
  
## <a name="options"></a>Opzioni  
 Quando si esegue l'aggiornamento a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], scegliere una delle opzioni di aggiornamento full-text seguenti.  
  
 **Importa**  
 I cataloghi full-text vengono importati. In genere, l'importazione è molto più veloce della ricompilazione. Se ad esempio si utilizza solo una CPU, l'importazione è di circa 10 volte più veloce della ricompilazione. Tuttavia, un catalogo full-text importato da [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] non utilizza i word breaker nuovi e migliorati, pertanto potrebbe essere necessario ricompilare i cataloghi full-text.  
  
> [!NOTE]  
>  La ricompilazione può essere eseguita in modalità a thread multipli e, nel caso in cui siano disponibili più di 10 CPU, può risultare più veloce dell'importazione se si consente alla ricompilazione di utilizzare tutte le CPU.  
  
 Se un catalogo full-text non è disponibile, gli indici full-text associati vengono ricreati. Questa opzione è disponibile solo per i database di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] .  
  
 Per informazioni sull'impatto dell'importazione di un indice full-text, vedere "Considerazioni per la scelta di un'opzione di aggiornamento full-text" più avanti in questo argomento.  
  
 **Ricompilare**  
 I cataloghi full-text vengono ricompilati utilizzando i nuovi word breaker ottimizzati. La ricompilazione degli indici può richiedere molto tempo. Dopo l'aggiornamento, inoltre, potrebbe essere necessaria una quantità significativa di CPU e di memoria.  
  
 **Reimposta**  
 I cataloghi full-text vengono ripristinati. Quando si esegue l'aggiornamento da [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], i file dei cataloghi full-text vengono rimossi, ma i metadati per i cataloghi full-text e gli indici full-text vengono mantenuti. Dopo l'aggiornamento, in tutti gli indici full-text il rilevamento delle modifiche viene disabilitato e le ricerche per indicizzazione non vengono avviate automaticamente. Il catalogo resterà vuoto fino a quando non si eseguirà manualmente un popolamento completo al termine dell'aggiornamento.  
  
 Tutte queste opzioni di aggiornamento consentono ai database aggiornati di sfruttare appieno i miglioramenti delle prestazioni full-text.  
  
## <a name="considerations-for-choosing-a-full-text-upgrade-option"></a>Considerazioni per la scelta di un'opzione di aggiornamento full-text  
 Quando si sceglie l'opzione di aggiornamento, considerare gli elementi seguenti:  
  
-   Modalità di utilizzo dei word breaker  
  
     Il servizio di ricerca full-text in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] include nuovi word breaker e stemmer che potrebbero modificare i risultati delle query full-text rispetto a [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] per un modello di testo o uno scenario specifico. Pertanto, la modalità di utilizzo dei word breaker è importante nella scelta di un'opzione di aggiornamento appropriata:  
  
    -   Se i word breaker della lingua utilizzata per la ricerca full-text non sono stati modificati o se l'accuratezza delle chiamate non è fondamentale, è consigliabile utilizzare l'importazione. Se successivamente si verificano problemi relativi alle chiamate, è possibile eseguire l'aggiornamento ai nuovi word breaker ricompilando semplicemente i cataloghi full-text.  
  
    -   Se invece l'accuratezza delle chiamate è importante e si utilizza uno dei word breaker aggiunti dopo [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], è consigliabile eseguire la ricompilazione.  
  
-   Eventuale presenza di indici full-text compilati in colonne chiave full-text di tipo integer  
  
     Con la ricompilazione vengono eseguite ottimizzazioni interne che in alcuni casi migliorano le prestazioni di esecuzione delle query dell'indice full-text aggiornato. In particolare, se si dispone di cataloghi full-text che contengono indici full-text per i quali la colonna chiave full-text della tabella di base è un tipo di dati integer, la ricompilazione consente di ottenere prestazioni ideali delle query full-text dopo l'aggiornamento. In questo caso, è consigliabile usare l'opzione **Ricompila** .  
  
    > [!NOTE]  
    >  Per gli indici full-text in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]è consigliabile che la colonna utilizzata come chiave full-text sia un tipo di dati integer. Per altre informazioni, vedere [Miglioramento delle prestazioni di indici full-text](../../relational-databases/indexes/indexes.md).  
  
-   Priorità della disponibilità online dell'istanza del server  
  
     L'importazione o la ricompilazione durante l'aggiornamento richiede l'utilizzo di molte risorse della CPU ritardando in questo modo l'aggiornamento del resto dell'istanza del server e la disponibilità online dell'istanza stessa. Se la disponibilità online dell'istanza del server è essenziale e si desidera eseguire un popolamento manuale dopo l'aggiornamento, è consigliabile utilizzare l'opzione **Reimposta** .  
  
## <a name="additional-resources"></a>Risorse aggiuntive  
  
