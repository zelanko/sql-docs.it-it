---
title: Creare un'origine dati incorporata o condivisa (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- data sources [Reporting Services], creating
ms.assetid: b111a8d0-a60d-4c8b-b00a-51644b19c34b
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 088889518d88c5fd45f988fe03185e22f041b627
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66109660"
---
# <a name="create-an-embedded-or-shared-data-source-ssrs"></a>Creare un'origine dati incorporata o condivisa (SSRS)
  Un'origine dati del report consente di specificare un nome e le informazioni di connessione. [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] supporta due tipi di origini dati, ovvero incorporate e condivise. Un'origine dati incorporata viene definita in una definizione del report e viene utilizzata solo dal report specifico, mentre un'origine dati condivisa viene definita come elemento separato e può essere utilizzata da più report. Per altre informazioni, vedere [incorporate e condivise le connessioni dati o origini dati &#40;Generatore Report e SSRS&#41;](../../2014/reporting-services/embedded-and-shared-data-connections-or-data-sources-report-builder-and-ssrs.md).  
  
 In Generatore report accedere al server di report o al sito di SharePoint e selezionare le origini dati oppure creare origini dati incorporate. Non è possibile creare origini dati condivise in Generatore report.  
  
 In Progettazione report è possibile creare origini dati condivise o incorporate. Nel riquadro dati Report, iniziare a creare un riferimento all'origine dati e quindi selezionare il **New** opzione. Dopo aver creato il riferimento all'origine dati, una nuova origine dati condivisa verrà aggiunta automaticamente a Esplora soluzioni nella cartella Origini dati condivise.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../includes/ssrbrddup-md.md)]  
  
 È possibile creare anche origini dati condivise direttamente in un server di report o in un sito di SharePoint. Per altre informazioni, vedere [creare, eliminare o modificare un'origine dati condivisa &#40;gestione Report&#41; ](../../2014/reporting-services/create-delete-or-modify-a-shared-data-source-report-manager.md) oppure [creare e gestire origini dati condivise &#40;Reporting Services in modalità integrata SharePoint&#41;](../../2014/reporting-services/create-manage-shared-data-sources-reporting-services-sharepoint-integrated-mode.md).  
  
### <a name="to-create-an-embedded-or-shared-data-source"></a>Per creare un'origine dati incorporata o condivisa  
  
1.  Nel riquadro dei dati del report fare clic su **Nuova** nella barra degli strumenti, quindi su **Origine dati**. Verrà visualizzata la finestra di dialogo **Proprietà origine dati** .  
  
    > [!NOTE]  
    >  Se il riquadro Dati report non è visualizzato, scegliere **Dati report** dal menu **Visualizza** .  
  
2.  Nella casella di testo **Nome** digitare un nome per l'origine dati oppure accettare quello predefinito. Il nome dell'origine dati viene utilizzato internamente nell'ambito del report. Per maggiore chiarezza è consigliabile assegnare all'origine dati un nome che includa il nome del database specificato nella stringa di connessione.  
  
3.  Per un'origine dati incorporata, verificare che **connessione incorporata** sia selezionata.  
  
    1.  Dall'elenco a discesa **Tipo** selezionare un tipo di origine dati, ad esempio **Microsoft SQL Server** o **OLE DB**.  
  
    2.  Specificare una stringa di connessione utilizzando una delle alternative seguenti:  
  
    -   Digitare la stringa di connessione direttamente nella casella di testo **Stringa di connessione** . Per un elenco di esempi di stringhe di connessione, vedere [connessioni dati, origini dati e stringhe di connessione in Generatore Report](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-report-builder.md) o [connessioni dati, origini dati e stringhe di connessione in Reporting Services](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-reporting-services.md).  
  
    -   Fare clic sul pulsante relativo all'espressione (**fx)** ) per creare un'espressione che restituisca una stringa di connessione. Nella finestra di dialogo **Espressione** digitare l'espressione nel riquadro relativo. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
    -   Fare clic su **Modifica** per aprire la finestra di dialogo **Proprietà connessione** per il tipo di origine dati scelto nel passaggio 2.  
  
         Nei campi della finestra di dialogo **Proprietà connessione** inserire le informazioni appropriate per il tipo di origine dati. Le proprietà della connessione includono il tipo e il nome dell'origine dati e le credenziali da utilizzare. Dopo avere specificato i valori in questa finestra di dialogo, fare clic su **Test connessione** per verificare che l'origine dati sia disponibile e che le credenziali specificate siano corrette. Per altre informazioni sui tipi di origini dati specifici, vedere [Aggiungere dati da origini dati esterne &#40;SSRS&#41;](report-data/add-data-from-external-data-sources-ssrs.md).  
  
4.  Per un'origine dati condivisa, verificare che **Usa riferimento a origine dati condivisa** sia selezionata.  
  
    1.  Fare clic su **Nuovo**. Nella finestra di dialogo **Proprietà origine dati condivisa** ed eseguire le operazioni descritte nei passaggi 2 e 3 per creare una nuova origine dati.  
  
    2.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
         La nuova origine dati verrà visualizzata nella cartella Origini dati condivise in Esplora soluzioni.  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     L'origine dati verrà visualizzata nel riquadro dei dati del report. Nel riquadro dei dati del report un'origine dati condivisa punta alla definizione dell'origine dati. In Generatore report la definizione dell'origine dati si trova in un server di report o in un sito di SharePoint. In Progettazione report la definizione dell'origine dati è un file di Esplora soluzioni nella cartella Origini dati condivise.  
  
### <a name="to-import-an-existing-data-source-in-report-designer"></a>Per importare un'origine dati esistente in Progettazione report  
  
1.  In Esplora soluzioni fare clic con il pulsante destro del mouse sulla cartella **Origini dati condivise** nel progetto del server report e quindi scegliere **Aggiungi elemento esistente**. Verrà visualizzata la finestra di dialogo **Aggiungi elemento esistente** .  
  
2.  Passare a un file relativo all'origine dati condivisa della definizione del report (con estensione rds) esistente e quindi fare clic su **Apri**.  
  
3.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
### <a name="to-convert-an-embedded-data-source-to-a-shared-data-source-in-report-designer"></a>Per convertire un'origine dati incorporata in un'origine dati condivisa in Progettazione report  
  
-   Nel riquadro dati Report fare doppio clic su origine dati e quindi fare clic su **Converti in origine dati condivisa**.  
  
### <a name="to-convert-a-shared-data-source-to-an-embedded-data-source-in-report-builder"></a>Per convertire un'origine dati condivisa in un'origine dati incorporata in Generatore report  
  
-   Nel riquadro dati Report fare doppio clic su origine dati e aprire **proprietà dell'origine dati**.  
  
-   Fare clic su **connessione incorporata** e completare la creazione l'origine dati incorporata, come descritto in una procedura precedente.  
  
## <a name="see-also"></a>Vedere anche  
 [Archiviare le credenziali in un'origine dati di Reporting Services](report-data/store-credentials-in-a-reporting-services-data-source.md)   
 [Connessioni dati o origini dati incorporate e condivise &#40;Generatore report e SSRS&#41;](../../2014/reporting-services/embedded-and-shared-data-connections-or-data-sources-report-builder-and-ssrs.md)   
 [Conversione di un'origine dati da incorporata a condivisa &#40;Report e SSRS&#41;](report-data/convert-data-sources-report-builder-and-ssrs.md)   
 [Associare un report o un modello a un'origine dati condivisa &#40;SSRS&#41;](report-data/bind-a-report-or-model-to-a-shared-data-source-ssrs.md)   
 [Configurare le proprietà delle origini dati per un report  &#40;Gestione report&#41;](report-data/configure-data-source-properties-for-a-report-report-manager.md)   
 [Origini dei dati supportate da Reporting Services &#40;SSRS&#41;](create-deploy-and-manage-mobile-and-paginated-reports.md)  
  
  
