---
title: Procedura guidata stima (componenti aggiuntivi Data mining per Excel) | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data modeling [data mining]
- estimation
ms.assetid: 7f2b1d5f-c9b3-4939-b35a-34ae099af15f
author: minewiskan
ms.author: owend
ms.openlocfilehash: 2706dae37c1dc303aa6708fe1f7387a39835e4d5
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/08/2020
ms.locfileid: "84528369"
---
# <a name="estimate-wizard-data-mining-add-ins-for-excel"></a>Procedura guidata Stima (componenti aggiuntivi Data mining per Excel)
  ![Procedura guidata Stima sulla barra multifunzione Data mining](media/dmc-estimate.gif "Procedura guidata Stima sulla barra multifunzione Data mining")  
  
 La procedura guidata **Valutazione** consente di creare un modello di valutazione. Un modello di valutazione consente di estrarre modelli dai dati e di utilizzarli per stimare i fattori che influiscono sui risultati.  
  
 La valutazione viene utilizzata per stimare i risultati numerici. Se, ad esempio, la colonna di destinazione contiene il numero dei diplomati nelle scuole, espresso come percentuale, è possibile analizzare i fattori che possono determinare un aumento o una riduzione di questo numero, ad esempio il numero di studenti per scuola, il rapporto numerico tra studenti e insegnanti e il numero di insegnanti.  
  
## <a name="using-the-estimate-data-wizard"></a>Utilizzo della procedura guidata Valutazione dati  
  
1.  Sulla barra multifunzione **data mining** fare clic su **stima**.  
  
2.  Nella finestra di dialogo **selezione dati di origine** selezionare i dati di origine da utilizzare. È possibile utilizzare i dati in una **tabella**di Excel, un **intervallo di dati**di Excel o da un' **origine dati esterna**.  
  
     Se si utilizza un'origine dati esterna, è possibile creare viste o query personalizzate e salvarle come origine dati di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
3.  Nella finestra di dialogo **stima** selezionare la **colonna da analizzare**.  
  
     La colonna di destinazione deve contenere dati numerici continui.  
  
4.  Selezionare le colonne da utilizzare come input selezionando la casella di controllo **colonne di input** .  
  
     Queste colonne verranno utilizzate per creare i modelli. Eliminare dall'analisi tutte le colonne di scarsa utilità, ad esempio i numeri di ID o le colonne che contengono dati irrilevanti.  
  
5.  La procedura guidata **stima** consente di selezionare l'algoritmo ottimale per il set di dati. Tuttavia, è possibile fare clic su **parametri** per aprire la finestra di dialogo **parametri algoritmo** e impostare le opzioni avanzate.  
  
6.  Se i dati sono numerici ed è possibile usare il metodo di regressione lineare Microsoft, è possibile selezionare la casella **regressore** per qualsiasi colonna numerica che si conosca (o sospetta) correlata al valore stimabile.  
  
     L'algoritmo testerà quindi i valori in tale colonna per determinare se influiscono sui risultati. In caso di dubbi, fare clic su **Suggerisci** e l'algoritmo eseguirà il test di tutte le colonne e rileverà automaticamente i valori migliori da utilizzare come regressori.  
  
    > [!NOTE]  
    >  Per creare una valutazione, è necessario un regressore. Tramite la procedura guidata viene consigliato sempre il regressore migliore, in base a un passaggio iniziale di analisi dei dati. Se pertanto non si è sicuri, è consigliabile accettare le selezioni consigliate.  
  
7.  Nella pagina **suddivisione dei dati in set di training e di testing** specificare se si desidera creare un piccolo subset di dati per il testing.  
  
8.  Nella pagina **fine** specificare i nomi per la nuova struttura di data mining e la modalità di data mining oppure accettare i nomi predefiniti specificati.  
  
9. Impostare le opzioni per l'utilizzo del modello.  
  
    -   Selezionare **Sfoglia** per aprire immediatamente il modello in un visualizzatore.  
  
         Il visualizzatore grafico consente di visualizzare un grafico della rete di dipendenze e l'albero delle decisioni generato dall'algoritmo. Esaminando queste informazioni, è possibile comprendere meglio i fattori che contribuiscono a generare i valori valutati.  
  
    -   Selezionare **Abilita drill-through** per consentire agli utenti dell'analisi di visualizzare i dati sottostanti.  
  
         Questa opzione è disponibile solo se si utilizzano gli algoritmi Decision Trees o Linear Regression.  
  
    -   **Usa modello temporaneo**. Se si seleziona questa opzione, il modello non verrà salvato nel server. I modelli temporanei vengono eliminati quando si chiude Excel.  
  
## <a name="more-about-estimation-models"></a>Ulteriori informazioni sui modelli di valutazione  
 La procedura guidata **stima** supporta l'utilizzo di uno degli algoritmi seguenti:  
  
-   Algoritmo Microsoft Decision Trees  
  
-   Algoritmo Microsoft Linear Regression  
  
-   Algoritmo Microsoft Logistic Regression  
  
-   Algoritmo Microsoft Neural Network  
  
 Nella finestra di dialogo **parametri algoritmo** è possibile impostare opzioni avanzate aggiuntive, a seconda dell'algoritmo scelto. Per informazioni sulle opzioni per ciascun algoritmo, vedere questi argomenti nella documentazione online di SQL Server:  
  
 [Guida di riferimento tecnico per l'algoritmo Microsoft Decision Trees](data-mining/microsoft-decision-trees-algorithm-technical-reference.md)  
  
 [Riferimento tecnico per l'algoritmo Microsoft Linear Regression](data-mining/microsoft-linear-regression-algorithm-technical-reference.md)  
  
 [Riferimento tecnico per l'algoritmo Microsoft Logistic Regression](data-mining/microsoft-logistic-regression-algorithm-technical-reference.md)  
  
 [Microsoft Neural Network Algorithm Technical Reference](data-mining/microsoft-neural-network-algorithm-technical-reference.md)  
  
### <a name="requirements"></a>Requisiti  
 Per utilizzare la procedura guidata Valutazione dati, è necessario essere connessi a un database di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
 Per informazioni su come creare una connessione, vedere [connettersi ai dati di origine &#40;client di data mining per&#41;Excel ](connect-to-source-data-data-mining-client-for-excel.md).  
  
 Per utilizzare l'algoritmo di valutazione, il risultato che si sta tentando di stimare deve essere espresso come valore numerico, ad esempio valuta, importo delle vendite, data oppure ora.  
  
## <a name="see-also"></a>Vedere anche  
 [Creazione di un modello di data mining](creating-a-data-mining-model.md)   
 [Diagramma dell'albero delle decisioni procedura dettagliata &#40;componenti aggiuntivi Data mining&#41;](decision-tree-diagram-walkthrough-data-mining-add-ins.md)  
  
  
