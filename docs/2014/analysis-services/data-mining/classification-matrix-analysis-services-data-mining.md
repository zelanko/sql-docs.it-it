---
title: Matrice di classificazione (Analysis Services - Data Mining) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining models [Analysis Services], validating
- validating data mining models
- viewing mining accuracy
- displaying mining accuracy
- confusion matrix [data mining]
- classification matrix [Analysis Services]
- accuracy testing [data mining]
ms.assetid: 5c12f202-2ed9-41fa-bee2-0f7ab3ff058a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7949729f3ebee87d06e5e591c46513c111b70016
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2018
ms.locfileid: "53358893"
---
# <a name="classification-matrix-analysis-services---data-mining"></a>Matrice di classificazione (Analysis Services - Data mining)
  Una *matrice di classificazione* consente di ordinare tutti i case del modello in categorie, determinando se il valore stimato corrisponde a quello effettivo. Vengono calcolati tutti i case di ogni categoria, quindi vengono visualizzati i totali nella matrice. La matrice di classificazione è uno strumento standard per la valutazione di modelli statistici, talvolta definita *matrice di confusione*.  
  
 Nel grafico creato quando si sceglie l'opzione **Matrice di classificazione** è possibile confrontare i valori effettivi con quelli stimati per ogni stato stimato specificato. Le righe nella matrice rappresentano i valori stimati per il modello, mentre le colonne rappresentano i valori effettivi. Le categorie usate nell'analisi sono *falso positivo*, *vero positivo*, *falso negativo*e *vero negativo*.  
  
 Una matrice di classificazione è uno strumento importante per valutare i risultati di una stima in quanto facilita la comprensione e la spiegazione degli effetti delle stime errate. Visualizzando la quantità e le percentuali in ogni cella di questa matrice, è possibile vedere con quale frequenza vengano eseguite stime accurate da parte del modello.  
  
 In questa sezione viene illustrato come creare una matrice di classificazione e come interpretarne i risultati.  
  
## <a name="understanding-the-classification-matrix"></a>Informazioni sulla matrice di classificazione  
 Si consideri il modello creato durante l'Esercitazione di base sul data mining. Il modello [TM_DecisionTree] consente di semplificare la creazione di una campagna di mailing diretto e può essere utilizzato per eseguire una stima dei clienti che con maggiore probabilità acquisteranno una bicicletta. Per testare l'utilità prevista di questo modello, è necessario utilizzare un set di dati per il quale i valori dell'attributo, [Bike Buyer], sono già noti. A tale scopo, viene in genere utilizzato il set di dati di testing riservato durante la creazione della struttura di data mining utilizzata per il training del modello.  
  
 È possibile ottenere solo due risultati, ovvero sì (è probabile che il cliente acquisti una bicicletta) e no (è probabile che il cliente non acquisti una bicicletta). Pertanto, la matrice di classificazione risultante è relativamente semplice.  
  
## <a name="interpreting-the-results"></a>Interpretazione dei risultati  
 Nella tabella seguente viene mostrata la matrice di classificazione per il modello TM_DecisionTree. Per questo attributo stimabile, 0 indica No mentre 1 indica Sì.  
  
|Stimati|0 (valore effettivo)|1 (valore effettivo)|  
|---------------|------------------|------------------|  
|0|362|144|  
|1|121|373|  
  
 La prima cella dei risultati, in cui è contenuto il valore 362, indica il numero di *veri positivi* per il valore 0. Poiché 0 significa che il cliente non ha acquistato una bicicletta, la statistica indica che il modello è stato in grado di eseguire una stima corretta per il valore relativo ai mancati acquirenti di biciclette in 362 case.  
  
 La cella immediatamente sottostante, che contiene il valore 121, indica il numero di *falsi positivi*, o il numero di volte in cui il modello ha erroneamente previsto che alcuni clienti avrebbero acquistato una bicicletta.  
  
 La cella che contiene il valore 144 indica il numero di *falsi positivi* per il valore 1. Poiché 1 significa che il cliente ha acquistato una bicicletta, questa statistica indica che in 144 case il modello ha stimato erroneamente che alcuni clienti non avrebbero acquistato una bicicletta.  
  
 La cella che contiene il valore 373, infine, indica il numero di veri positivi per il valore di destinazione 1. In altri termini, in 373 case il modello ha eseguito una stima corretta, prevedendo che alcuni clienti avrebbero acquistato una bicicletta.  
  
 Sommando i valori nelle celle adiacenti in diagonale, è possibile determinare l'accuratezza complessiva del modello. Una diagonale indica il numero complessivo di stime accurate, mentre l'altra indica il numero totale di stime errate.  
  
