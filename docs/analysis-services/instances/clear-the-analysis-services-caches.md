---
title: Cancella la cache di Analysis Services | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 0b9276d0a8684023d8e6dba1a890b5f1698a017a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68181990"
---
# <a name="clear-the-analysis-services-caches"></a>Cancellare le cache di Analysis Services
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Analysis Services consente di memorizzare i dati nella cache per migliorare le prestazioni delle query. In questo argomento vengono forniti consigli per l'utilizzo del comando XMLA ClearCache con cui cancellare le cache create in risposta a una query MDX. Gli effetti dell'esecuzione di ClearCache variano a seconda che si utilizzi un modello tabulare o multidimensionale.  
  
 **Quando cancellare la cache per i modelli multidimensionali**  
  
 Per i database multidimensionali, in Analysis Services le cache vengono compilate nel motore delle formule in caso di valutazione di un calcolo e nel motore di archiviazione per i risultati delle query sulla dimensione e delle query sul gruppo di misure. Le query sul gruppo di misure si verificano quando tramite il motore delle formule devono essere misurati dati per una coordinata o un sottocubo di cella. Le query sulla dimensione si verificano in caso di esecuzione di query sulle gerarchie non naturali e di applicazione di Auto Exist.  
  
 La cancellazione della cache è consigliata quando si effettuano test delle prestazioni. Cancellando la cache tra le esecuzioni dei test, ci si assicura che la memorizzazione nella cache non distorca i risultati dei test in cui viene misurato l'impatto di una modifica della progettazione della query.  
  
 **Quando cancellare la cache per i modelli tabulari**  
  
 I modelli tabulari generalmente vengono archiviati in memoria, dove aggregazioni e altri calcoli vengono eseguiti al momento dell'esecuzione di una query. In tal senso, il comando ClearCache ha un effetto limitato sui modelli tabulari. Per un modello tabulare, è possibile che vengano aggiunti dati alle cache di Analysis Services se vengono eseguite query MDX sul modello stesso. In particolare, per le misure DAX a cui fanno riferimento MDX e le operazioni Auto Exist, i risultati possono essere memorizzati rispettivamente nella cache delle formule e nella cache di dimensione. Notare, tuttavia, che per le gerarchie non naturali e le query sul gruppo di misure i risultati non vengono memorizzati nella cache del motore di archiviazione. Inoltre, è importante sapere che per le query DAX i risultati non vengono memorizzati nella cache del motore delle formule e di archiviazione. Nella misura in cui le cache esistono in conseguenza dell'esecuzione di query MDX, l'esecuzione del comando ClearCache su un modello tabulare comporterà l'invalidazione dei dati di sistema eventualmente memorizzati nella cache.  
  
 L'esecuzione di ClearCache cancellerà anche le cache in memoria nel motore di analisi in memoria xVelocity (VertiPaq). Il motore xVelocity gestisce un piccolo set di risultati memorizzati nella cache. L'esecuzione di ClearCache comporterà anche l'invalidazione di queste cache nel motore xVelocity.  
  
 Infine, l'esecuzione di ClearCache comporterà anche la rimozione dei dati rimasti in memoria quando un modello tabulare viene riconfigurato per la modalità **DirectQuery** . Questo è particolarmente importante se il modello contiene dati sensibili soggetti a controlli rigidi. In questo caso, l'esecuzione di ClearCache è un'azione precauzionale che è possibile intraprendere per assicurarsi che i dati sensibili siano presenti solo nelle posizioni previste. La cancellazione manuale della cache è necessaria se si utilizza [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] per distribuire il modello e modificare la modalità di query. Di contro, se si usa [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] per specificare **DirecQuery** sul modello e sulle partizioni, la cache verrà automaticamente cancellata quando si passa a tale modalità di query per il modello.  
  
 Rispetto ai consigli relativi alla cancellazione delle cache dei modelli multidimensionali durante i test delle prestazioni, non è specificamente consigliato di cancellare le cache dei modelli tabulari. Se non si gestisce la distribuzione di un modello tabulare che contiene dati sensibili, non c'è nessuna attività amministrativa specifica che richiede la cancellazione della cache.  
  
