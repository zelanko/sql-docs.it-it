---
title: Progettazione di aggregazioni (XMLA) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b9f681b3c99bd0e8351a844f28b16be6249de199
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63288500"
---
# <a name="designing-aggregations-xmla"></a>Progettazione di aggregazioni (XMLA)
  Le progettazioni delle aggregazioni sono associate alle partizioni di un gruppo di misure specifico per garantire che utilizzino la stessa struttura nell'archiviazione delle aggregazioni. Usando la stessa struttura di archiviazione per le partizioni consente di definire in modo semplice partizioni che possono essere unite in un secondo momento usando il [MergePartitions](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/mergepartitions-element-xmla) comando. Per altre informazioni sulle progettazioni delle aggregazioni, vedere [aggregazioni e progettazione di aggregazioni](../../analysis-services/multidimensional-models-olap-logical-cube-objects/aggregations-and-aggregation-designs.md).  
  
 Per definire le aggregazioni per una progettazione delle aggregazioni, è possibile usare la [DesignAggregations](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/designaggregations-element-xmla) comando XML for Analysis (XMLA). Il **DesignAggregations** comando dispone di proprietà che identificano quale progettazione delle aggregazioni da usare come riferimento e come controllare il processo di progettazione in base al riferimento. Usando il **DesignAggregations** comando e le relative proprietà, è possibile progettare le aggregazioni in modo iterativo oppure in batch e quindi visualizzare le statistiche relative alla progettazione risultanti per valutare il processo di progettazione.  
  
## <a name="specifying-an-aggregation-design"></a>Specifica di una progettazione delle aggregazioni  
 Il [oggetti](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla) proprietà delle **DesignAggregations** comando deve contenere un riferimento a una progettazione delle aggregazioni esistente. Il riferimento all'oggetto contiene un identificatore di database, un identificatore di cubo, un identificatore del gruppo di misure e un identificatore della progettazione delle aggregazioni. Se la progettazione delle aggregazioni non esiste, si verifica un errore.  
  
## <a name="controlling-the-design-process"></a>Controllo del processo di progettazione  
 È possibile usare le proprietà seguenti del **DesignAggregations** comando per controllare l'algoritmo utilizzato per definire aggregazioni per la progettazione delle aggregazioni:  
  
-   Il [passaggi](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/steps-element-xmla) proprietà determina il numero di iterazioni di **DesignAggregations** comando da eseguire prima che restituisca il controllo all'applicazione client.  
  
-   Il [tempo](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/time-element-xmla) proprietà determina quanti millisecondi la **DesignAggregations** comando da eseguire prima che restituisca il controllo all'applicazione client.  
  
-   Il [Optimization](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/optimization-element-xmla) proprietà determina la percentuale stimata di miglioramento delle prestazioni di **DesignAggregations** comando deve provare a raggiungere. Se si progettano le aggregazioni in modo iterativo, è necessario inviare questa proprietà solo al primo comando.  
  
-   Il [memorizzazione](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/storage-element-xmla) proprietà determina la quantità stimata di archiviazione su disco, in byte usata dal **DesignAggregations** comando. Se si progettano le aggregazioni in modo iterativo, è necessario inviare questa proprietà solo al primo comando.  
  
-   Il [Materialize](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/materialize-element-xmla) proprietà determina se il **DesignAggregations** comando deve creare le aggregazioni definite durante il processo di progettazione. Se si progettano le aggregazioni in modo iterativo, questa proprietà deve essere impostata su false fino a quando non è possibile salvare le aggregazioni progettate. Quando la proprietà viene impostata su true, il processo di progettazione corrente termina e le aggregazioni definite vengono aggiunte alla progettazione delle aggregazioni specificata.  
  
