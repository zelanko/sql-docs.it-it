---
title: Stimare la procedura guidata (dati componenti aggiuntivi Data Mining per Excel) | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 9b7ffc1b77d90946a119dc462da2057cf3fe4988
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66081250"
---
# <a name="estimate-wizard-data-mining-add-ins-for-excel"></a>Procedura guidata Stima (componenti aggiuntivi Data mining per Excel)
  ![Procedura guidata stima sulla barra multifunzione Data Mining](media/dmc-estimate.gif "procedura guidata stima sulla barra multifunzione Data Mining")  
  
 La procedura guidata **Valutazione** consente di creare un modello di valutazione. Un modello di valutazione consente di estrarre modelli dai dati e di utilizzarli per stimare i fattori che influiscono sui risultati.  
  
 La valutazione viene utilizzata per stimare i risultati numerici. Se, ad esempio, la colonna di destinazione contiene il numero dei diplomati nelle scuole, espresso come percentuale, è possibile analizzare i fattori che possono determinare un aumento o una riduzione di questo numero, ad esempio il numero di studenti per scuola, il rapporto numerico tra studenti e insegnanti e il numero di insegnanti.  
  
## <a name="using-the-estimate-data-wizard"></a>Utilizzo della procedura guidata Valutazione dati  
  
1.  Nel **Data Mining** sulla barra multifunzione, fare clic su **stima**.  
  
2.  Nel **selezione dati di origine** finestra di dialogo, selezionare i dati di origine da utilizzare. È possibile usare i dati in un Excel **tabella**, un Excel **intervallo di dati**, o da un **origine dati esterna**.  
  
     Se si utilizza un'origine dati esterna, è possibile creare viste o query personalizzate e salvarle come origine dati di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
3.  Nel **stima** finestra di dialogo, seleziona la **colonna da analizzare**.  
  
     La colonna di destinazione deve contenere dati numerici continui.  
  
4.  Selezionare le colonne da utilizzare come input selezionando la **colonne di Input** casella di controllo.  
  
     Queste colonne verranno utilizzate per creare i modelli. Eliminare dall'analisi tutte le colonne di scarsa utilità, ad esempio i numeri di ID o le colonne che contengono dati irrilevanti.  
  
5.  Il **stima** procedura guidata consente di selezionare l'algoritmo ottimale per il set di dati. Tuttavia, è possibile fare clic su **parametri** per aprire il **i parametri dell'algoritmo** nella finestra di dialogo e impostare le opzioni avanzate.  
  
6.  Se i dati sono numerici ed è possibile usare il metodo Microsoft Linear Regression, è possibile controllare la **regressore** casella per qualsiasi colonna numerica che sa (o fortemente convinto) da correlare con il valore stimabile.  
  
     L'algoritmo testerà quindi i valori in tale colonna per determinare se influiscono sui risultati. Se si è certi, fare clic su **Suggerisci** e l'algoritmo verrà testate tutte le colonne e rilevare automaticamente i valori migliori da utilizzare come regressori.  
  
    > [!NOTE]  
    >  Per creare una valutazione, è necessario un regressore. Tramite la procedura guidata viene consigliato sempre il regressore migliore, in base a un passaggio iniziale di analisi dei dati. Se pertanto non si è sicuri, è consigliabile accettare le selezioni consigliate.  
  
7.  Nel **suddividere i dati in set di training e set di testing** , specificare se si desidera creare un piccolo subset di dati per il testing.  
  
8.  Nel **fine** pagina, fornire nomi per la nuova struttura di data mining e la modalità di data mining o accettare i nomi predefiniti forniti.  
  
9. Impostare le opzioni per l'utilizzo del modello.  
  
    -   Selezionare **esplorare** per aprire immediatamente il modello in un visualizzatore.  
  
         Il visualizzatore grafico consente di visualizzare un grafico della rete di dipendenze e l'albero delle decisioni generato dall'algoritmo. Esaminando queste informazioni, è possibile comprendere meglio i fattori che contribuiscono a generare i valori valutati.  
  
    -   Selezionare **abilitare il drill-through** per consentire agli utenti di analisi di visualizzare i dati sottostanti.  
  
         Questa opzione è disponibile solo se si utilizzano gli algoritmi Decision Trees o Linear Regression.  
  
    -   **Usa modello temporaneo**. Se si seleziona questa opzione, il modello non verrà salvato nel server. I modelli temporanei vengono eliminati quando si chiude Excel.  
  
## <a name="more-about-estimation-models"></a>Ulteriori informazioni sui modelli di valutazione  
 Il **stima** guidata supporta l'utilizzo di uno qualsiasi degli algoritmi seguenti:  
  
-   Algoritmo Microsoft Decision Trees  
  
-   Algoritmo Microsoft Linear Regression  
  
-   Algoritmo Microsoft Logistic Regression  
  
-   Algoritmo Microsoft Neural Network  
  
 Nel **i parametri dell'algoritmo** nella finestra di dialogo è possibile impostare opzioni avanzate aggiuntive, a seconda dell'algoritmo scelto. Per informazioni sulle opzioni per ciascun algoritmo, vedere questi argomenti nella documentazione online di SQL Server:  
  
 [Riferimento tecnico per l'algoritmo Microsoft Decision Trees](data-mining/microsoft-decision-trees-algorithm-technical-reference.md)  
  
 [Riferimento tecnico per l'algoritmo Microsoft Linear Regression](data-mining/microsoft-linear-regression-algorithm-technical-reference.md)  
  
 [Riferimento tecnico per l'algoritmo Microsoft Logistic Regression](data-mining/microsoft-logistic-regression-algorithm-technical-reference.md)  
  
 [Riferimento tecnico per l'algoritmo Microsoft Neural Network](data-mining/microsoft-neural-network-algorithm-technical-reference.md)  
  
### <a name="requirements"></a>Requisiti  
 Per utilizzare la procedura guidata Valutazione dati, è necessario essere connessi a un database di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
 Per informazioni su come creare una connessione, vedere [Connetti ai dati di origine &#40;Client di Data Mining per Excel&#41;](connect-to-source-data-data-mining-client-for-excel.md).  
  
 Per utilizzare l'algoritmo di valutazione, il risultato che si sta tentando di stimare deve essere espresso come valore numerico, ad esempio valuta, importo delle vendite, data oppure ora.  
  
## <a name="see-also"></a>Vedere anche  
 [Creazione di un modello di Data Mining](creating-a-data-mining-model.md)   
 [Decision Trees descrizione dettagliata del diagramma dell'albero &#40;componenti aggiuntivi data mining&#41;](decision-tree-diagram-walkthrough-data-mining-add-ins.md)  
  
  
