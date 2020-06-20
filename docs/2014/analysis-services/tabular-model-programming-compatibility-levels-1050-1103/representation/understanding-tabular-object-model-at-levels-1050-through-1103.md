---
title: Informazioni sul modello a oggetti tabulare | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
ms.assetid: 6077b7e8-cb3e-4480-a5de-bb602cf9d69a
author: minewiskan
ms.author: owend
ms.openlocfilehash: ed120bedfd236dcb55780982f0f611368147f813
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84939972"
---
# <a name="understanding-the-tabular-object-model"></a>Informazioni sul modello a oggetti tabulare
  Un modello tabulare è una rappresentazione logica di tabelle, relazioni, gerarchie, prospettive, misure e prestazioni chiave. In questa sezione viene illustrata l'implementazione interna tramite AMO. Vedere [sviluppo con Analysis Management Objects &#40;amo&#41;](https://docs.microsoft.com/bi-reference/amo/developing-with-analysis-management-objects-amo) se prima non è stato usato amo.  
  
 In questo caso si utilizza un approccio discendente, viene prima eseguito il mapping logico agli oggetti AMO per tutti gli oggetti rilevanti nel modello tabulare, quindi viene fornita la spiegazione dell'interazione o del flusso di lavoro necessario. Un esempio di codice sorgente per creare un modello tabulare tramite AMO, Da AMO a tabulare, è disponibile in Codeplex. Nota importante sul codice di questo esempio: il codice viene fornito solo come supporto ai concetti logici illustrati in questo argomento e non deve essere utilizzato in un ambiente di produzione. L'esempio viene fornito senza supporto o garanzia.  
  