## <a name="specifying-queries"></a>Specifica di query  
 Il comando DesignAggregations supporta il comando per l'ottimizzazione basata sull'utilizzo includendo uno o più **Query** elementi nel [query](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/queries-element-xmla) proprietà. Il **query** proprietà può contenere uno o più [Query](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/query-element-xmla) elementi. Se il **query** proprietà non contiene alcun **Query** elementi, la progettazione delle aggregazioni specificata nel **oggetto** elemento utilizza una struttura predefinita che contiene un set generale di aggregazioni. Questo set generale di aggregazioni è progettato per soddisfare i criteri specificati nel **Optimization** e **archiviazione** le proprietà del **DesignAggregations** comando.  
  
 Ogni elemento **Query** rappresenta una query di tipo goal utilizzata dal processo di progettazione per definire le aggregazioni destinate alle query utilizzate più di frequente. È possibile specificare query di tipo goal personalizzate oppure utilizzare le informazioni archiviate da un'istanza di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] nel log di query per recuperare le informazioni sulle query utilizzate più di frequente. L'ottimizzazione guidata basata sull'utilizzo Usa i log di query per recuperare query di tipo goal basate sul tempo, utilizzo o un utente specificato durante l'invio di un **DesignAggregations** comando. Per altre informazioni, vedere [basata sull'utilizzo della Guida di ottimizzazione guidata F1](http://msdn.microsoft.com/library/e5f5a938-ae7c-4f4e-9416-a7f94ac82763).  
  
 Se si stanno progettando aggregazioni in modo iterativo, è necessario passare le query di tipo goal solo al primo comando **DesignAggregations** , in quanto l'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] archivia queste query e le utilizza durante i comandi **DesignAggregations** successivi. Dopo avere passato query di tipo goal al primo comando **DesignAggregations** di un processo iterativo, qualsiasi comando **DesignAggregations** successivo che contiene query di tipo goal nella proprietà **Queries** genera un errore.  
  
 L'elemento **Query** contiene un valore delimitato da virgole in cui sono presenti gli argomenti seguenti:  
  
 *Frequency*,*Dataset*[,*Dataset*...]  
  
 *Frequenza*  
 Fattore di ponderazione corrispondente al numero di volte che la query è stata eseguita in precedenza. Se l'elemento **Query** rappresenta una nuova query, il valore *Frequency* rappresenta il fattore del ponderazione utilizzato dal processo di progettazione per valutare la query. Con l'aumentare del valore della frequenza, aumenta il peso associato alla query durante il processo di progettazione.  
  
 *Set di dati*  
 Stringa numerica che specifica gli attributi di una dimensione da includere nella query. Questa stringa deve avere un numero di caratteri uguale al numero di attributi della dimensione. Il valore zero (0) indica che l'attributo nella posizione ordinale specificata non è incluso nella query per la dimensione specificata, mentre il valore uno (1) indica che l'attributo nella posizione ordinale specificata è incluso nella query per la dimensione specificata.  
  
 La stringa "011" fa riferimento ad esempio a una query relativa a una dimensione con tre attributi, di cui il secondo e il terzo sono inclusi nella query.  
  
> [!NOTE]  
>  Alcuni attributi non vengono considerati nel set di dati. Per altre informazioni sugli attributi esclusi, vedere [elemento Query &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/query-element-xmla).  
  
 Ogni dimensione nel gruppo di misure che contiene la progettazione delle aggregazioni è rappresentata da un valore *Dataset* nell'elemento **Query** . L'ordine dei valori *Dataset* deve corrispondere all'ordine delle dimensioni incluse nel gruppo di misure.  
  
## <a name="designing-aggregations-using-iterative-or-batch-processes"></a>Progettazione di aggregazioni tramite processi iterativi o elaborazioni batch  
 È possibile usare la **DesignAggregations** comando come parte di un processo iterativo o di un processo batch, in base all'interattività richiesta dal processo di progettazione.  
  
### <a name="designing-aggregations-using-an-iterative-process"></a>Progettazione di aggregazioni tramite un processo iterativo  
 Per progettare in modo iterativo le aggregazioni, inviare più **DesignAggregations** comandi per fornire un controllo accurato sul processo di progettazione. Questo approccio viene utilizzato anche dalla Progettazione guidata aggregazioni per ottenere lo stesso scopo. Per altre informazioni, vedere [della Guida F1 di aggregazione progettazione guidata](http://msdn.microsoft.com/library/39e23cf1-6405-4fb6-bc14-ba103314362d).  
  
> [!NOTE]  
>  Per progettare in modo iterativo le aggregazioni, è necessaria una sessione esplicita. Per altre informazioni sulle sessioni esplicite, vedere [alla gestione delle connessioni e sessioni &#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md).  
  
 Per avviare il processo iterativo, è prima necessario inviare una **DesignAggregations** comando che contiene le informazioni seguenti:  
  
-   Il **memorizzazione** e **ottimizzazione** i valori delle proprietà in cui è destinato l'intero processo di progettazione.  
  
-   Il **passaggi** e **ora** i valori delle proprietà in cui viene limitato il primo passaggio del processo di progettazione.  
  
-   Se si desidera che Ottimizzazione basata sull'utilizzo, la **query** proprietà che contiene l'obiettivo esegue una query sul quale è destinato l'intero processo di progettazione.  
  
-   Il **Materialize** proprietà impostata su false. L'impostazione di questa proprietà su false indica che durante il processo di progettazione le aggregazioni definite non vengono salvate nella progettazione delle aggregazioni quando il comando è completato.  
  
 Quando il primo **DesignAggregations** comando al termine, il comando restituisce un set di righe contenente statistiche relative alla progettazione. È possibile valutare tali statistiche per determinare se il processo di progettazione deve continuare o se è completato. Se il processo deve continuare, è quindi inviare un'altra **DesignAggregations** comandi che contiene il **passaggi** e **ora** valori con cui elaborare questo passaggio della progettazione è limitato. È possibile valutare le statistiche risultanti e successivamente determinare se il processo di progettazione deve continuare. Questo processo iterativo di invio **DesignAggregations** comandi e la valutazione dei risultati continua fino a quando non si raggiungono gli obiettivi e dispone di un set appropriato di aggregazioni definite.  
  
 Dopo avere ottenuto il set di aggregazioni desiderato, si invia un'ultima **DesignAggregations** comando. Questo finale **DesignAggregations** comando è necessario relativo **passaggi** proprietà impostata su 1 e il relativo **Materialize** proprietà impostata su true. Utilizzando queste impostazioni, finale **DesignAggregations** comando completa il processo di progettazione e Salva l'aggregazione definita per la progettazione delle aggregazioni.  
  
### <a name="designing-aggregations-using-a-batch-process"></a>Progettazione di aggregazioni tramite un'elaborazione batch  
 È anche possibile progettare le aggregazioni in un processo batch inviando un unico **DesignAggregations** comandi che contiene il **passaggi**, **ora**, **archiviazione** , e **ottimizzazione** i valori delle proprietà in cui è destinato e limitato l'intero processo di progettazione. Se si desidera che Ottimizzazione basata sull'utilizzo, la query di tipo goal in cui è indirizzato il processo di progettazione deve essere presente anche nel **query** proprietà. Assicurarsi anche che il **Materialize** proprietà è impostata su true, in modo che il processo di progettazione Salva le aggregazioni definite per la progettazione delle aggregazioni quando il completamento del comando.  
  
 È possibile progettare aggregazioni tramite un'elaborazione batch in una sessione implicita oppure in una esplicita. Per altre informazioni sulle sessioni implicite ed esplicite, vedere [alla gestione delle connessioni e sessioni &#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md).  
  
## <a name="returning-design-statistics"></a>Restituzione di statistiche relative alla progettazione  
 Quando la **DesignAggregations** comando restituisce il controllo all'applicazione client, il comando restituisce un set di righe che contiene una singola riga che rappresenta le statistiche relative alla progettazione per il comando. Nel set di righe sono contenute le colonne elencate nella tabella seguente.  
  
|colonna|Tipo di dati|Descrizione|  
|------------|---------------|-----------------|  
|Passaggi|Valore intero|Numero di passaggi eseguiti dal comando prima di restituire il controllo all'applicazione client.|  
|Time|Long integer|Numero di millisecondi necessari al comando prima di restituire il controllo all'applicazione client.|  
|Optimization|Double|Percentuale stimata di miglioramento delle prestazioni ottenuta dal comando prima di restituire il controllo all'applicazione client.|  
|Archiviazione|Long integer|Numero stimato di byte necessari al comando prima di restituire il controllo all'applicazione client.|  
|Aggregations|Long integer|Numero di aggregazioni definite dal comando prima di restituire il controllo all'applicazione client.|  
|LastStep|Boolean|Indica se i dati nel set di righe rappresentano l'ultimo passaggio del processo di progettazione. Se il **Materialize** del comando è stata impostata su true, il valore di questa colonna è impostato su true.|  
  
 È possibile usare le statistiche relative alla progettazione contenute nel set di righe restituito dopo ogni **DesignAggregations** comando sia iterativo e progettazione di batch. Nella progettazione di tipo iterativo è possibile utilizzare le statistiche relative alla progettazione per determinare e visualizzare lo stato di avanzamento. Quando si progettano le aggregazioni in batch, è possibile utilizzare le statistiche relative alla progettazione per determinare il numero di aggregazioni create dal comando.  
  
## <a name="see-also"></a>Vedere anche  
 [Sviluppo con XMLA in Analysis Services](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
