---
title: Grafico di accuratezza (componenti aggiuntivi Data mining SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- accuracy chart
- mining models, validating
- mining models, charting
- lift chart
- mining models, testing
- lift [data mining]
ms.assetid: 303973b4-71c0-4cfc-b7bc-92218b52509d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ebe159aed7b27bf00ef47a110de1c7ec5ee70adb
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66062984"
---
# <a name="accuracy-chart-sql-server-data-mining-add-ins"></a>Grafico di accuratezza (componenti aggiuntivi Data mining di SQL Server)
  ![Pulsante Grafico di accuratezza sulla barra multifunzione Data mining](media/dmc-accchart.gif "Pulsante Grafico di accuratezza sulla barra multifunzione Data mining")  
  
 Un grafico di accuratezza consente di applicare un modello a un nuovo set di dati, quindi di valutare le prestazioni del modello. Il grafico di accuratezza creato da questa procedura guidata è un *grafico*di accuratezza, ovvero un tipo di grafico utilizzato spesso per misurare l'accuratezza di un modello di data mining. In questo tipo di grafico di accuratezza viene visualizzata una rappresentazione grafica del miglioramento che si ottiene utilizzando il modello di data mining specificato rispetto alle stime casuali e a uno scenario ideale in cui risulta accurato il 100% delle stime. In un singolo grafico è possibile confrontare più modelli.  
  
## <a name="example"></a>Esempio  
 Si supponga che il reparto Marketing di Adventure Works Cycles intenda condurre una campagna di mailing diretto. Dalle campagne precedenti è risultato che la percentuale di risposta tipica è pari al 10%. In una tabella del database è archiviato un elenco di 10.000 potenziali clienti. In base alla percentuale di risposta tipica, è possibile prevedere che risponderanno 1.000 clienti.  
  
 Poiché tuttavia il budget consente di inviare un annuncio pubblicitario solo a 5.000 clienti, il reparto Marketing utilizza un modello di data mining per contattare i 5.000 clienti che hanno maggiore probabilità di rispondere.  
  
 Se l'azienda seleziona in modo casuale 5.000 clienti, è possibile prevedere che riceverà solo 500 risposte positive, in quanto generalmente risponde solo il 10% dei destinatari. Questo scenario è rappresentato dalla linea dell'ipotesi casuale del grafico di accuratezza.  
  
 Se invece il reparto Marketing utilizza un modello di data mining per individuare i destinatari da contattare tramite mailing e se il modello è perfetto, l'azienda può prevedere di ricevere 1.000 risposte inviando la pubblicità ai 1.000 potenziali clienti indicati dal modello. Questo scenario è rappresentato dalla linea del modello ideale del grafico di accuratezza.  
  
## <a name="using-the-accuracy-chart-wizard"></a>Utilizzo della procedura guidata Grafico di accuratezza  
 Per creare un grafico di accuratezza, è necessario fare riferimento a una struttura di data mining esistente. È possibile misurare l'accuratezza di più modelli basati sulla struttura, a condizione che venga eseguita la stessa stima.  
  
 Se non si è certi delle strutture disponibili, è possibile esplorare il server. Per ulteriori informazioni, vedere [esplorazione di modelli in Excel &#40;SQL Server componenti aggiuntivi Data Mining&#41;](browsing-models-in-excel-sql-server-data-mining-add-ins.md).  
  
#### <a name="to-create-an-accuracy-chart"></a>Per creare un grafico di accuratezza  
  
1.  Fare clic sulla barra multifunzione **client di data mining** .  
  
2.  Nel gruppo **accuratezza e convalida** fare clic su **grafico di accuratezza**.  
  
3.  Nella finestra di dialogo **selezione struttura o modello** scegliere il modello che si desidera valutare. Fare clic su **Avanti**.  
  
    > [!NOTE]  
    >  È necessario scegliere un modello che corrisponda il più possibile ai dati che si desidera testare.  
  
4.  Nella finestra di dialogo **specifica colonna da stimare e valore da stimare** scegliere la colonna da stimare e un valore di destinazione, se appropriato. Fare clic su **Avanti**.  
  
     Nel caso dell'esempio precedente, è possibile scegliere la colonna che modella la risposta del cliente e specificare "Probably Will Buy" come valore di destinazione.  
  
    > [!NOTE]  
    >  Non è possibile stimare un valore continuo. È tuttavia possibile discretizzare la colonna, suddividendo i valori in intervalli discreti. Questa operazione deve essere eseguita prima di creare il modello di data mining.  
  
5.  Nella finestra di dialogo **selezione dati di origine** specificare l'origine dei dati che passerà attraverso il modello per creare una stima.  
  
6.  Se si utilizza un'origine dati esterna e non i dati di test archiviati con il modello, nella finestra di dialogo **specifica relazioni** eseguire il mapping delle colonne nei nuovi dati di origine alle colonne utilizzate nel modello di data mining.  
  
     Viene automaticamente eseguito il mapping delle colonne con nomi simili. Benché alcune colonne dei dati di input risultino irrilevanti per l'analisi e possano essere ignorate, altre sono necessarie per consentire l'elaborazione dell'input da parte del modello di data mining, ad esempio le colonne con ID transazione o con valori di destinazione oppure le colonne utilizzate per la stima. Se non è possibile eseguire il mapping di una colonna richiesta, tramite la procedura guidata viene generato un messaggio di avviso.  
  
7.  Fare clic su **Fine**.  
  
     Tramite la procedura guidata viene creato un report che include il grafico di accuratezza e i dati sottostanti.  
  
### <a name="requirements"></a>Requisiti  
 Per la stima di un valore discreto, è necessario selezionare il valore di destinazione da stimare. Se ad esempio i dati vengono assegnati alla relativa categoria con una risposta "Yes: Buy" come 1 e la risposta "No: Do Not Buy" come 2, sarà necessario specificare 1 o 2 come valori di stima. Se invece si desidera stimare un intervallo di valori, sarà possibile confrontare solo due valori alla volta. Se, ad esempio, si desidera stimare un punteggio superiore a 5, potrebbe essere necessario modificare le etichette dei dati di origine e creare un nuovo modello in cui i risultati vengano separati in due set: quelli superiori a 5 e quelli inferiori a 5. È quindi possibile confrontare l'accuratezza di questi due gruppi.  
  
## <a name="understanding-accuracy"></a>Informazioni sull'accuratezza  
 È possibile creare due tipi di grafico, uno in cui si specifica uno stato della colonna stimabile e l'altro in cui non si specifica lo stato.  
  
 Se si specifica lo stato della colonna stimabile, l'asse x del grafico rappresenta la percentuale del set di dati di test utilizzata per confrontare le stime. L'asse y del grafico rappresenta la percentuale di valori stimati come corrispondenti allo stato specificato.  
  
 Se non si specifica lo stato della colonna stimabile, sul grafico viene mostrata l'accuratezza del modello per tutte le stime possibili.  
  
 Per ulteriori informazioni sul funzionamento di un grafico di accuratezza e sul calcolo dell'accuratezza in base alle linee di stima casuali e ideali, vedere l'argomento "Grafico di accuratezza" nella documentazione online di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Vedere anche  
 [Convalida di modelli e utilizzo di modelli per la stima &#40;componenti aggiuntivi Data mining per Excel&#41;](validating-models-and-using-models-for-prediction-data-mining-add-ins-for-excel.md)  
  
  
