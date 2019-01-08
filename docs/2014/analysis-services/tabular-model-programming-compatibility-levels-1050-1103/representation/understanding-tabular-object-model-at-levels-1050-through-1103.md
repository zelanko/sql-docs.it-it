---
title: Comprendere il modello a oggetti tabulare | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
ms.assetid: 6077b7e8-cb3e-4480-a5de-bb602cf9d69a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 574614976a9d24f6c9cedbfede2fd5a150211416
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52525791"
---
# <a name="understanding-the-tabular-object-model"></a>Informazioni sul modello a oggetti tabulare
  Un modello tabulare è una rappresentazione logica di tabelle, relazioni, gerarchie, prospettive, misure e prestazioni chiave. In questa sezione viene illustrata l'implementazione interna tramite AMO. Visualizzare [lo sviluppo con Analysis Management Objects &#40;AMO&#41; ](https://docs.microsoft.com/bi-reference/amo/developing-with-analysis-management-objects-amo) se si ha familiarità con AMO.  
  
 In questo caso si utilizza un approccio discendente, viene prima eseguito il mapping logico agli oggetti AMO per tutti gli oggetti rilevanti nel modello tabulare, quindi viene fornita la spiegazione dell'interazione o del flusso di lavoro necessario. Un esempio di codice sorgente per creare un modello tabulare tramite AMO, Da AMO a tabulare, è disponibile in Codeplex. Nota importante sul codice di questo esempio: il codice viene fornito solo come supporto ai concetti logici illustrati in questo argomento e non deve essere utilizzato in un ambiente di produzione. L'esempio viene fornito senza supporto o garanzia.  
  