## <a name="database-representation"></a>Rappresentazione di un database  
 Un database fornisce l'oggetto contenitore per il modello tabulare. Tutti gli oggetti in un modello tabulare sono contenuti nel database. In termini di oggetti AMO, una rappresentazione di database dispone di una relazione di mapping uno-a-uno con <xref:Microsoft.AnalysisServices.Database> e non sono richiesti altri oggetti AMO principali. È importante notare che questo non significa che tutti gli oggetti contenuti nell'oggetto di database AMO possano essere utilizzati nella modellazione.  
  
 Per una spiegazione dettagliata su come creare e modificare la rappresentazione del database, vedere [rappresentazione del database&#40;&#41;tabulare](database-representation-tabular.md) .  
  
## <a name="connection-representation"></a>Rappresentazione di una connessione  
 Una connessione stabilisce la relazione tra i dati da includere in una soluzione di modello tabulare e il modello stesso. In termini di oggetti AMO, una connessione dispone di una relazione di mapping uno-a-uno con <xref:Microsoft.AnalysisServices.DataSource> e non sono richiesti altri oggetti AMO principali. È importante notare che questo non significa che tutti gli oggetti contenuti nell'oggetto datasource AMO possano essere utilizzati nella modellazione.  
  
 Per una spiegazione dettagliata su come creare e modificare la rappresentazione dell'origine dati, vedere [rappresentazione della connessione &#40;tabulare&#41;](connection-representation-tabular.md) .  
  
## <a name="table-representation"></a>Rappresentazione della tabella  
 Le tabelle sono oggetti di database che contengono tutti i dati presenti nel database. In termini di oggetti AMO, una tabella dispone di una relazione di mapping uno-a-molti. Una tabella è rappresentata dall'utilizzo degli oggetti AMO <xref:Microsoft.AnalysisServices.DataSourceView>, <xref:Microsoft.AnalysisServices.Dimension>, <xref:Microsoft.AnalysisServices.Cube>, <xref:Microsoft.AnalysisServices.CubeDimension>, <xref:Microsoft.AnalysisServices.MeasureGroup> e <xref:Microsoft.AnalysisServices.Partition>, che sono gli oggetti principali richiesti. È tuttavia importante notare che ciò non significa che tutti gli oggetti contenuti negli oggetti AMO precedentemente citati possano essere utilizzati nella modellazione.  
  
 Per una spiegazione dettagliata su come creare e modificare la rappresentazione della tabella, vedere la pagina relativa alla [rappresentazione delle tabelle &#40;&#41;tabulare](tables-representation-tabular.md) .  
  
### <a name="calculated-column-representation"></a>Rappresentazione della colonna calcolata  
 Le colonne calcolate sono espressioni valutate che generano una colonna in una tabella, dove viene calcolato e archiviato un nuovo valore per ogni riga nella tabella. In termini di oggetti AMO, una colonna calcolata dispone di una relazione di mapping uno-a-molti. Una colonna calcolata è rappresentata dall'utilizzo degli oggetti AMO <xref:Microsoft.AnalysisServices.Dimension> e <xref:Microsoft.AnalysisServices.MeasureGroup>, che sono gli oggetti principali richiesti. È importante notare che questo non significa che tutti gli oggetti contenuti negli oggetti AMO citati in precedenza possano essere utilizzati nella modellazione.  
  
 Per una spiegazione dettagliata su come creare e modificare la rappresentazione della colonna calcolata, vedere [rappresentazione della colonna calcolata &#40;&#41;tabulare](tables-calculated-column-representation.md) .  
  
### <a name="calculated-measure-representation"></a>Rappresentazione della misura calcolata  
 Le misure calcolate sono espressioni archiviate che vengono valutate su richiesta una volta distribuito il modello. In termini di oggetti AMO, una misura calcolata dispone di una relazione di mapping uno-a-molti. Una colonna calcolata è rappresentata dall'utilizzo degli oggetti AMO <xref:Microsoft.AnalysisServices.MdxScript.Commands%2A> e <xref:Microsoft.AnalysisServices.MdxScript.CalculationProperties%2A>, che sono gli oggetti principali richiesti. È importante notare che questo non significa che tutti gli oggetti contenuti negli oggetti AMO citati in precedenza possano essere utilizzati nella modellazione.  
  
> [!NOTE]  
>  Gli oggetti <xref:Microsoft.AnalysisServices.Measure> non dispongono di relazione con le misure calcolate dei modelli tabulari e non sono supportati nei modelli tabulari.  
  
 Per una spiegazione dettagliata su come creare e modificare la rappresentazione della misura calcolata, vedere [rappresentazione della misura calcolata &#40;tabulare&#41;](tables-calculated-measure-representation.md) .  
  
### <a name="hierarchy-representation"></a>Rappresentazione della gerarchia  
 Le gerarchie sono un meccanismo che consente all'utente finale un'esecuzione più efficace di analisi drill-up e drill-down. In termini di oggetti AMO, una rappresentazione di gerarchia dispone di una relazione di mapping uno-a-uno con <xref:Microsoft.AnalysisServices.Hierarchy> e non sono richiesti altri oggetti AMO principali. È importante notare che questo non significa che tutti gli oggetti contenuti nell'oggetto di database AMO possano essere utilizzati nella modellazione tabulare.  
  
 Per una spiegazione dettagliata su come creare e modificare la rappresentazione della gerarchia, vedere [rappresentazione della gerarchia &#40;&#41;tabulare](tables-hierarchy-representation.md) .  
  
### <a name="key-performance-indicator--kpi--representation"></a>Indicatore di prestazioni chiave-KPI-rappresentazione  
 Un indicatore KPI viene utilizzato per misurare le prestazioni di un valore, definito mediante una misura di base, rispetto a un valore di destinazione. In termini di oggetti AMO, una rappresentazione KPI dispone di una relazione di mapping uno-a-molti. Un indicatore KPI è rappresentato dall'utilizzo degli oggetti AMO <xref:Microsoft.AnalysisServices.MdxScript.Commands%2A> e <xref:Microsoft.AnalysisServices.MdxScript.CalculationProperties%2A>, che sono gli oggetti principali richiesti.  È importante notare che questo non significa che tutti gli oggetti contenuti negli oggetti AMO citati in precedenza possano essere utilizzati nella modellazione.  
  
> [!NOTE]  
>  Un'altra distinzione importante è che gli oggetti <xref:Microsoft.AnalysisServices.Kpi> non dispongono di relazione con gli indicatori KPI nei modelli tabulari e non sono di fatto supportati nei modelli tabulari stessi.  
  
 Per una spiegazione dettagliata su come creare e modificare la rappresentazione degli indicatori KPI, vedere [rappresentazione dell'indicatore di prestazioni chiave &#40;&#41;tabulare](tables-key-performance-indicator-representation.md) .  
  
### <a name="partition-representation"></a>Rappresentazione di una partizione  
 Ai fini operativi, una tabella può essere divisa in diversi subset di righe che, se combinati insieme, formano la tabella. Ognuno di tali subset è una partizione della tabella. In termini di oggetti AMO, una rappresentazione di partizione dispone di una relazione di mapping uno-a-uno con <xref:Microsoft.AnalysisServices.Partition> e non sono richiesti altri oggetti AMO principali. È importante notare che questo non significa che tutti gli oggetti contenuti nell'oggetto di database AMO possano essere utilizzati nella modellazione.  
  
 Per una spiegazione dettagliata su come creare e modificare la rappresentazione della partizione, vedere [rappresentazione della partizione &#40;tabulare&#41;](tables-partition-representation.md) .  
  
## <a name="relationship-representation"></a>Rappresentazione di una relazione  
 Una relazione è una connessione tra due tabelle di dati e consente di stabilire in che modo devono essere correlati i dati nelle due tabelle.  
  
 Nei modelli tabulari, più relazioni possono essere definite tra due tabelle. Quando sono definite più relazioni tra due tabelle, se ne può definire solo una come relazione attiva predefinita. Tutte le altre relazioni sono inattive.  
  
 In termini di oggetti AMO, tutte le relazioni inattive dispongono di una rappresentazione di una relazione di mapping uno-a-uno con <xref:Microsoft.AnalysisServices.Relationship> e non sono richiesti altri oggetti AMO principali. Per la relazione attiva, esistono altri requisiti e il mapping a <xref:Microsoft.AnalysisServices.ReferenceMeasureGroupDimension> è obbligatorio. È importante notare che questo non significa che tutti gli oggetti contenuti nella relazione AMO o nell'oggetto referenceMeasureGroupDimension possano essere utilizzati nella modellazione.  
  
 Per una spiegazione dettagliata su come creare e modificare la rappresentazione della relazione, vedere [rappresentazione di relazioni &#40;tabulare&#41;](relationship-representation-tabular.md) .  
  
## <a name="perspective-representation"></a>Rappresentazione della prospettiva  
 Una prospettiva è un meccanismo per semplificare o concentrare la modalità. In termini di oggetti AMO, una rappresentazione della relazione dispone di una relazione di mapping uno-a-uno con <xref:Microsoft.AnalysisServices.Perspective> e non sono richiesti altri oggetti AMO principali. È importante notare che questo non significa che tutti gli oggetti contenuti nell'oggetto prospettiva AMO possano essere utilizzati nella modellazione tabulare.  
  
 Per una spiegazione dettagliata su come creare e modificare la rappresentazione della prospettiva, vedere [rappresentazione prospettica &#40;&#41;tabulare](perspective-representation-tabular.md) .  
  
> [!WARNING]  
>  Le prospettive non sono un meccanismo di sicurezza. L'utente può comunque accedere agli oggetti esterni alla prospettiva tramite altre interfacce.  
  
  