## <a name="clear-the-cache-for-analysis-services-models"></a>Cancellare la cache per i modelli di Analysis Services  
 Per cancellare la cache, utilizzare XMLA e [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. È possibile cancellare la cache a livello di database, cubo, dimensione o tabella oppure gruppo di misure. I passaggi seguenti per la cancellazione della cache a livello di database si applicano sia ai modelli multidimensionali che ai modelli tabulari.  
  
> [!NOTE]  
>  La rigorosa esecuzione di test delle prestazioni potrebbe richiedere un approccio più completo alla cancellazione della cache. Per istruzioni su come scaricare le cache di Analysis Services e del file system, vedere la sezione sulla cancellazione delle cache nella [Guida operativa di SQL Server 2008 R2 Analysis Services](http://go.microsoft.com/fwlink/?linkID=http://go.microsoft.com/fwlink/?LinkID=225539).  
  
 Sia per i modelli multidimensionali che per i modelli tabulari, la cancellazione di alcune di queste cache può essere un processo in due passaggi, costituito dall'invalidazione della cache quando viene eseguito ClearCache, seguita dallo svuotamento della cache alla ricezione della query successiva. Una riduzione dell'utilizzo di memoria sarà evidente solo dopo che la cache è stata effettivamente svuotata.  
  
 La cancellazione della cache richiede che si fornisca un identificatore di oggetto all'istruzione **ClearCache** in una query XMLA. Nel primo passaggio di questo argomento viene illustrato come ottenere un identificatore di oggetto.  
  
#### <a name="step-1-get-the-object-identifier"></a>Passaggio 1: Ottenere l'identificatore di oggetto  
  
1.  In [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]fare clic con il pulsante destro del mouse su un oggetto, selezionare **Proprietà**e copiare il valore dell'ID proprietà nel riquadro **Proprietà** . Questo approccio funziona per database, cubi, dimensioni o tabelle.  
  
2.  Per ottenere l'ID del gruppo di misure, fare clic con il pulsante destro del mouse sul gruppo di misure e selezionare **Crea script per gruppo di misure**. Scegliere **Crea** o **Modifica**e inviare la query a una finestra. L'ID del gruppo di misure sarà visibile nella definizione dell'oggetto. Copiare l'ID della definizione dell'oggetto.  
  
#### <a name="step-2-run-the-query"></a>Passaggio 2: Eseguire la query  
  
1.  In [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]fare clic con il pulsante destro del mouse su un database, scegliere **Nuova query**, quindi **XMLA**.  
  
2.  Copiare l'esempio di codice seguente nella finestra di query XMLA. Sostituire **DatabaseID** con l'ID del database nella connessione corrente.  
  
    ```  
    <ClearCache xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
      <Object>  
        <DatabaseID> Adventure Works DW Multidimensional</DatabaseID>  
      </Object>  
    </ClearCache>  
  
    ```  
  
     In alternativa, è possibile specificare un percorso di un oggetto figlio, quale un gruppo di misure, per cancellare la cache solo per quell'oggetto.  
  
    ```  
    <ClearCache xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
      <Object>  
        <DatabaseID>Adventure Works DW Multidimensional</DatabaseID>  
            <CubeID>Adventure Works</CubeID>  
            <MeasureGroupID>Fact Currency Rate</MeasureGroupID>  
      </Object>  
    </ClearCache>  
    ```  
  
3.  Premere F5 per eseguire la query. Il risultato dovrebbe essere il seguente:  
  
    ```  
    <return xmlns="urn:schemas-microsoft-com:xml-analysis">  
      <root xmlns="urn:schemas-microsoft-com:xml-analysis:empty" />  
    </return>  
    ```  
  

  
  
