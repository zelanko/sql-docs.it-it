---
title: Scegliere ed eseguire il mapping dei dati di test del modello | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- columns [data mining], mining accuracy charts
- Mining Accuracy Chart [Analysis Services], column mappings
- input column mapping [Analysis Services]
- mapping input columns [Analysis Services]
ms.assetid: be0d9f20-40c3-4dac-81da-281cfe724126
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ac7a8f813aa884cc4267c73fbcedc88eecfb0a36
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62705953"
---
# <a name="choose-and-map-model-testing-data"></a>Scegliere ed eseguire il mapping dei dati di test del modello
  Per creare un grafico di accuratezza in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], è necessario scegliere i dati che verranno utilizzati per il test del modello ed eseguire il mapping dei dati al modello.  
  
 Per impostazione predefinita, in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] verranno utilizzati i dati di test del modello di data mining, a condizione che sia stato creato un set di dati di controllo al momento della compilazione della struttura di data mining. La creazione di un set di test di controllo rappresenta il modo più semplice per testare i modelli basati sulla stessa struttura di data mining perché i nomi delle colonne e i tipi di dati corrisponderanno sempre al modello e si può essere ragionevolmente certi che la distribuzione dei dati sia simile. Nella finestra di progettazione verranno inoltre create automaticamente le relazioni tra le colonne di input e le colonne del modello.  
  
 In alternativa, è possibile specificare un'origine esterna dei dati. Per i dati esterni, esistono alcuni requisiti aggiuntivi:  
  
-   Il set di dati esterno deve essere definito come vista origine dati in un'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
-   Il set di dati esterno deve contenere almeno una colonna di cui sia possibile eseguire il mapping alla colonna stimabile del modello di data mining. È possibile scegliere di ignorare alcune colonne.  
  
-   Non è possibile aggiungere nuove colonne o eseguire il mapping di colonne in una vista origine dati diversa. La vista origine dati selezionata deve contenere tutte le colonne necessarie per la query di stima.  
  
-   Se i nomi delle colonne esterne corrispondono esattamente a quelli nel modello, il mapping verrà eseguito automaticamente. Se i mapping non sono corretti, è possibile modificarli o eliminare e creare nuovi mapping per colonne esistenti.  
  
-   Se si utilizza un'origine dati esterna, è possibile applicare i filtri per limitare i dati di test a un subset attinente di case.  
  
