---
title: Area dati Tablix (Generatore report e SSRS) | Microsoft Docs
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 99f83b32-4b86-4d40-973c-9a328d23ac8b
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: b80383fee9ede0fece7ed2fd16e95bdf63592b04
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65574493"
---
# <a name="tablix-data-region-report-builder-and-ssrs"></a>Area dati Tablix (Generatore report e SSRS)
  In [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)], l'area dati Tablix è un elemento del report di layout generalizzato in cui i dati del report impaginati vengono visualizzati in celle suddivise in righe e colonne. I dati del report possono essere dati dettaglio recuperati direttamente dall'origine dati o dati dettaglio aggregati organizzati in gruppi specificati dall'utente. Ogni cella della Tablix può contenere qualsiasi elemento del report, ad esempio una casella di testo, un'immagine o un'altra area dati, ad esempio un grafico, un misuratore o un'area Tablix. Per aggiungere più elementi del report a una cella, aggiungere innanzitutto un rettangolo da utilizzare come contenitore. Aggiungere elementi del report al rettangolo.  
  
 Le aree dati di tabella, matrice ed elenco sono rappresentate sulla barra multifunzione mediante modelli per l'area dati Tablix sottostante. Quando si aggiunge uno di questi modelli a un report, in realtà si aggiunge un'area dati Tablix ottimizzata per uno specifico layout dei dati. Per impostazione predefinita, un modello di tabella visualizza i dati dettaglio in un layout di griglia, una matrice visualizza i dati di gruppo in un layout di griglia e un elenco visualizza i dati dettaglio in un layout in formato libero.  
  
 Per impostazione predefinita, in ogni cella Tablix di una tabella o matrice è contenuta una casella di testo. La cella di un elenco contiene un rettangolo. È possibile sostituire un elemento del report predefinito con un altro elemento del report, ad esempio un'immagine.  
  
 Quando si definiscono gruppi di una tabella, una matrice o un elenco, Generatore report e Progettazione report aggiungono righe e colonne all'area dati Tablix nella quale visualizzare dati raggruppati.  
  
 Per comprendere l'area dati Tablix, è utile essere a conoscenza di quanto segue:  
  
*   Differenza tra dati dettaglio e dati raggruppati.  
  
*   I gruppi, ovvero elementi organizzati come membri di gerarchie di gruppi e disposti sull'asse orizzontale come gruppi di righe e sull'asse verticale come gruppi di colonne.  
  
*  Funzione delle celle della Tablix nelle quattro aree di un'area dati Tablix, ovvero il corpo, le intestazioni dei gruppi di righe, le intestazioni dei gruppi di colonne e l'angolo.  
  
