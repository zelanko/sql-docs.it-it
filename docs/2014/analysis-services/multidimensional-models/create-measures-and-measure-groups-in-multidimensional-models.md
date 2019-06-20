---
title: Creare misure e gruppi di misure nei modelli multidimensionali | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- measure groups [Analysis Services], defining
ms.assetid: 1018bb2e-b89b-489e-aead-450dec5dca3b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2883a9092f7b84e8dd18954cec631b90a8bbe0e9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66076245"
---
# <a name="create-measures-and-measure-groups-in-multidimensional-models"></a>Creare misure e gruppi di misure nei modelli multidimensionali
  Una *misura* è un'aggregazione di valori di dati numerici, ad esempio somme, conteggi, valori minimi, valori massimi, medie o un'espressione MDX personalizzata creata. Un *gruppo di misure* è un contenitore per una o più misure. Tutte le misure sono disponibili in un gruppo di misure, anche se esiste una sola misura. Un cubo deve avere almeno una misura e un gruppo di misure.  
  
 In questo argomento sono contenute le sezioni seguenti:  
  
-   [Approcci per la creazione di misure](#bkmk_create)  
  
-   [Componenti di una misura](#bkmk_comps)  
  
-   [Modellazione misure e gruppi di misure su fatti e delle tabelle dei fatti](#bkmk_modeling)  
  
-   [Granularità di un gruppo di misure](#bkmk_grain)  
  
##  <a name="bkmk_create"></a> Approcci per la creazione di misure  
 Una misura può essere un elemento statico del cubo, creata in fase di progettazione, sempre presente ogni volta che si accede al cubo. È anche possibile definire una misura come *membro calcolato* usando un'espressione MDX per specificare un valore calcolato per una misura in base ad altre misure del cubo. Un membro calcolato può essere limitato a sessione o un utente.  
  
 Per creare una misura o un gruppo di misure, usare uno di questi approcci:  
  
|||  
|-|-|  
|Creazione guidata cubo|Eseguire la creazione guidata cubo in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] per creare un cubo.<br /><br /> In Esplora soluzioni fare clic con il pulsante destro del mouse su **Cubi** e scegliere **Nuovo cubo**. Per altre informazioni su questi passaggi, vedere [Modellazione multidimensionale &#40;esercitazione di AdventureWorks&#41;](../multidimensional-modeling-adventure-works-tutorial.md).<br /><br /> Quando si crea un cubo basato su tabelle da un data warehouse esistente, le definizioni per le misure e un gruppo di misure materializzare come parte del processo di creazione del cubo. Nella procedura guidata, scegliendo i fatti e delle tabelle dei fatti per usare come base per la misura e misurare gli oggetti gruppo nel cubo.|  
|Finestra di dialogo Nuova misura|Supponendo che il cubo già esiste [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], fare doppio clic sul nome del cubo in Esplora soluzioni per aprirlo in Progettazione cubi. Nel riquadro misure destro del mouse sul nodo principale per creare un nuovo gruppo di misure o nuove misure specificando una tabella di origine, la colonna e il tipo di aggregazione. Utilizzando questo approccio, è necessario scegliere il metodo di aggregazione da un elenco fisso di funzioni predefinite. Vedere [Use Aggregate Functions](use-aggregate-functions.md) per una discussione più comunemente utilizzati aggregazioni.|  
|membro calcolato|Membri calcolati aggiungono funzionalità di analisi e la flessibilità di un cubo in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] perché è possibile controllare come e quando vengono creati. In alcuni casi è sufficiente una misura temporaneamente, per la durata di una sessione utente o in Management Studio come parte di un'indagine.<br /><br /> In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], aprire la scheda calcoli per creare un nuovo membro calcolato.<br /><br /> Scegliere questo approccio quando basare una misura su un'espressione MDX. Vedere gli argomenti seguenti per altre informazioni: [Creazione di misure in MDX](mdx/mdx-building-measures.md), [calcoli](../multidimensional-models-olap-logical-cube-objects/calculations.md), [calcoli nei modelli multidimensionali](calculations-in-multidimensional-models.md) e [nozioni fondamentali sullo Scripting MDX &#40;Analysis Services&#41; ](mdx/mdx-scripting-fundamentals-analysis-services.md).|  
|MDX o XMLA|In SQL Server Management Studio, è possibile eseguire MDX o XMLA per modificare un database per includere una nuova misura calcolata. Questo approccio è utile per test ad hoc dei dati, dopo la soluzione viene distribuita a un server. Vedere [Document and Script an Analysis Services Database](document-and-script-an-analysis-services-database.md).|  
  
##  <a name="bkmk_comps"></a> Componenti di una misura  
 Una misura è un oggetto con proprietà. Oltre al nome, una misura deve disporre di un tipo di aggregazione e una colonna di origine o un'espressione utilizzata per caricare la misura con dati. È possibile modificare la definizione della misura impostandone le proprietà.  
  
|||  
|-|-|  
|**origine**|La maggior parte delle misure deriva da colonne numeriche presenti nelle tabelle dei fatti in un data warehouse esterno, ad esempio la colonna Sales Amount nelle tabelle Internet Sales e Reseller Sales del data warehouse AdventureWorks, ma è anche possibile creare nuove misure basate interamente sui calcoli definiti.<br /><br /> Per definire le misure è possibile usare le colonne degli attributi delle tabelle delle dimensioni. Queste misure, tuttavia, in genere sono di tipo semiadditivo o non additivo per quanto riguarda la modalità di aggregazione. Per altre informazioni sulle funzioni semiadditive, vedere [Definire una funzione semiadditiva](define-semiadditive-behavior.md).|  
|**aggregazione**|Per impostazione predefinita, le misure vengono sommate in ogni dimensione. La proprietà `AggregateFunction` consente tuttavia di modificare tale comportamento. Vedere [Use Aggregate Functions](use-aggregate-functions.md) per un elenco.|  
|**Proprietà**|Vedere [Configure Measure Properties](configure-measure-properties.md) per le descrizioni di proprietà aggiuntive.|  
  
##  <a name="bkmk_modeling"></a> Modellazione misure e gruppi di misure su fatti e delle tabelle dei fatti  
 Prima di eseguire una procedura guidata, è utile per comprendere i principi di modellazione dietro la definizione della misura.  
  
 Misure e gruppi di misure sono gli oggetti multidimensionali che rappresentano i fatti e delle tabelle dei fatti in un data warehouse esterno. Nella maggior parte dei casi, misure e gruppi di misure basa sugli oggetti in una vista origine dati, che a sua volta, vengono creati dal data warehouse sottostante.  
  
 Nella figura seguente vengono rappresentate la tabella dei fatti **FactSalesQuota** e le due tabelle delle dimensioni associate **DimTime** e **DimEmployee**. Cubo di esempio Adventure Works, queste tabelle vengono utilizzate come base per il gruppo di misure Sales Quotas e le dimensioni Time ed Employee.  
  
 ![Tabella FactSalesQuota con due tabelle delle dimensioni](../media/factsalesquota.gif "tabella FactSalesQuota con due tabelle delle dimensioni")  
  
 La tabella dei fatti contiene due tipi di colonne di base: le colonne degli attributi e le colonne delle misure.  
  
-   Le colonne degli attributi vengono utilizzate per creare relazioni di chiave esterna a tabelle delle dimensioni in modo da poter organizzare i dati quantificabili nelle colonne delle misure in base ai dati contenuti nelle tabelle delle dimensioni. Le colonne degli attributi vengono inoltre utilizzate per definire la granularità di una tabella dei fatti e del gruppo di misure.  
  
-   Le colonne delle misure definiscono le misure contenute in un gruppo di misure.  
  
 Quando si esegue la creazione guidata cubo, le chiavi esterne vengono filtrate. Nell'elenco di colonne rimanenti da selezionare, si vedrà colonne di misura più colonne di attributi che non sono identificate come chiave esterna. Nell'esempio di **FactSalesQuote** la procedura guidata includerà **CalendarYear** e **CalendarQuarter** oltre a **SalesAmountQuota**. Solo la colonna della misura **SalesAmountQuota** restituirà una misura utilizzabile per il modello multidimensionale. Le altre colonne data esistono per qualificare ogni importo della quota. È consigliabile escludere le altre colonne, **CalendarYear** e **CalendarQuarter**, dall'elenco delle misure nella creazione guidata cubo oppure rimuoverle dal gruppo di misure in un secondo momento nella finestra di progettazione.  
  
 Il punto a questa discussione è che non tutte le colonne offerte dalla procedura guidata sono utili come una misura. Utilizzare la comprensione dei dati e come utilizzarlo quando decidere le colonne da usare come misura. Tenere presente che è possibile fare doppio clic su una tabella nella vista origine dati per esplorare i dati, che consentono di identificare le colonne da usare come misure. Per altre informazioni, vedere [Esplorare dati in una vista origine dati &#40;Analysis Services&#41;](explore-data-in-a-data-source-view-analysis-services.md).  
  
> [!NOTE]  
>  Non tutte le misure derivano direttamente da un valore archiviato in una colonna della tabella dei fatti. Ad esempio, la misura **Sales Person Count** definita nel gruppo di misure **Sales Quota** del cubo di esempio Adventure Works si basa in realtà sul conteggio di valori univoci, o Distinct Count, nella colonna **EmployeeKey** della tabella dei fatti **FactSalesQuota** .  
  
##  <a name="bkmk_grain"></a> Granularità di un gruppo di misure  
 Gruppi di misure hanno un livello di dettaglio associato indica il livello di dettaglio supportato da una tabella dei fatti. La granularità viene impostata tramite la relazione di chiave esterna a una dimensione.  
  
 Ad esempio, la tabella dei fatti **FactSalesQuota** ha una relazione di chiave esterna con la tabella **DimEmployee** , ogni record nella tabella **FactSalesQuota** si riferisce a un solo dipendente, pertanto il gruppo di misure, da un punto di vista della dimensione Employee, ha una granularità a livello di singolo dipendente.  
  
 La granularità di un gruppo di misure non può essere impostata su un livello più basso del livello inferiore della dimensione da cui viene considerato il gruppo di misure, ma può essere aumentata tramite l'utilizzo di attributi aggiuntivi. Ad esempio, la tabella dei fatti **FactSalesQuota** utilizza tre colonne, **TimeKey**, **CalendarYear**e **CalendarQuarter**, per impostare la granularità della relazione con la tabella **DimTime** . Di conseguenza la granularità del gruppo di misure, dal punto di vista della dimensione temporale, è il trimestre del calendario e non il giorno, corrispondente al livello più basso della dimensione temporale.  
  
 Per specificare la granularità di un gruppo di misure in relazione a una dimensione specifica, usare la scheda **Utilizzo dimensioni** di Progettazione cubi. Per altre informazioni sulle relazioni tra dimensioni, vedere [Dimension Relationships](../multidimensional-models-olap-logical-cube-objects/dimension-relationships.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Cubi nei modelli multidimensionali](cubes-in-multidimensional-models.md)   
 [Misure e gruppi di misure](measures-and-measure-groups.md)  
  
  