## <a name="database-representation"></a>Rappresentazione di un database  
 Un database fornisce l'oggetto contenitore per il modello tabulare. Tutti gli oggetti in un modello tabulare sono contenuti nel database. In termini di oggetti AMO, una rappresentazione di database dispone di una relazione di mapping uno-a-uno con <xref:Microsoft.AnalysisServices.Database> e non sono richiesti altri oggetti AMO principali. È importante notare che questo non significa che tutti gli oggetti contenuti nell'oggetto di database AMO possano essere utilizzati nella modellazione.  
  
 Visualizzare [rappresentazione di Database&#40;tabulare&#41; ](database-representation-tabular.md) per una spiegazione dettagliata su come creare e modificare la rappresentazione del database.  
  
## <a name="connection-representation"></a>Rappresentazione di una connessione  
 Una connessione stabilisce la relazione tra i dati da includere in una soluzione di modello tabulare e il modello stesso. In termini di oggetti AMO, una connessione dispone di una relazione di mapping uno-a-uno con <xref:Microsoft.AnalysisServices.DataSource> e non sono richiesti altri oggetti AMO principali. È importante notare che questo non significa che tutti gli oggetti contenuti nell'oggetto datasource AMO possano essere utilizzati nella modellazione.  
  
 Visualizzare [rappresentazione di una connessione &#40;tabulare&#41; ](connection-representation-tabular.md) per una spiegazione dettagliata su come creare e modificare la rappresentazione dell'origine dati.  
  
## <a name="table-representation"></a>Rappresentazione della tabella  
 Le tabelle sono oggetti di database che contengono tutti i dati presenti nel database. In termini di oggetti AMO, una tabella dispone di una relazione di mapping uno-a-molti. Una tabella è rappresentata dall'utilizzo degli oggetti AMO <xref:Microsoft.AnalysisServices.DataSourceView>, <xref:Microsoft.AnalysisServices.Dimension>, <xref:Microsoft.AnalysisServices.Cube>, <xref:Microsoft.AnalysisServices.CubeDimension>, <xref:Microsoft.AnalysisServices.MeasureGroup> e <xref:Microsoft.AnalysisServices.Partition>, che sono gli oggetti principali richiesti. È tuttavia importante notare che ciò non significa che tutti gli oggetti contenuti negli oggetti AMO precedentemente citati possano essere utilizzati nella modellazione.  
  
 Visualizzare [rappresentazione delle tabelle &#40;tabulare&#41; ](tables-representation-tabular.md) per una spiegazione dettagliata su come creare e modificare la rappresentazione della tabella.  
  
### <a name="calculated-column-representation"></a>Rappresentazione della colonna calcolata  
 Le colonne calcolate sono espressioni valutate che generano una colonna in una tabella, dove viene calcolato e archiviato un nuovo valore per ogni riga nella tabella. In termini di oggetti AMO, una colonna calcolata dispone di una relazione di mapping uno-a-molti. Una colonna calcolata è rappresentata dall'utilizzo degli oggetti AMO <xref:Microsoft.AnalysisServices.Dimension> e <xref:Microsoft.AnalysisServices.MeasureGroup>, che sono gli oggetti principali richiesti. È importante notare che questo non significa che tutti gli oggetti contenuti negli oggetti AMO citati in precedenza possano essere utilizzati nella modellazione.  
  
 Visualizzare [rappresentazione della colonna calcolata &#40;tabulare&#41; ](tables-calculated-column-representation.md) per una spiegazione dettagliata su come creare e modificare la rappresentazione della colonna calcolata.  
  
### <a name="calculated-measure-representation"></a>Rappresentazione della misura calcolata  
 Le misure calcolate sono espressioni archiviate che vengono valutate su richiesta una volta distribuito il modello. In termini di oggetti AMO, una misura calcolata dispone di una relazione di mapping uno-a-molti. Una colonna calcolata è rappresentata dall'utilizzo degli oggetti AMO <xref:Microsoft.AnalysisServices.MdxScript.Commands%2A> e <xref:Microsoft.AnalysisServices.MdxScript.CalculationProperties%2A>, che sono gli oggetti principali richiesti. È importante notare che questo non significa che tutti gli oggetti contenuti negli oggetti AMO citati in precedenza possano essere utilizzati nella modellazione.  
  
> [!NOTE]  
>  Gli oggetti <xref:Microsoft.AnalysisServices.Measure> non dispongono di relazione con le misure calcolate dei modelli tabulari e non sono supportati nei modelli tabulari.  
  
 Visualizzare [rappresentazione della misura calcolata &#40;tabulare&#41; ](tables-calculated-measure-representation.md) per una spiegazione dettagliata su come creare e modificare la rappresentazione della misura calcolata.  
  
### <a name="hierarchy-representation"></a>Rappresentazione della gerarchia  
 Le gerarchie sono un meccanismo che consente all'utente finale un'esecuzione più efficace di analisi drill-up e drill-down. In termini di oggetti AMO, una rappresentazione di gerarchia dispone di una relazione di mapping uno-a-uno con <xref:Microsoft.AnalysisServices.Hierarchy> e non sono richiesti altri oggetti AMO principali. È importante notare che questo non significa che tutti gli oggetti contenuti nell'oggetto di database AMO possano essere utilizzati nella modellazione tabulare.  
  
 Visualizzare [rappresentazione della gerarchia &#40;tabulare&#41; ](tables-hierarchy-representation.md) per una spiegazione dettagliata su come creare e modificare la rappresentazione della gerarchia.  
  
### <a name="key-performance-indicator--kpi--representation"></a>Prestazioni chiave KPI--rappresentazione dell'indicatore  
 Un indicatore KPI viene utilizzato per misurare le prestazioni di un valore, definito mediante una misura di base, rispetto a un valore di destinazione. In termini di oggetti AMO, una rappresentazione KPI dispone di una relazione di mapping uno-a-molti. Un indicatore KPI è rappresentato dall'utilizzo degli oggetti AMO <xref:Microsoft.AnalysisServices.MdxScript.Commands%2A> e <xref:Microsoft.AnalysisServices.MdxScript.CalculationProperties%2A>, che sono gli oggetti principali richiesti.  È importante notare che questo non significa che tutti gli oggetti contenuti negli oggetti AMO citati in precedenza possano essere utilizzati nella modellazione.  
  
> [!NOTE]  
>  Un'altra distinzione importante è che gli oggetti <xref:Microsoft.AnalysisServices.Kpi> non dispongono di relazione con gli indicatori KPI nei modelli tabulari e non sono di fatto supportati nei modelli tabulari stessi.  
  
 Visualizzare [rappresentazione dell'indicatore di prestazioni chiave &#40;tabulare&#41; ](tables-key-performance-indicator-representation.md) per una spiegazione dettagliata su come creare e modificare la rappresentazione di indicatore KPI.  
  
### <a name="partition-representation"></a>Rappresentazione di una partizione  
 Ai fini operativi, una tabella può essere divisa in diversi subset di righe che, se combinati insieme, formano la tabella. Ognuno di tali subset è una partizione della tabella. In termini di oggetti AMO, una rappresentazione di partizione dispone di una relazione di mapping uno-a-uno con <xref:Microsoft.AnalysisServices.Partition> e non sono richiesti altri oggetti AMO principali. È importante notare che questo non significa che tutti gli oggetti contenuti nell'oggetto di database AMO possano essere utilizzati nella modellazione.  
  
 Visualizzare [rappresentazione della partizione &#40;tabulare&#41; ](tables-partition-representation.md) per una spiegazione dettagliata su come creare e modificare la rappresentazione della partizione.  
  
## <a name="relationship-representation"></a>Rappresentazione di una relazione  
 Una relazione è una connessione tra due tabelle di dati e consente di stabilire in che modo devono essere correlati i dati nelle due tabelle.  
  
 Nei modelli tabulari, più relazioni possono essere definite tra due tabelle. Quando sono definite più relazioni tra due tabelle, se ne può definire solo una come relazione attiva predefinita. Tutte le altre relazioni sono inattive.  
  
 In termini di oggetti AMO, tutte le relazioni inattive dispongono di una rappresentazione di una relazione di mapping uno-a-uno con <xref:Microsoft.AnalysisServices.Relationship> e non sono richiesti altri oggetti AMO principali. Per la relazione attiva, esistono altri requisiti e il mapping a <xref:Microsoft.AnalysisServices.ReferenceMeasureGroupDimension> è obbligatorio. È importante notare che questo non significa che tutti gli oggetti contenuti nella relazione AMO o nell'oggetto referenceMeasureGroupDimension possano essere utilizzati nella modellazione.  
  
 Visualizzare [rappresentazione della relazione &#40;tabulare&#41; ](relationship-representation-tabular.md) per una spiegazione dettagliata su come creare e modificare la rappresentazione della relazione.  
  
## <a name="perspective-representation"></a>Rappresentazione della prospettiva  
 Una prospettiva è un meccanismo per semplificare o concentrare la modalità. In termini di oggetti AMO, una rappresentazione della relazione dispone di una relazione di mapping uno-a-uno con <xref:Microsoft.AnalysisServices.Perspective> e non sono richiesti altri oggetti AMO principali. È importante notare che questo non significa che tutti gli oggetti contenuti nell'oggetto prospettiva AMO possano essere utilizzati nella modellazione tabulare.  
  
 Visualizzare [rappresentazione della prospettiva &#40;tabulare&#41; ](perspective-representation-tabular.md) per una spiegazione dettagliata su come creare e modificare la rappresentazione della prospettiva.  
  
> [!WARNING]  
>  Le prospettive non sono un meccanismo di sicurezza. L'utente può comunque accedere agli oggetti esterni alla prospettiva tramite altre interfacce.  
  
  
