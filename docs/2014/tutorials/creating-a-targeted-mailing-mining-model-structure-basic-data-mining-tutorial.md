---
title: Creazione di una struttura del modello di data mining Targeted Mailing (esercitazione di base sul data mining) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: a9c67f29-0c47-4a5a-862b-db0f5213c2c9
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 2bd2e9d0decc730a59b63ee600bec2d080cc85fb
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62856168"
---
# <a name="creating-a-targeted-mailing-mining-model-structure-basic-data-mining-tutorial"></a>Creazione di una struttura del modello di data mining Targeted Mailing (Esercitazione di base sul data mining)
  Il primo passaggio nella creazione di uno scenario relativo al mailing diretto consiste nell'utilizzo di Creazione guidata modello di data mining in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] per creare una nuova struttura e un nuovo modello di data mining basato su un albero delle decisioni.  
  
 In questa attività verrà configurata una nuova struttura di data mining e verrà aggiunto un modello di data mining [!INCLUDE[msCoName](../includes/msconame-md.md)] iniziale basato sull'algoritmo Decision Trees. Per creare la struttura, verranno innanzitutto selezionate le tabelle e le viste, quindi si identificheranno le colonne da utilizzare rispettivamente per il training e per il testing.  
  
### <a name="to-create-a-mining-structure-for-the-targeted-mailing-scenario"></a>Per creare una struttura di data mining per lo scenario relativo al mailing diretto  
  
1.  In Esplora soluzioni fare clic con il pulsante destro del mouse su **strutture di data** mining e scegliere **nuova struttura di data** mining per avviare Creazione guidata modello di data mining  
  
2.  Nella pagina iniziale **Creazione guidata modello di data mining** fare clic su **Avanti**.  
  
3.  Nella pagina **Selezione metodo di definizione** verificare che sia selezionato **da database relazionale o data warehouse esistente** e quindi fare clic su **Avanti**.  
  
4.  Nella pagina **Crea la struttura di data mining** in **cui data mining tecnica si desidera utilizzare?** selezionare **Microsoft Decision Trees**.  
  
    > [!NOTE]  
    >  Se viene visualizzato un avviso relativo al mancato rilevamento di algoritmi di data mining, è possibile che le proprietà del progetto non siano state configurate correttamente. Questo avviso viene visualizzato quando il progetto tenta di recuperare un elenco di algoritmi di data mining dal server di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] e quest'ultimo non viene rilevato. Per impostazione predefinita [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] , utilizzerà **localhost** come server. Se si utilizza un'istanza diversa o un'istanza denominata, è necessario modificare le proprietà del progetto. Per ulteriori informazioni, vedere la pagina relativa alla [creazione di un progetto Analysis Services &#40;esercitazione di base sul Data Mining&#41;](../../2014/tutorials/creating-an-analysis-services-project-basic-data-mining-tutorial.md).  
  
5.  Fare clic su **Avanti**.  
  
6.  Nella pagina **Selezione vista origine dati** , nel riquadro **viste origine dati disponibili** , selezionare **Targeted Mailing**. È possibile fare clic su **Sfoglia** per visualizzare le tabelle nella vista origine dati e quindi fare clic su **Chiudi** per tornare alla procedura guidata.  
  
7.  Fare clic su **Avanti**.  
  
8.  Nella pagina **impostazione tipi di tabelle** selezionare la casella di controllo nella colonna **case** per vTargetMail per utilizzarla come tabella del case, quindi fare clic su **Avanti**. La tabella ProspectiveBuyer verrà utilizzata in un secondo momento per il testing. Per il momento, ignorarla.  
  
9. Nella pagina **impostazione dati di training** si identificherà almeno una colonna stimabile, una colonna chiave e una colonna di input per il modello. Selezionare la casella di controllo nella colonna **stimabile** nella riga **BikeBuyer** .  
  
    > [!NOTE]  
    >  Si noti il messaggio di avviso nella parte inferiore della finestra. Non sarà possibile passare alla pagina successiva fino a quando non si seleziona almeno una colonna di **input** e una colonna **stimabile** .  
  
10. Fare clic su **Suggerisci** per aprire la finestra di dialogo **Suggerisci colonne correlate** .  
  
     Il pulsante **Suggerisci** è abilitato ogni volta che è stato selezionato almeno un attributo stimabile. Nella finestra di dialogo **Suggerisci colonne correlate** sono elencate le colonne più strettamente correlate alla colonna stimabile e gli attributi vengono ordinati in base alla relativa correlazione con l'attributo stimabile. Le colonne che presentano una correlazione significativa (confidenza maggiore del 95%) vengono selezionate automaticamente per essere incluse nel modello.  
  
     Esaminare i suggerimenti e quindi fare clic su **Annulla** per ignorare i suggerimenti.  
  
    > [!NOTE]  
    >  Se si fa clic su **OK**, tutti i suggerimenti elencati verranno contrassegnati come colonne di input nella procedura guidata. Se si accetta solo una parte dei suggerimenti, è necessario modificare i valori manualmente.  
  
11. Verificare che la casella di controllo nella colonna **chiave** sia selezionata nella riga **CustomerKey** .  
  
    > [!NOTE]  
    >  Se la tabella di origine nella vista origine dati indica una chiave, Creazione guidata modello di data mining sceglierà automaticamente tale colonna come chiave per il modello.  
  
12. Selezionare le caselle di controllo nella colonna **input** nelle righe seguenti. È possibile selezionare più colonne evidenziando un intervallo di celle e premendo CTRL mentre si seleziona una casella di controllo.  
  
    -   **Età**  
  
    -   **CommuteDistance**  
  
    -   **EnglishEducation**  
  
    -   **EnglishOccupation**  
  
    -   **Genere**  
  
    -   **GeographyKey**  
  
    -   **HouseOwnerFlag**  
  
    -   **MaritalStatus**  
  
    -   **NumberCarsOwned**  
  
    -   **NumberChildrenAtHome**  
  
    -   **Region**  
  
    -   **TotalChildren**  
  
    -   **YearlyIncome**  
  
13. Nella colonna all'estrema sinistra della pagina selezionare le caselle di controllo relative alle righe seguenti.  
  
    -   **AddressLine1**  
  
    -   **AddressLine2**  
  
    -   **DateFirstPurchase**  
  
    -   **EmailAddress**  
  
    -   **FirstName**  
  
    -   **LastName**  
  
     Assicurarsi che queste righe contengano segni di spunta solo nella colonna sinistra. Le colonne corrispondenti verranno aggiunte alla struttura ma non verranno incluse nel modello. Tuttavia, dopo la compilazione del modello, saranno disponibili per il drill-through e il testing. Per ulteriori informazioni sul drill-through, vedere [query drill-through &#40;Data Mining&#41;](../../2014/analysis-services/data-mining/drillthrough-queries-data-mining.md)  
  
14. Fare clic su **Avanti**.  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
 [Impostazione del tipo di dati e del tipo di contenuto &#40;esercitazione di base sul data mining&#41;](../../2014/tutorials/specifying-the-data-type-and-content-type-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Impostazione tipi di tabella &#40;creazione guidata modello di data mining&#41;](../../2014/analysis-services/specify-table-types-data-mining-wizard.md)   
 [Progettazione modelli di data mining](../../2014/analysis-services/data-mining/data-mining-designer.md)   
 [Algoritmo Microsoft Decision Trees](../../2014/analysis-services/data-mining/microsoft-decision-trees-algorithm.md)  
  
  
