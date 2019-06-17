---
title: Grafico di accuratezza (componenti aggiuntivi Data Mining SQL Server dati) | Microsoft Docs
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
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66062984"
---
# <a name="accuracy-chart-sql-server-data-mining-add-ins"></a>Grafico di accuratezza (componenti aggiuntivi Data mining di SQL Server)
  ![Pulsante grafico di accuratezza sulla barra multifunzione Data Mining](media/dmc-accchart.gif "pulsante grafico di accuratezza sulla barra multifunzione Data Mining")  
  
 Un grafico di accuratezza consente di applicare un modello a un nuovo set di dati, quindi di valutare le prestazioni del modello. Il grafico di accuratezza creato dalla procedura guidata è un *grafico di accuratezza*, ovvero un tipo di grafico utilizzato frequentemente per misurare l'accuratezza del modello di data mining. In questo tipo di grafico di accuratezza viene visualizzata una rappresentazione grafica del miglioramento che si ottiene utilizzando il modello di data mining specificato rispetto alle stime casuali e a uno scenario ideale in cui risulta accurato il 100% delle stime. In un singolo grafico è possibile confrontare più modelli.  
  
## <a name="example"></a>Esempio  
 Si supponga che il reparto Marketing di Adventure Works Cycles intenda condurre una campagna di mailing diretto. Dalle campagne precedenti è risultato che la percentuale di risposta tipica è pari al 10%. In una tabella del database è archiviato un elenco di 10.000 potenziali clienti. In base alla percentuale di risposta tipica, è possibile prevedere che risponderanno 1.000 clienti.  
  
 Poiché tuttavia il budget consente di inviare un annuncio pubblicitario solo a 5.000 clienti, il reparto Marketing utilizza un modello di data mining per contattare i 5.000 clienti che hanno maggiore probabilità di rispondere.  
  
 Se l'azienda seleziona in modo casuale 5.000 clienti, è possibile prevedere che riceverà solo 500 risposte positive, in quanto generalmente risponde solo il 10% dei destinatari. Questo scenario è rappresentato dalla linea dell'ipotesi casuale del grafico di accuratezza.  
  
 Se invece il reparto Marketing utilizza un modello di data mining per individuare i destinatari da contattare tramite mailing e se il modello è perfetto, l'azienda può prevedere di ricevere 1.000 risposte inviando la pubblicità ai 1.000 potenziali clienti indicati dal modello. Questo scenario è rappresentato dalla linea del modello ideale del grafico di accuratezza.  
  
## <a name="using-the-accuracy-chart-wizard"></a>Utilizzo della procedura guidata Grafico di accuratezza  
 Per creare un grafico di accuratezza, è necessario fare riferimento a una struttura di data mining esistente. È possibile misurare l'accuratezza di più modelli basati sulla struttura, a condizione che venga eseguita la stessa stima.  
  
 Se non si è certi delle strutture disponibili, è possibile esplorare il server. Per altre informazioni, vedere [esplorazione di modelli in Excel &#40;componenti aggiuntivi Data Mining di SQL Server&#41;](browsing-models-in-excel-sql-server-data-mining-add-ins.md).  
  
#### <a name="to-create-an-accuracy-chart"></a>Per creare un grafico di accuratezza  
  
1.  Scegliere il **Client di Data Mining** della barra multifunzione.  
  
2.  Nel **accuratezza e convalida** gruppo, fare clic su **grafico di accuratezza**.  
  
3.  Nel **selezione struttura o modello** finestra di dialogo, scegliere il modello che si desidera valutare. Scegliere **Avanti**.  
  
    > [!NOTE]  
    >  È necessario scegliere un modello che corrisponda il più possibile ai dati che si desidera testare.  
  
4.  Nel **impostazione della colonna e del valore da stimare** finestra di dialogo scegliere la colonna che si desidera stimare e un valore di destinazione, se appropriato. Scegliere **Avanti**.  
  
     Nel caso dell'esempio precedente, è possibile scegliere la colonna che modella la risposta del cliente e specificare "Probably Will Buy" come valore di destinazione.  
  
    > [!NOTE]  
    >  Non è possibile stimare un valore continuo. È tuttavia possibile discretizzare la colonna, suddividendo i valori in intervalli discreti. Questa operazione deve essere eseguita prima di creare il modello di data mining.  
  
5.  Nel **selezione dati di origine** finestra di dialogo, specificare l'origine dei dati che verranno passati tramite il modello per creare una stima.  
  
6.  Se si usa un'origine esterna di dati e non i dati di test che viene archiviati con il modello, nei **specificare le relazioni** della finestra di dialogo mappa le colonne nei nuovi dati di origine alle colonne utilizzate nel modello di data mining.  
  
     Viene automaticamente eseguito il mapping delle colonne con nomi simili. Benché alcune colonne dei dati di input risultino irrilevanti per l'analisi e possano essere ignorate, altre sono necessarie per consentire l'elaborazione dell'input da parte del modello di data mining, ad esempio le colonne con ID transazione o con valori di destinazione oppure le colonne utilizzate per la stima. Se non è possibile eseguire il mapping di una colonna richiesta, tramite la procedura guidata viene generato un messaggio di avviso.  
  
7.  Scegliere **Fine**.  
  
     Tramite la procedura guidata viene creato un report che include il grafico di accuratezza e i dati sottostanti.  
  
### <a name="requirements"></a>Requisiti  
 Per la stima di un valore discreto, è necessario selezionare il valore di destinazione da stimare. Ad esempio, se i dati sono classificati con una risposta "Yes: Buy"come 1 e la risposta" No: Do Not Buy"come 2, è necessario specificare 1 o 2 come valori di stima. Se invece si desidera stimare un intervallo di valori, sarà possibile confrontare solo due valori alla volta. Se, ad esempio, si desidera stimare un punteggio superiore a 5, potrebbe essere necessario modificare le etichette dei dati di origine e creare un nuovo modello in cui i risultati vengano separati in due set: quelli superiori a 5 e quelli inferiori a 5. È quindi possibile confrontare l'accuratezza di questi due gruppi.  
  
## <a name="understanding-accuracy"></a>Informazioni sull'accuratezza  
 È possibile creare due tipi di grafico, uno in cui si specifica uno stato della colonna stimabile e l'altro in cui non si specifica lo stato.  
  
 Se si specifica lo stato della colonna stimabile, l'asse x del grafico rappresenta la percentuale del set di dati di test utilizzata per confrontare le stime. L'asse y del grafico rappresenta la percentuale di valori stimati come corrispondenti allo stato specificato.  
  
 Se non si specifica lo stato della colonna stimabile, sul grafico viene mostrata l'accuratezza del modello per tutte le stime possibili.  
  
 Per ulteriori informazioni sul funzionamento di un grafico di accuratezza e sul calcolo dell'accuratezza in base alle linee di stima casuali e ideali, vedere l'argomento "Grafico di accuratezza" nella documentazione online di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Vedere anche  
 [Convalida dei modelli e utilizzo dei modelli per la stima &#40;dati di componenti aggiuntivi Data Mining per Excel&#41;](validating-models-and-using-models-for-prediction-data-mining-add-ins-for-excel.md)  
  
  