*  Colonne e righe statiche e dinamiche e rispettive relazioni con i gruppi.  
  
 Questo articolo chiarisce questi concetti per spiegare la struttura che Generatore report e Progettazione report aggiungono quando si aggiungono modelli e si creano gruppi, di modo che possa essere modificata in base a esigenze specifiche. Generatore report e Progettazione report forniscono più indicatori visivi per agevolare l'identificazione della struttura dell'area dati Tablix. Per altre informazioni, vedere [Celle, righe e colonne dell'area dati Tablix &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="understanding-detail-and-grouped-data"></a>Informazioni su dati dettaglio e raggruppati  
 I dati dettaglio sono tutti i dati provenienti da un set di dati del report e restituiti dall'origine dati. I dati dettaglio sono essenzialmente quelli visualizzati nel riquadro Risultati di Progettazione query quando si esegue una query del set di dati. I dati dettaglio effettivi includono campi calcolati creati dall'utente e limitati da filtri impostati sul set di dati, sull'area dati e sul gruppo dettagli. Per visualizzare i dati dettaglio in una riga di dettaglio è necessario specificare un'espressione semplice quale [Quantity]. Durante l'esecuzione del report, la riga di dettaglio viene ripetuta una volta per ogni riga dei risultati della query.  
  
 I dati raggruppati sono dati dettaglio organizzati in base a un valore specificato nella definizione di gruppo, ad esempio [SalesOrder]. Per visualizzare i dati raggruppati in righe e colonne di gruppi è necessario specificare espressioni semplici che aggregano i dati raggruppati, ad esempio [Sum(Quantity)]. Per altre informazioni, vedere [Informazioni sui gruppi &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/understanding-groups-report-builder-and-ssrs.md).  
  
## <a name="understanding-group-hierarchies"></a>Informazioni sulle gerarchie di gruppi  
 I gruppi sono organizzati come membri di gerarchie di gruppi. Le gerarchie dei gruppi di colonne e di righe sono strutture identiche disposte su assi differenti. È possibile immaginare i gruppi di righe come elementi che si espandono verso il basso all'interno della pagina e i gruppi di colonne come elementi che si espandono per tutta l'estensione della pagina.  
  
 Una struttura ad albero rappresenta gruppi di righe e di colonne nidificati caratterizzati da una relazione padre/figlio, ad esempio una categoria contenente alcune sottocategorie. Il gruppo padre è la radice della struttura ad albero, mentre i gruppi figlio ne rappresentano le diramazioni. I gruppi possono anche presentare una relazione indipendente adiacente, come nel caso delle vendite per territorio e delle vendite per anno. In presenza di più gerarchie ad albero non correlate si parla di foresta. In un'area dati Tablix i gruppi di righe e i gruppi di colonne vengono rappresentati ognuno come una foresta indipendente. Per altre informazioni, vedere [Informazioni sui gruppi &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/understanding-groups-report-builder-and-ssrs.md).  
  
## <a name="understanding-tablix-data-region-areas"></a>Informazioni sulle aree dell'area dati Tablix  
 Un'area dati Tablix può includere quattro possibili aree per le celle, ovvero l'angolo, la gerarchia dei gruppi di righe, la gerarchia dei gruppi di colonne o il corpo della Tablix. Il corpo della Tablix è sempre presente, mentre le altre aree sono facoltative.  
  
 Nelle celle dell'area del corpo della Tablix sono visualizzati dati dettaglio e dati di gruppo.  
  
 Le celle dell'area Gruppi di righe vengono create automaticamente quando si crea un gruppo di righe e rappresentano celle di intestazione dei gruppi di righe che visualizzano per impostazione predefinita i valori delle istanze dei gruppi di righe. Se ad esempio si specifica un raggruppamento per [SalesOrder], i valori delle istanze di gruppo sono i singoli ordini di vendita in base ai quali si esegue il raggruppamento.  
  
 Le celle dell'area Gruppi di colonne vengono create automaticamente quando si crea un gruppo di colonne e rappresentano celle di intestazione dei gruppi di colonne che visualizzano per impostazione predefinita i valori delle istanze dei gruppi di colonne. Se ad esempio si specifica un raggruppamento per [Year], i valori delle istanze di gruppo sono i singoli anni in base ai quali si esegue il raggruppamento.  
  
 Le celle nell'area dell'angolo della Tablix vengono create automaticamente quando sono definiti sia gruppi di righe che gruppi di colonne. Le celle incluse in questa area possono visualizzare etichette o possono essere unite per creare un titolo.  
  
 Per altre informazioni, vedere [Aree dell'area dati Tablix &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/tablix-data-region-areas-report-builder-and-ssrs.md).  
  
## <a name="understanding-static-and-dynamic-rows-and-columns"></a>Informazioni sulle righe e sulle colonne statiche e dinamiche  
 In un'area dati Tablix le celle sono organizzate in righe e colonne associate a gruppi. Le strutture dei gruppi di righe e colonne sono identiche. In questo esempio vengono utilizzati gruppi di righe, ma è possibile applicare gli stessi concetti ai gruppi di colonne.  
  
 Una riga può essere statica o dinamica. Una riga statica non è associata a un gruppo. Quando il report è in esecuzione, il rendering di una riga statica viene eseguito una sola volta. Le intestazioni e i piè di pagina di tabella sono righe statiche. Nelle righe statiche vengono visualizzate le etichette e i totali. L'ambito delle celle di una riga statica è rappresentato dall'area dati.  
  
 Una riga dinamica è associata a uno o più gruppi. Il rendering di una riga dinamica viene eseguito una volta per ogni valore di gruppo univoco del gruppo più interno. L'ambito delle celle di una riga dinamica è rappresentato dal gruppo di righe e dal gruppo di colonne più interni al quale appartiene la cella.  
  
 Le righe di dettaglio dinamiche vengono associate al gruppo Dettagli creato automaticamente quando si aggiunge una tabella o un elenco all'area di progettazione. Per definizione, il gruppo Dettagli è il gruppo più interno di un'area dati Tablix. Nelle celle delle righe di dettaglio vengono visualizzati i dati dettaglio.  
  
 Le righe dei gruppi dinamici vengono create quando si aggiunge un gruppo di righe o un gruppo di colonne a un'area dati Tablix esistente. Nelle celle delle righe dei gruppi dinamici vengono visualizzati i valori aggregati per l'ambito predefinito.  
  
 La caratteristica Aggiungi totale crea automaticamente una riga all'esterno del gruppo corrente nella quale visualizzare i valori che hanno come ambito il gruppo. È anche possibile aggiungere righe statiche e dinamiche manualmente. Gli indicatori visivi consentono di distinguere le righe statiche da quelle dinamiche. Per altre informazioni, vedere [Celle, righe e colonne dell'area dati Tablix &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Collegamento di più aree dati allo stesso set di dati &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/linking-multiple-data-regions-to-the-same-dataset-report-builder-and-ssrs.md)   
 [Controllo della visualizzazione dell'area dati Tablix in una pagina del report &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/controlling-the-tablix-data-region-display-on-a-report-page.md)   
 [Esplorazione della flessibilità di un'area dati Tablix &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/exploring-the-flexibility-of-a-tablix-data-region-report-builder-and-ssrs.md)   
 [Tabelle, matrici ed elenchi &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