-   Anche quando si utilizza il set di test di controllo, è necessario ricordare che i filtri possono creare differenze tra i dati di test associati a una struttura di data mining e i test case del modello di data mining.  
  
 In questo argomento viene illustrato come scegliere ed eseguire il mapping dei dati di test:  
  
 [Selezionare le tabelle di input per testare l'accuratezza di un modello di data mining](#bkmk_SelectInputs)  
  
 [Eseguire il mapping delle colonne del modello alle colonne nei dati di test](#bkmk_MapColumns)  
  
 [Modificare il mapping delle colonne nei dati di test al modello](#bkmk_ChangeMappings)  
  
##  <a name="bkmk_SelectInputs"></a> Per selezionare le tabelle di input per testare l'accuratezza di un modello di data mining  
  
1.  Nella Progettazione modelli di data mining in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]fare doppio clic sulla struttura di data mining che contiene i modelli di cui tracciare il grafico.  
  
2.  Selezionare la scheda **Grafico di accuratezza modello di data mining** .  
  
3.  Nella scheda **Selezione input** della vista **Grafico accuratezza modello di data mining** selezionare una delle opzioni seguenti:  
  
     **Utilizza test case del modello di data mining**  
  
     **Utilizza test case della struttura di data mining**  
  
     **Specifica un set di dati diverso**  
  
4.  Se è stato selezionato **Specifica un set di dati diverso**, è possibile fare clic facoltativamente su **Apri editor filtri** per creare condizioni di filtro nei set di dati di input. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
5.  Fare clic sulla scheda **Grafico di accuratezza** o **Matrice di classificazione** per compilare automaticamente il grafico utilizzando i dati di test specificati.  
  
##  <a name="bkmk_MapColumns"></a> Per eseguire il mapping delle colonne del modello alle colonne nei dati di test  
  
1.  Fare doppio clic sulla struttura di data mining contenente i modelli per i quali creare il grafico per aprire la struttura e i modelli in Progettazione modelli di data mining.  
  
2.  Selezionare la scheda **Grafico di accuratezza modello di data mining** , quindi selezionare la scheda **Selezione input** .  
  
3.  Nell'area **Seleziona set di dati da utilizzare per il grafico di accuratezza** della scheda **Selezione input**selezionare l'opzione **Specifica un set di dati diverso**.  
  
4.  Fare clic sul pulsante **(...)**  per aprire una finestra di dialogo e compilare la definizione del set di dati esterno.  
  
5.  Nella finestra di dialogo **Seleziona struttura di data mining** selezionare la struttura di data mining contenente i modelli che si desidera utilizzare e quindi fare clic su **OK**.  
  
6.  Nella tabella **Seleziona tabelle di input** della scheda **Grafico accuratezza modello di data mining** fare clic su **Seleziona tabella del case** per aprire la finestra di dialogo **Seleziona tabella** .  
  
7.  Nella finestra di dialogo **Seleziona tabella** selezionare un'origine dati nell'elenco **Origine dati** . Scegliere una tabella contenente i dati che si desidera utilizzare nella query di stima per determinare l'accuratezza dei modelli.  
  
8.  Nella casella **Nome tabella/vista** selezionare la tabella contenente i dati che si desidera usare per testare i modelli.  
  
9. Modificare i mapping, se necessario. Verrà automaticamente eseguito il mapping tra le colonne della struttura di data mining e le colonne con lo stesso nome incluse nella tabella di input. Per creare mapping manualmente, fare clic su una colonna nella tabella **Seleziona tabelle di input** e trascinarla sulla colonna corrispondente nella tabella **Struttura di data mining** . Per eliminare un mapping, fare clic sulla linea che collega la colonna contenuta nella tabella **Struttura di data mining** alla colonna contenuta nella tabella **Seleziona tabelle di input** , quindi premere CANC.  
  
10. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="bkmk_ChangeMappings"></a> Per modificare il mapping dei dati di input al modello  
  
1.  In Progettazione modelli di data mining fare doppio clic sulla struttura che contiene i modelli di cui tracciare il grafico.  
  
2.  Selezionare la scheda **Grafico di accuratezza modello di data mining** .  
  
3.  Fare clic sulla scheda **Selezione input** .  
  
4.  In **Seleziona set di dati da utilizzare per il grafico di accuratezza**selezionare l'opzione **Specifica un set di dati diverso**.  
  
5.  Fare clic sul pulsante **(...)**  per aprire una finestra di dialogo e compilare la definizione dell'origine dati esterna.  
  
6.  Nella finestra di dialogo **Specifica mapping colonne** fare clic su **Seleziona tabella del case**.  
  
7.  Nella finestra di dialogo Seleziona tabella selezionare una vista origine dati nell'elenco, quindi la tabella che contiene i dati del case. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
8.  Se le tabelle necessarie non sono disponibili, chiudere la finestra di dialogo e creare una nuova vista origine dati contenente la tabella. Per informazioni su come creare una vista origine dati, vedere [Definizione di una vista origine dati &#40;Analysis Services&#41;](../multidimensional-models/defining-a-data-source-view-analysis-services.md).  
  
9. Se il modello di data mining contiene una tabella nidificata, fare clic su **Seleziona tabella nidificata**, quindi selezionare la tabella nidificata nell'elenco di tabelle nella vista origine dati. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
10. Selezionare la linea join del mapping che si desidera modificare, quindi fare clic su **Modifica connessioni**.  
  
     Verrà visualizzata la finestra di dialogo **Modifica mapping** . In questa finestra di dialogo è presente una tabella all'interno della quale la sezione **Colonna struttura di data mining** consente di visualizzare l'elenco delle colonne incluse nella struttura di data mining selezionata, mentre la sezione **Colonna tabella** consente di visualizzare le colonne delle tabelle di input sulle quali viene eseguito il mapping alle colonne della struttura di data mining.  
  
11. In **Colonna tabella**selezionare la riga corrispondente alla riga inclusa in **Colonna struttura di data mining** per cui si desidera modificare una relazione. Selezionare una nuova colonna nell'elenco oppure selezionare la voce vuota dell'elenco per eliminare la colonna.  
  
12. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     I nuovi mapping delle colonna verranno visualizzati nella finestra di dialogo **Specifica mapping colonne** . È possibile rimuovere un mapping selezionando la linea tra le colonne e premendo CANC. È possibile creare una nuova connessione selezionando una colonna nella tabella **Struttura di data mining** , quindi trascinandola nella colonna corrispondente della tabella **Seleziona tabelle di input** .  
  
## <a name="see-also"></a>Vedere anche  
 [Attività e procedure di test e convalida &#40;data mining&#41;](testing-and-validation-tasks-and-how-tos-data-mining.md)  
  
  
