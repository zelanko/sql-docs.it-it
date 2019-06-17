---
title: Grafico profitti (Analysis Services - Data Mining) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- accuracy, charting
- revenue, estimating
- benefits, estimating
- charts [Analysis Services]
- profit charts [Analysis Services]
ms.assetid: 760ee051-6fd8-48e3-8d2e-82db3ab45e45
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1a64eacb1219e239ad894d9922db5a5032ed525b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66083086"
---
# <a name="profit-chart-analysis-services---data-mining"></a>Grafico profitti (Analysis Services - Data mining)
  In un grafico dei profitti viene visualizzata la redditività associata all'utilizzo di un modello di data mining. Si supponga, ad esempio, che il modello vengono stimati i clienti che una società dovrebbero contattare in uno scenario aziendale. In tal caso, sarebbe necessario aggiungere le informazioni del grafico dei profitti in merito al costo della campagna di mailing diretto. Successivamente, nel grafico completato verrà visualizzato il profitto stimato della campagna indirizzata ai clienti corretti, rispetto a quello di una campagna con clienti contattati casualmente.  
  
## <a name="build-a-profit-chart"></a>Creare un grafico dei profitti  
 Un grafico dei profitti è simile a uno di accuratezza. Iniziare creando un grafico di accuratezza e quindi aggiungere le informazioni sui costi e i profitti.  
  
 Per creare un grafico dei profitti, è necessario disporre di un modello esistente.  
  
 Per questo esempio, è stato utilizzato il modello di albero delle decisioni di Mailing diretto. Il modello identifica i clienti che con una certa probabilità acquisteranno una bicicletta. È possibile applicare il **Grafico profitti** per determinare il numero di clienti di destinazione per ottimizzare il profitto.  
  
 Se non si dispone del modello di esempio, è possibile creare usando il [Basic Data Mining Tutorial](../../tutorials/basic-data-mining-tutorial.md).  
  
1.  Aprire il generatore del grafico di accuratezza del modello di data mining.  
  
    -   In SQL Server Management Studio fare clic con il pulsante destro del mouse sul modello e scegliere **Visualizza grafico di accuratezza**.  
  
    -   In SQL Server Data Tools aprire il progetto in cui è stato creato il modello e fare clic sulla scheda **Grafico accuratezza modello di data mining** .  
  
2.  Nella scheda **Selezione input** selezionare il modello e scegliere il valore dell'attributo stimabile.  
  
     Per questo scenario specifico, si è interessati solo alla redditività della stima accurata di un valore: [Bike buyer] =1.  
  
     Esistono tuttavia altri scenari in cui si sarà ugualmente interessati alla stima corretta dei valori falsi. Ad esempio, il costo di un falso positivo in un test di diagnosi medica può essere significativo e deve essere incluso nella redditività della stima, oltre al costo dei falsi negativi. In questi scenari sarà necessario misurare tutti gli esiti.  
  
3.  Selezionare un set di dati per il testing. Per questo esempio, selezionare il set di dati di testing.  
  
4.  Fare clic sulla scheda **Grafico di accuratezza** .  
  
     Verrà generato automaticamente un grafico di accuratezza.  
  
5.  Per convertire questo grafico in un grafico dei profitti, selezionare **Grafico profitti** nell'elenco **Tipo di grafico** .  
  
6.  Dopo avere scelto il grafico dei profitti come tipo di grafico, verrà aperta automaticamente la finestra di dialogo **Impostazione grafico profitti** .  
  
     Questa finestra di dialogo consente di specificare i costi e i vantaggi associati a una campagna di mailing diretto. Per il grafico mostrato in questi esempi, sono stati utilizzati i valori seguenti:  
  
    |Impostazione|Value|Commenti|  
    |-------------|-----------|--------------|  
    |**Popolazione**|20,000|Impostare il valore per la popolazione target totale<br /><br /> Il database può contenere molti clienti, ma per risparmiare sulle spese di mailing è possibile scegliere di individuare come destinatari solo i primi 20.000 clienti aventi maggiore probabilità di rispondere. È possibile ottenere questo elenco eseguendo una query di stima e ordinando i dati in base alla probabilità restituita dal modello predittivo.|  
    |**Costi fissi**|500|Immettere il costo una tantum per la configurazione di una campagna di mailing diretto per 20.000 persone. Nel costo possono essere incluse le spese di stampa o le spese di configurazione di una campagna di posta elettronica.|  
    |**Costi singolo contatto**|3|Immettere il costo unitario per la campagna di mailing diretto<br /><br /> Questa quantità verrà moltiplicata per un numero minore o uguale a 20.000, a seconda del numero di clienti stimati dal modello come buone possibilità.|  
    |**Ricavi per singolo contatto**|400|Immettere un valore che rappresenta la quantità di profitto o reddito che può essere previsto da un risultato positivo In questo caso, si presupporrà che la spedizione di un catalogo dei risultati nell'acquisto di accessori o di biciclette Media di €400.<br /><br /> Questo importo verrà utilizzato per prevedere il profitto complessivo associato ai case con probabilità elevata.|  
  
