---
title: Query (SQL Server Data Mining Add-ins) | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: dcddeb64b14301f08a7dc723ef89737102f257ad
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66070475"
---
# <a name="query-sql-server-data-mining-add-ins"></a>Query (componenti aggiuntivi Data mining di SQL Server)
  ![Pulsante query modello, barra multifunzione Data Mining](media/dmc-query.gif "pulsante Query modello, barra multifunzione Data Mining")  
  
 Il **Query** procedura guidata consente di interagire con i modelli di data mining esistenti per eseguire stime basate sui dati in una tabella di Excel, un intervallo di Excel o un'altra origine dati. Il processo di applicazione dei nuovi dati a un modello esistente per prevedere le tendenze viene definito un *query di stima*.  
  
 Il **Query** guidata fornisce inoltre un editor avanzato per la creazione o modifica di modelli di data mining, per la generazione di query personalizzate o per l'utilizzo di strutture non supportate in altri strumenti, ad esempio set di dati nidificati.  
  
-   Usare l'editor di testo per digitare o incollare le istruzioni di Data Mining Extensions (DMX) creati in un' posizione.  
  
-   Utilizzare il Generatore di query interattivo per comporre un'istruzione DMX personalizzata con l'aiuto di modelli e finestre di dialogo.  
  
-   Creare istruzioni DMX per gestire o eseguire il backup di modelli e strutture di data mining.  
  
## <a name="using-the-query-wizard"></a>Utilizzo della procedura guidata di query  
  
1.  È innanzitutto necessario specificare un'origine per i dati da utilizzare come input. Si possono utilizzare i dati in una tabella o un intervallo di Excel esistente oppure è possibile specificare un'istruzione SQL per recuperare i dati.  
  
2.  Nella procedura guidata viene quindi visualizzato un elenco dei modelli di data mining disponibili nel server a cui si è connessi. Se si conosce il modello desiderato e si ha familiarità con il data mining, è possibile anche fare clic su **avanzate** per aprire il **Editor di Query avanzate di Data Mining**.  
  
3.  A seconda del tipo di modello scelto, è necessario specificare la colonna che contiene i dati da valutare e definire i mapping tra le colonne dei dati di input e le colonne del modello. In base all'algoritmo prescelto si possono impostare altre proprietà per il modello.  
  
4.  La procedura guidata consente infine di scegliere una o più stime e di specificare la destinazione di archiviazione dei risultati.  
  
 In qualsiasi momento, è possibile fare clic su **avanzate** per passare alle **Advanced Query Editor di Data Mining**, che offre un maggiore controllo su qualsiasi parte dell'istruzione DMX. Per altre informazioni su come usare la query avanzata strumenti di modifica, vedere [avanzati Editor di Query di Data Mining](advanced-data-mining-query-editor.md).  
  
### <a name="requirements"></a>Requisiti  
 Usare la **Query** procedura guidata, è necessario essere connessi a un'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Il server deve inoltre contenere almeno un modello di data mining di tipo appropriato. Se non è disponibile alcun modello di data mining, è possibile crearne uno con le procedure guidate incluse nel client di data mining per Excel. Per informazioni su come creare una nuova modalità di data mining tramite una procedura guidata, vedere [creazione di un modello di Data Mining](creating-a-data-mining-model.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Distribuzione e scalabilità di modelli di Data Mining &#40;dati di componenti aggiuntivi Data Mining per Excel&#41;](deploying-and-scaling-mining-models-data-mining-add-ins-for-excel.md)   
 [Client di Data Mining per Excel &#40;componenti aggiuntivi Data Mining di dati SQL Server&#41;](data-mining-client-for-excel-sql-server-data-mining-add-ins.md)  
  
  
