---
title: Uso di dati della tabella nidificata come Input per un grafico di accuratezza | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Mining Accuracy Chart [Analysis Services], nested tables
- Mining Accuracy Chart [Analysis Services], input tables
- nested tables
- adding nested tables
ms.assetid: 162e0686-ada3-4dd3-9151-9589926e6613
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3a6e6d0ade60dbb42fca9bda9ee78f4dbb50064a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66082724"
---
# <a name="using-nested-table-data-as-an-input-for-an-accuracy-chart"></a>Utilizzo di dati di tabelle nidificate come input per un grafico di accuratezza
  Quando si esegue il test dell'accuratezza di un modello di data mining utilizzando dati esterni, se il modello di data mining contiene tabelle nidificate, anche i dati esterni devono contenere una tabella del case e una tabella nidificata associata.  
  
 In questo argomento viene decritto come utilizzare le tabelle nidificate utilizzate per il test del modello, come eseguire il mapping delle tabelle nidificate e del case nel modello e nei dati esterni e come applicare un filtro a una tabella nidificata.  
  
 Quando si utilizzano tabelle annidate, ricordare i suggerimenti riportati di seguito:  
  
-   Se si seleziona l'opzione **Usa test case del modello di data mining** o **Usa test case della struttura di data mining**, non è necessario specificare una tabella del case o una tabella nidificata. Con queste opzioni, la definizione dei dati di test viene archiviata nella struttura di data mining e i dati di test vengono automaticamente selezionati quando si crea il grafico di accuratezza.  
  
-   Se esiste già una relazione tra il case e la tabella nidificata nell'origine dati, viene eseguito il mapping automatico tra le colonne della struttura di data mining e le colonne con lo stesso nome della tabella di input.  
  
-   Non è possibile selezionare una tabella nidificata fino a quando non è stata specificata la tabella del case. Inoltre, non è possibile specificare una tabella nidificata come input a meno che anche il modello di data mining non utilizzi una tabella del case e una struttura della tabella nidificata.  
  
### <a name="use-a-nested-table-as-input-to-an-accuracy-chart"></a>Utilizzare una tabella nidificata come input per un grafico di accuratezza  
  
1.  Fare doppio clic sulla struttura di data mining per aprirla in Progettazione modelli di data mining.  
  
2.  Selezionare la scheda **Grafico di accuratezza modello di data mining** , quindi selezionare la scheda **Selezione input** .  
  
3.  In **Seleziona set di dati da utilizzare per il grafico di accuratezza**selezionare l'opzione **Specifica un set di dati diverso**.  
  
4.  Fare clic sul pulsante **(...)**  per scegliere il set di dati esterno da un elenco di viste origine dati nel server corrente.  
  
5.  Fare clic su **Seleziona tabella del case**. Nella finestra di dialogo **Seleziona tabella** scegliere una tabella dalla vista origine dati che contiene i dati del case e quindi fare clic su **OK**.  
  
6.  Fare clic su **Seleziona tabella nidificata**. Nella finestra di dialogo **Seleziona tabella** selezionare la tabella che contiene i dati nidificati e quindi fare clic su **OK**.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     Se è necessario modificare la relazione tra la tabella nidificata e la tabella del case, fare clic su **Modifica join** per aprire la finestra di dialogo **Crea relazione** .  
  
## <a name="see-also"></a>Vedere anche  
 [Scegliere ed eseguire il mapping dei dati di test del modello](choose-and-map-model-testing-data.md)   
 [Applicare filtri ai dati di test del modello](apply-filters-to-model-testing-data.md)  
  
  
