---
title: Aree dell'area dati Tablix (Generatore report e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: f6c13407-2887-4287-9396-a58dba619d9b
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 21b92fe6ab723b9e519b8828f9adcd4e67dad2e4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62720267"
---
# <a name="tablix-data-region-areas-report-builder-and-ssrs"></a>Aree dell'area dati Tablix (Generatore report e SSRS)
  Un'area dati Tablix può includere quattro aree contenenti le celle della Tablix, ovvero l'angolo, l'area dei gruppi di righe, l'area dei gruppi di colonne e il corpo. Le celle di ogni area presentano una funzione distinta. L'aggiunta di celle all'area del corpo della Tablix consente la visualizzazione di dati dettaglio e dati raggruppati. Quando si crea un gruppo, Progettazione report e Generatore report consentono di aggiungere celle all'area del gruppo di righe o del gruppo di colonne per visualizzare i valori delle istanze del gruppo. Consentono inoltre di creare celle d'angolo della Tablix quando sono presenti gruppi di righe e gruppi di colonne.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
 Nell'area di progettazione le linee tratteggiate indicano le quattro aree di un'area dati Tablix selezionata. Nella figura seguente sono mostrate le aree di una Tablix con gruppi di righe nidificati in base a categoria e sottocategoria, gruppi di colonne nidificati in base a geografia e paese/regione e un gruppo di colonne adiacenti basato sull'anno.  
  
 ![Tablix data region areas](../media/rs-tablixareas.gif "Tablix data region areas")  
  
 Nell'elenco seguente vengono descritte le diverse aree.  
  
-   **Area dell'angolo della Tablix**. (Facoltativo) Un angolo della Tablix si trova nell'angolo superiore sinistro o nell'angolo superiore destro nel caso dei layout da destra a sinistra. Quest'area viene creata automaticamente quando si aggiungono gruppi di righe e gruppi di colonne a un'area dati Tablix. In tale area è possibile unire le celle e aggiungere un'etichetta o incorporare un altro elemento del report. Nella figura le celle unite dell'angolo presentano l'etichetta Sales by Area and Year.  
  
-   **Area dei gruppi di colonne della Tablix**. (Facoltativo) I gruppi di colonne della Tablix si trovano nell'angolo superiore destro o nell'angolo superiore sinistro nel caso dei layout da destra a sinistra. Quest'area viene creata automaticamente quando si aggiunge un gruppo di colonne. Le celle di tale area rappresentano i membri della gerarchia di gruppi di colonne e contengono i valori delle istanze dei gruppi. Nella figura le celle in cui vengono visualizzati [Geography] e [CountryRegion] sono gruppi di colonne nidificati, mentre la cella in cui viene visualizzato [Year] è un gruppo di colonne adiacente. Nella colonna [Total] vengono visualizzati i totali aggregati in ogni riga.  
  
-   **Area dei gruppi di righe della Tablix**. (Facoltativo) I gruppi di righe della Tablix si trovano nell'angolo inferiore sinistro o nell'angolo inferiore destro nel caso dei layout da destra a sinistra. Quest'area viene creata automaticamente quando si aggiunge un gruppo di righe. Le celle di tale area rappresentano i membri della gerarchia di gruppi di righe e contengono i valori delle istanze dei gruppi. Nella figura le celle in cui vengono visualizzati [Category] e [Subcat] sono gruppi di righe nidificati. La riga Total al di sotto di Subcat si ripete con ogni gruppo di categorie per mostrare i subtotali aggregati di ogni colonna. Nella riga del totale complessivo sono mostrati i totali di tutte le categorie.  
  
-   **Area del corpo della Tablix**. Il corpo della Tablix si trova nell'angolo inferiore destro o nell'angolo inferiore sinistro nel caso di layout da destra a sinistra. Nel corpo della Tablix sono visualizzati dati dettaglio e dati raggruppati. In questo esempio vengono utilizzati solo dati aggregati. L'ambito dell'espressione è determinato dai gruppi più interni ai quali appartiene la casella di testo. Le celle nel corpo della Tablix contengono dati dettaglio quando sono membri di una riga di dettaglio e rappresentano dati di aggregazione quando sono membri di una riga o di una colonna associata a un gruppo. Per impostazione predefinita, le celle di una riga o di una colonna di gruppo che contengono espressioni semplici prive di funzioni di aggregazione restituiscono il primo valore nel gruppo. Nella figura le celle contengono i totali di aggregazione per i totali delle righe di tutti gli ordini di vendita.  
  
 Quando il report viene eseguito, i gruppi di colonne si espandono verso destra o verso sinistra se la proprietà Direction dell'area dati Tablix è impostata su RTL, per un numero di colonne pari ai valori univoci di un'espressione di raggruppamento. Le righe dinamiche si espandono verso la parte inferiore della pagina. Per altre informazioni, vedere [Celle, righe e colonne dell'area dati Tablix &#40;Generatore report e SSRS&#41;](tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md).  
  
 Nella figura seguente viene mostrata l'area dati Tablix nel riquadro Anteprima.  
  
 ![Anteprima, angolo Tablix, gruppi di righe di colonne, corpo](../media/rs-tablixareaspreview.gif "Anteprima, angolo Tablix, gruppi di righe di colonne, corpo")  
  
 Nell'area del gruppo di righe vengono visualizzate due istanze del gruppo di categorie relative a Clothing e Components. Il gruppo di colonne contiene un'istanza del gruppo geografia relativa al Nord America, con due istanze del gruppo paese/regione nidificate per Canada (CA) e Stati Uniti (US). Inoltre, nella colonna adiacente sono visualizzate due istanze del gruppo anno relative a 2003 e 2004. La riga della colonna Total contiene i totali delle righe. Nella riga dei totali che si ripete con il gruppo di categorie sono mostrati i totali delle sottocategorie mentre nella riga del totale complessivo sono visualizzati i totali delle categorie una volta per ogni area dati.  
  
## <a name="see-also"></a>Vedere anche  
 [Elenchi &#40;Generatore report e SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [Esercitazioni su &#40;Generatore Report&#41;](../report-builder-tutorials.md)   
 [Tabelle &#40;Generatore report e SSRS&#41;](tables-report-builder-and-ssrs.md)   
 [Matrici &#40;Generatore report e SSRS&#41;](create-a-matrix-report-builder-and-ssrs.md)   
 [Elenchi &#40;Generatore report e SSRS&#41;](create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)   
 [Area dati Tablix &#40;Generatore report e SSRS&#41;](../tablix-data-region-report-builder-and-ssrs.md)  
  
  
