---
title: Rilevare le categorie (strumenti di analisi tabelle per Excel) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Table Analysis tools
- clustering [data mining]
- mining model, decision tree
- category detection
ms.assetid: 3c7e9ebb-d0c9-498e-a9ba-cc13eaa43520
author: minewiskan
ms.author: owend
ms.openlocfilehash: a507e0d77cd81165b0220e3d09ec10227d32d853
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/08/2020
ms.locfileid: "84528707"
---
# <a name="detect-categories-table-analysis-tools-for-excel"></a>Rileva categorie (Strumenti di analisi tabelle per Excel)
  ![Pulsante Rileva categorie sulla barra multifunzione](media/tat-detectcat.gif "Pulsante Rileva categorie sulla barra multifunzione")

 Lo strumento **Rileva categorie** consente di trovare automaticamente le righe in una tabella con caratteristiche simili.

 Al termine dell'esecuzione dello strumento, viene creato un report in cui sono elencate tutte le categorie trovate, insieme alle relative caratteristiche distintive. Per impostazione predefinita, nella tabella dati contenente la categoria proposta viene aggiunta una nuova colonna per ogni riga di dati. È quindi possibile esaminare le categorie e rinominarle.

## <a name="using-the-detect-categories-tool"></a>Utilizzo dello strumento Rileva categorie

1.  Aprire una tabella di Excel.

2.  Fare clic su **Rileva categorie**.

3.  Specificare le colonne da utilizzare nell'analisi. È possibile deselezionare le colonne contenenti valori distinti, ad esempio nomi o ID di record, poiché non sono utili per l'analisi.

4.  È possibile specificare il numero massimo di categorie da creare. Per impostazione predefinita, vengono create automaticamente tutte le categorie trovate dallo strumento.

5.  Fare clic su **Esegui**.

6.  Tramite lo strumento viene creato un nuovo foglio di lavoro, denominato Report categorie, contenente l'elenco delle categorie e le relative caratteristiche.

 Per ulteriori informazioni su come specificare le opzioni per lo strumento, vedere [finestra di dialogo Rileva categorie (strumenti di analisi tabelle per Excel)](detect-categories-table-analysis-tools-for-excel.md).

## <a name="understanding-the-categories-report"></a>Informazioni su Report categorie
 Il **report categorie** contiene due tabelle, le caratteristiche **elenco** categorie e **categoria**e un grafico **Profili categoria** .

### <a name="category-list"></a>Elenco di categorie
 Nella prima tabella sono elencate le categorie trovate. La colonna **conteggio** righe indica il numero di righe di dati assegnate a ogni categoria.

 Il modello crea nomi temporanei per ogni categoria, ma è possibile rinominare le categorie come si desidera. Nell'esempio seguente, ad esempio, la prima categoria è stata rinominata **low income**, perché questo è l'attributo principale del cluster.

 ![Report creato dallo strumento Rileva categorie](media/dm13-tat-detectcat-report1.gif "Report creato dallo strumento Rileva categorie")

 Non appena si digita la nuova etichetta, la modifica viene propagata a tutti gli altri grafici e all'elenco di categorie aggiunto nel foglio di lavoro dati di origine.

### <a name="category-characteristics"></a>Caratteristiche categoria
 La seconda tabella, **categoria caratteristiche**, Mostra i dettagli relativi alla composizione di ogni categoria. Fare clic sul pulsante **filtro** nella parte superiore della colonna **categoria** per visualizzare lo stato attivo su una o solo alcune categorie.

 ![Report creato dallo strumento Rileva categorie](media/dm13-tat-detectcat-report2.gif "Report creato dallo strumento Rileva categorie")

 L'ombreggiatura nella colonna relativa all' **importanza relativa**indica l'importanza della combinazione di attributo e valore come fattore di distinzione. Più è lunga la barra, più è probabile che l'attributo sia fortemente rappresentativo della categoria.

### <a name="categories-profile-chart"></a>Grafico Profili categoria
 Il grafico finale nel foglio di calcolo del **report Categories** , **Profili categoria**, è un **grafico pivot** interattivo che è possibile utilizzare per ridisporre e nascondere i campi, filtrare i valori e personalizzare l'aspetto del grafico.

 In Excel 2013 sono ora disponibili gli **stili dei grafici** e i controlli **degli elementi del grafico** direttamente nell'area di progettazione che semplificano il miglioramento della progettazione del grafico.

 ![Report creato dallo strumento Rileva categorie](media/dm13-tat-detectcat-report3.gif "Report creato dallo strumento Rileva categorie")

## <a name="requirements"></a>Requisiti
 Lo strumento **Rileva categorie** non prevede requisiti per la quantità o il tipo di dati.

> [!NOTE]
>  Quando si utilizza lo strumento **Rileva categorie** , viene creata una nuova colonna, Category, nella tabella dati originale. Se si lascia questa colonna nella tabella dati e quindi si eseguono successivamente operazioni di data mining, è possibile che i risultati vengano falsati dalla presenza di tale colonna. Per evitare questo problema, è consigliabile creare una copia della tabella dati senza la colonna Categoria prima di utilizzare altri strumenti di data mining.

## <a name="related-tools"></a>Strumenti correlati
 Quando lo strumento **Rileva categorie** analizza i dati, crea una struttura data mining e data mining modello usando l' [!INCLUDE[msCoName](../includes/msconame-md.md)] algoritmo Clustering.

 Dopo aver creato un modello di data mining utilizzando lo strumento **Analizza fattori di influenza chiave** , è possibile utilizzare il client di data mining per Excel per esplorare il modello ed esplorare le relazioni in modo più dettagliato. Il Client di data mining per Excel è un componente aggiuntivo separato in cui sono disponibili funzionalità di data mining più avanzate. Per informazioni, vedere [esplorazione di modelli in Excel &#40;SQL Server componenti aggiuntivi Data Mining&#41;](browsing-models-in-excel-sql-server-data-mining-add-ins.md).

 Per ulteriori informazioni sull'utilizzo delle funzionalità di modellazione dei dati nel client di data mining per Excel, vedere [creazione di un modello di data mining](creating-a-data-mining-model.md).

 Per ulteriori informazioni sull'algoritmo utilizzato dallo strumento **Rileva categorie** , vedere l'argomento "algoritmo Microsoft Clustering" nella [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] documentazione online di.

## <a name="see-also"></a>Vedere anche
 [Strumenti di analisi tabelle per Excel](table-analysis-tools-for-excel.md)