### <a name="using-multiple-predictable-values"></a>Utilizzo di più valori stimabili  
 Il case [Bike Buyer] è particolarmente semplice da interpretare perché vi sono solo due valori possibili. Quando l'attributo stimabile ha più valori possibili, la matrice di classificazione aggiunge una nuova colonna per ogni valore effettivo possibile, quindi conteggia il numero di corrispondenze per ciascun valore stimato. Nella tabella seguente vengono illustrati i risultati di un modello diverso in cui sono possibili tre valori: 0, 1 e 2.  
  
|Stimati|0 (valore effettivo)|1 (valore effettivo)|2 (valore effettivo)|  
|---------------|------------------|------------------|------------------|  
|0|111|3|5|  
|1|2|123|17|  
|2|19|0|20|  
  
 Benché l'aggiunta di più colonne renda più complesso l'aspetto del report, il dettaglio aggiuntivo può rivelarsi molto utile quando si desidera valutare il costo cumulativo di una stima errata. Per creare somme sulle diagonali o confrontare i risultati per diverse combinazioni di righe, è possibile fare clic sul pulsante **Copia** disponibile nella scheda **Matrice di classificazione** e incollare il report in Excel. In alternativa, è possibile usare un client, ad esempio il client di data mining per Excel, che supporta [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versioni successive, per creare direttamente in Excel un report di classificazione contenente sia conteggi sia percentuali. Per altre informazioni, vedere [SQL Server Data Mining](https://go.microsoft.com/fwlink/?LinkID=77733).  
  
## <a name="restrictions-on-the-classification-matrix"></a>Restrizioni sulla matrice di classificazione  
 Una matrice di classificazione può essere utilizzata solo con attributi stimabili discreti.  
  
 Anche se è possibile aggiungere più modelli quando si selezionano modelli nella scheda **Selezione input** della finestra di progettazione **Grafico accuratezza modello di data mining** , nella scheda **Matrice di classificazione** verrà visualizzata una matrice separata per ogni modello.  
  
## <a name="related-content"></a>Contenuto correlato  
 Negli argomenti seguenti sono contenute ulteriori informazioni su come sia possibile compilare e utilizzare le matrici di classificazione ed altri grafici.  
  
|Argomento|Collegamenti|  
|------------|-----------|  
|Viene fornita una procedura dettagliata relativa alla creazione di un grafico di accuratezza per il modello Targeted Mailing.|[Esercitazione di base sul data mining](../../tutorials/basic-data-mining-tutorial.md)<br /><br /> [Test dell'accuratezza con i grafici di accuratezza &#40;Esercitazione di base sul data mining&#41;](../../tutorials/testing-accuracy-with-lift-charts-basic-data-mining-tutorial.md)|  
|Vengono illustrati i tipi di grafici correlati.|[Grafico di accuratezza &#40;Analysis Services - Data mining&#41;](lift-chart-analysis-services-data-mining.md)<br /><br /> [Grafico dei profitti &#40;Analysis Services - Data mining&#41;](profit-chart-analysis-services-data-mining.md)<br /><br /> [Grafico a dispersione &#40;Analysis Services - Data mining&#41;](scatter-plot-analysis-services-data-mining.md)|  
|Vengono descritti gli utilizzi della convalida incrociata per modelli e strutture di data mining.|[Convalida incrociata &#40;Analysis Services - Data mining&#41;](cross-validation-analysis-services-data-mining.md)|  
|Vengono descritti i passaggi per la creazione di grafici di accuratezza e di altri grafici simili.|[Attività e procedure di test e convalida &#40;data mining&#41;](testing-and-validation-tasks-and-how-tos-data-mining.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Test e convalida &#40;Data mining&#41;](testing-and-validation-data-mining.md)  
  
  
