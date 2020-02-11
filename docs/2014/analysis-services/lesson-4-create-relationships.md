---
title: 'Lezione 5: creare relazioni | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: abac1a00-f827-4c3e-a473-6db5c8a3a66f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7a80f607c3187e967404ce018b7eed00497d9c01
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66078577"
---
# <a name="lesson-5-create-relationships"></a>Lezione 5: Creare relazioni
  In questa lezione verranno verificate le relazioni create automaticamente al momento dell'importazione dei dati e verranno aggiunte nuove relazioni tra tabelle diverse. Una relazione è una connessione tra due tabelle che stabilisce la modalità con cui devono essere correlati i dati in tali tabelle. Tra la tabella Product e la tabella Product Subcategory vi è ad esempio una relazione basata sul fatto che ogni prodotto appartiene a una sottocategoria. Per altre informazioni, vedere [Relazioni &#40;SSAS tabulare&#41;](tabular-models/relationships-ssas-tabular.md).  
  
 Tempo previsto per il completamento della lezione: **10 minuti**  
  
## <a name="prerequisites"></a>Prerequisites  
 Questo argomento fa parte di un'esercitazione sulla creazione di modelli tabulari, con lezioni che è consigliabile completare nell'ordine indicato. Prima di eseguire le attività in questa lezione è necessario aver completato la lezione precedente: [Lezione 3: Rinominare colonne](rename-columns.md).  
  
## <a name="review-existing-relationships-and-add-new-relationships"></a>Esaminare le relazioni esistenti e aggiungere nuove relazioni  
 Quando sono stati importati i dati utilizzando l'Importazione guidata tabella, sono state importate sette tabelle del database AdventureWorksDW. In genere, se si importano dati da un'origine relazionale, le relazioni esistenti vengono importate automaticamente insieme ai dati. Tuttavia, prima di procedere alla creazione del modello è necessario verificare che le relazioni create tra le tabelle siano appropriate. Per gli scopi di questa esercitazione verranno anche aggiunte tre nuove relazioni.  
  
#### <a name="to-review-existing-relationships"></a>Per esaminare le relazioni esistenti  
  
1.  In [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]scegliere **Vista modelli** dal menu **Modello**, quindi fare clic su **Vista diagramma**.  
  
     La finestra di progettazione dei modelli viene ora aperta in Vista diagramma, ovvero un formato grafico in cui sono rappresentate tutte le tabelle importate, con linee tra di esse. Le linee tra le tabelle indicano le relazioni create automaticamente al momento dell'importazione dei dati.  
  
     Utilizzare i controlli della mini mappa nell'angolo superiore destro di Progettazione modelli per regolare la vista in modo da includere il maggior numero di tabelle possibile. È anche possibile fare clic e trascinare le tabelle in posizioni diverse, avvicinandole o disponendole in un ordine particolare. Lo spostamento delle tabelle non influisce sulle relazioni già esistenti tra le tabelle. Per visualizzare tutte le colonne in una determinata tabella, fare clic e trascinare un bordo della tabella per ingrandirla o ridurla.  
  
2.  Fare clic sulla linea continua tra la tabella **Customer** e la tabella **Geography** . La linea continua tra queste due tabelle indica che questa relazione è attiva, vale a dire usata per impostazione predefinita durante il calcolo delle formule DAX.  
  
     Si noti che la colonna **Geography Id** nella tabella **Customer** e la colonna **Geography Id** nella tabella **Geography** appaiono ora entrambe all'interno di una casella. Ciò indica che queste sono le colonne usate nella relazione. Le proprietà della relazione sono ora visualizzate anche nella finestra **Proprietà** .  
  
    > [!TIP]  
    >  Oltre a utilizzare Progettazione modelli nella vista diagramma, è inoltre possibile utilizzare la finestra di dialogo **Gestisci relazioni** per visualizzare le relazioni tra tutte le tabelle in un formato tabella. Fare clic sul menu **Tabella** e quindi su **Gestisci relazioni**. Nella finestra di dialogo **Gestisci relazioni** sono visualizzate le relazioni create automaticamente quando sono stati importati i dati.  
  
3.  Utilizzare Progettazione modelli nella vista diagramma o la finestra di dialogo **Gestisci relazioni** per verificare che le relazioni seguenti siano state create quando ogni tabella è stata importata dal database AdventureWorksDW:  
  
    |Attivo|Tabella|Tabella di ricerca correlata|  
    |------------|-----------|--------------------------|  
    |Sì|**Customer [Geography Id]**|**Geography [Geography Id]**|  
    |Sì|**Product [Product Subcategory Id]**|**Product Subcategory [Product Subcategory Id]**|  
    |Sì|**Product Subcategory [Product Category Id]**|**Product Category [Product Category Id]**|  
    |Sì|**Internet Sales [Customer Id]**|**Customer [Customer Id]**|  
    |Sì|**Internet Sales [Product Id]**|**Product [Product Id]**|  
  
 Se qualsiasi relazione indicata nella tabella precedente non è presente, verificare che il modello includa le tabelle seguenti: Customer, Date, Geography, Product, Product Category, Product Subcategory e Internet Sales. Se si importano tabelle dalla stessa connessione origine dati in momenti distinti, tutte le relazioni tra tali tabelle non verranno create e devono essere create manualmente.  
  
 In alcuni casi, potrebbe essere necessario creare relazioni aggiuntive tra le tabelle nel modello per supportare una determinata logica di business. Per questa esercitazione, è necessario creare tre relazioni aggiuntive tra la tabella Internet Sales e la tabella Date.  
  
#### <a name="to-add-new-relationships-between-tables"></a>Per aggiungere nuove relazioni tra le tabelle  
  
1.  In Progettazione modelli, nella tabella **Internet Sales** fare clic e tenere premuto il pulsante del mouse sulla colonna **Order Date** , quindi trascinare il cursore nella colonna **Date** della tabella **Date** e infine rilasciare.  
  
     Viene visualizzata una linea continua per indicare che è stata creata una relazione attiva tra la colonna **Order Date** nella tabella **Internet Sales** e la colonna **Date** nella tabella **Date** .  
  
    > [!NOTE]  
    >  Quando si creano relazioni, l'ordine tra la tabella primaria e la tabella di ricerca correlata viene definito automaticamente in modo corretto.  
  
2.  Nella tabella **Internet Sales** fare clic e tenere premuto il pulsante del mouse sulla colonna **Due Date** , quindi trascinare il cursore nella colonna **Date** della tabella **Date** e infine rilasciare.  
  
     Viene visualizzata una linea punteggiata per indicare che è stata creata una relazione non attiva tra la colonna **Due Date** nella tabella **Internet Sales** e la colonna **Date** nella tabella **Date** . È possibile creare più relazioni tra le tabelle, ma può essere attiva una sola relazione alla volta.  
  
3.  Creare infine un'ulteriore relazione. In Progettazione modelli, nella tabella **Internet Sales** fare clic e tenere premuto il pulsante del mouse sulla colonna **Ship Date** , quindi trascinare il cursore nella colonna **Date** della tabella **Date** e infine rilasciare.  
  
     Viene visualizzata una linea punteggiata per indicare che è stata creata una relazione non attiva tra la colonna **Ship Date** nella tabella **Internet Sales** e la colonna **Date** nella tabella **Date** .  
  
## <a name="next-step"></a>passaggio successivo  
 Per continuare questa esercitazione, passare alla lezione successiva: [Lezione 6: Creare colonne calcolate](lesson-5-create-calculated-columns.md).  
  
  
