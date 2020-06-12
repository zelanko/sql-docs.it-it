---
title: Query (SQL Server componenti aggiuntivi Data mining) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- queries [data mining]
- Data Mining Query Advanced Editor
- query builder [data mining]
- DMX
ms.assetid: 16af4a6f-18d4-496a-a304-7a13aa32ee76
author: minewiskan
ms.author: owend
ms.openlocfilehash: 1d0f0212795adcaed220806f8cc1349f95c2a6f3
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/09/2020
ms.locfileid: "84539573"
---
# <a name="query-sql-server-data-mining-add-ins"></a>Query (componenti aggiuntivi Data mining di SQL Server)
  ![Pulsante Query modello, barra multifunzione Data mining](media/dmc-query.gif "Pulsante Query modello, barra multifunzione Data mining")  
  
 La procedura guidata **query** consente di interagire con i modelli di data mining esistenti per eseguire stime basate sui dati in una tabella di Excel, un intervallo di Excel o un'altra origine dati. Il processo di applicazione di nuovi dati a un modello esistente per stimare le tendenze viene definito *query di stima*.  
  
 La procedura guidata **query** fornisce inoltre un editor avanzato per la creazione o la modifica di modelli di data mining, per la generazione di query personalizzate o per l'utilizzo di strutture non supportate negli altri strumenti, ad esempio i set di impostazioni.  
  
-   Utilizzare l'editor di testo per digitare o incollare le istruzioni DMX (Data Mining Extensions) create altrove.  
  
-   Utilizzare il Generatore di query interattivo per comporre un'istruzione DMX personalizzata con l'aiuto di modelli e finestre di dialogo.  
  
-   Creare istruzioni DMX per gestire o eseguire il backup di modelli e strutture di data mining.  
  
## <a name="using-the-query-wizard"></a>Utilizzo della procedura guidata di query  
  
1.  È innanzitutto necessario specificare un'origine per i dati da utilizzare come input. Si possono utilizzare i dati in una tabella o un intervallo di Excel esistente oppure è possibile specificare un'istruzione SQL per recuperare i dati.  
  
2.  Nella procedura guidata viene quindi visualizzato un elenco dei modelli di data mining disponibili nel server a cui si è connessi. Se si conosce il modello desiderato e si ha familiarità con data mining, è anche possibile fare clic su **Avanzate** per aprire l' **Editor avanzato query di data mining**.  
  
3.  A seconda del tipo di modello scelto, è necessario specificare la colonna che contiene i dati da valutare e definire i mapping tra le colonne dei dati di input e le colonne del modello. In base all'algoritmo prescelto si possono impostare altre proprietà per il modello.  
  
4.  La procedura guidata consente infine di scegliere una o più stime e di specificare la destinazione di archiviazione dei risultati.  
  
 In qualsiasi momento, è possibile fare clic su **Avanzate** per passare all' **Editor avanzato query di data mining**, che offre un maggiore controllo su ogni parte dell'istruzione DMX. Per ulteriori informazioni sull'utilizzo degli strumenti avanzati per la modifica delle query, vedere [Advanced Data mining query editor](advanced-data-mining-query-editor.md).  
  
### <a name="requirements"></a>Requisiti  
 Per utilizzare la procedura guidata **query** , è necessario essere connessi a un'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . Il server deve inoltre contenere almeno un modello di data mining di tipo appropriato. Se non è disponibile alcun modello di data mining, è possibile crearne uno con le procedure guidate incluse nel client di data mining per Excel. Per informazioni sulla creazione di una nuova modalità di data mining tramite una procedura guidata, vedere [creazione di un modello di data mining](creating-a-data-mining-model.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Distribuzione e scalabilità di modelli di data mining &#40;componenti aggiuntivi Data mining per Excel&#41;](deploying-and-scaling-mining-models-data-mining-add-ins-for-excel.md)   
 [Client di data mining per Excel &#40;SQL Server componenti aggiuntivi Data mining&#41;](data-mining-client-for-excel-sql-server-data-mining-add-ins.md)  
  
  