7.  Dopo avere impostato i parametri obbligatori, fare clic su **OK**.  
  
8.  Il grafico verrà aggiornato per mostrare la curva dei profitti.  
  
## <a name="understanding-the-profit-chart"></a>Informazioni sul grafico dei profitti  
 Nel diagramma seguente viene mostrato il grafico basato su questi parametri. L'asse Y del grafico rappresenta i profitti, mentre l'asse X rappresenta la percentuale di clienti contattata mediante la campagna di marketing diretto.  
  
 Come illustrato, è possibile utilizzare un grafico dei profitti per confrontare più modelli, purché in tutti venga stimato lo stesso attributo discreto.  
  
 ![confronto tra tre modelli di grafico profitti](../media/dm14-profitchartupdated.gif "confronto di tre modelli di grafico profitti")  
  
 Si noti la linea verticale grigia nel grafico. Quando si fa clic e si trascina la riga, la descrizione comando mostra la percentuale della popolazione di destinazione inclusa sotto la curva in corrispondenza di quel punto.  
  
 Man mano che si sposta la linea, la **Legenda data mining** viene aggiornata per visualizzare il valore in percentuale, un punteggio per il profitto e la probabilità di stima associata alla percentuale di popolazione in corrispondenza della linea verticale grigia.  
  
 Se, ad esempio, si utilizza questo modello per stabilire a chi conviene inviare il materiale promozionale, è possibile decidere di selezionare come destinatari il 25% della popolazione, in base alle probabilità di stima. Tuttavia, l'area sotto la curva dei profitti del grafico risulta maggiore tra il 40 e il 70 percento, indicando così che indirizzando la campagna a un maggior numero di persone è possibile ottimizzare il ritorno anche se risponde una percentuale complessiva di destinatari inferiore.  
  
## <a name="saving-charts"></a>Salvataggio di grafici  
 Quando si crea un grafico di accuratezza o un grafico dei profitti, nel server non viene creato alcun oggetto. Al contrario, le query vengono eseguite su un modello esistente e i risultati vengono visualizzati nel visualizzatore. Per salvare i risultati, è necessario copiare il grafico o i risultati in Excel o in un altro file.  
  
## <a name="related-content"></a>Contenuto correlato  
 Negli argomenti seguenti sono contenute ulteriori informazioni su come sia possibile compilare e utilizzare i grafici di accuratezza.  
  
|Argomento|Collegamenti|  
|------------|-----------|  
|Viene fornita una procedura dettagliata relativa alla creazione di un grafico di accuratezza per il modello Targeted Mailing.|[Esercitazione di base sul data mining](../../tutorials/basic-data-mining-tutorial.md)<br /><br /> [Test dell'accuratezza con i grafici di accuratezza &#40;Esercitazione di base sul data mining&#41;](../../tutorials/testing-accuracy-with-lift-charts-basic-data-mining-tutorial.md)|  
|Vengono illustrati i tipi di grafici correlati.|[Grafico di accuratezza &#40;Analysis Services - Data mining&#41;](lift-chart-analysis-services-data-mining.md)<br /><br /> [Matrice di classificazione &#40;Analysis Services - Data mining&#41;](classification-matrix-analysis-services-data-mining.md)<br /><br /> [Grafico a dispersione &#40;Analysis Services - Data mining&#41;](scatter-plot-analysis-services-data-mining.md)|  
|Viene descritta la convalida incrociata per modelli e strutture di data mining.|[Convalida incrociata &#40;Analysis Services - Data mining&#41;](cross-validation-analysis-services-data-mining.md)|  
|Vengono descritti i passaggi per la creazione di grafici di accuratezza e di altri grafici simili.|[Attività e procedure di test e convalida &#40;data mining&#41;](testing-and-validation-tasks-and-how-tos-data-mining.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Test e convalida &#40;Data mining&#41;](testing-and-validation-data-mining.md)   
 [Test dell'accuratezza con i grafici di accuratezza &#40;Esercitazione di base sul data mining&#41;](../../tutorials/testing-accuracy-with-lift-charts-basic-data-mining-tutorial.md)  
  
  
