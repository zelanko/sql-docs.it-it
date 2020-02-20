---
title: Creare e modificare origini dati incorporate | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
ms.assetid: 1c38c2e8-7a29-4f79-a4a3-85ed2b13723b
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: f2ce2535a28661e40e845aa87936f3c23353e544
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "74190841"
---
# <a name="create-and-modify-embedded-data-sources"></a>Creare e modificare origini dati incorporate
  Un'origine dati incorporata viene definita in una definizione del report e viene utilizzata solo dal report specifico,  
  
## <a name="to-create-an-embedded-data-source-in-report-designer"></a>Per creare un'origine dati incorporata in Progettazione report  
  
1.  Nel riquadro dei dati del report fare clic su **Nuova** nella barra degli strumenti, quindi su **Origine dati**. Verrà visualizzata la finestra di dialogo **Proprietà origine dati** .  
  
    > [!NOTE]  
    >  Se il riquadro Dati report non è visualizzato, scegliere **Dati report** dal menu **Visualizza** .  
  
2.  Nella casella di testo **Nome** digitare un nome per l'origine dati oppure accettare quello predefinito. Il nome dell'origine dati viene utilizzato internamente nell'ambito del report. Per maggiore chiarezza è consigliabile assegnare all'origine dati un nome che includa il nome del database specificato nella stringa di connessione.  
  
3.  Verificare che l'opzione **Connessione incorporata** sia selezionata, quindi eseguire la procedura seguente.  
  
    1.  Dall'elenco a discesa **Tipo** selezionare un tipo di origine dati, ad esempio **Microsoft SQL Server** o **OLE DB**.  
  
    2.  Specificare una stringa di connessione utilizzando una delle alternative seguenti:  
  
        -   Digitare la stringa di connessione direttamente nella casella di testo **Stringa di connessione** . Per un elenco di stringhe di connessione, vedere [Creare stringhe di connessione dati - Generatore report e SSRS](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md).  
  
        -   Fare clic sul pulsante relativo all'espressione (**fx)** ) per creare un'espressione che restituisca una stringa di connessione. Nella finestra di dialogo **Espressione** digitare l'espressione nel riquadro relativo. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
        -   Fare clic su **Modifica** per aprire la finestra di dialogo **Proprietà connessione** per il tipo di origine dati scelto nel passaggio 2.  
  
             Nei campi della finestra di dialogo **Proprietà connessione** inserire le informazioni appropriate per il tipo di origine dati. Le proprietà della connessione includono il tipo e il nome dell'origine dati e le credenziali da utilizzare. Dopo avere specificato i valori in questa finestra di dialogo, fare clic su **Test connessione** per verificare che l'origine dati sia disponibile e che le credenziali specificate siano corrette. Per altre informazioni sui tipi di origini dati specifici, vedere [Aggiungere dati da origini dati esterne &#40;SSRS&#41;](../../reporting-services/report-data/add-data-from-external-data-sources-ssrs.md).  
  
    3.  Fare clic su **Credenziali**.  
  
         Specificare le credenziali da utilizzare per questa origine dati. Il tipo di credenziali supportato viene determinato dal proprietario dell'origine dati.  
  
4.  La nuova origine dati incorporata verrà visualizzata nel riquadro Dati report.  
  
## <a name="to-create-an-embedded-data-source-in-report-builder"></a>Per creare un'origine dati incorporata in Generatore report  
  
1.  Nel riquadro dei dati del report della barra degli strumenti fare clic su **Nuova**, quindi su **Origine dati**. Verrà visualizzata la finestra di dialogo **Proprietà origine dati** .  
  
2.  Nella casella di testo **Nome** digitare un nome per l'origine dati oppure accettare quello predefinito.  
  
3.  Verificare che l'opzione **Usa una connessione incorporata nel report** sia selezionata.  
  
    1.  Dall'elenco a discesa **Seleziona tipo di connessione** selezionare un tipo di origine dati, ad esempio **Microsoft SQL Server** o **OLE DB**.  
  
    2.  Specificare una stringa di connessione utilizzando una delle alternative seguenti:  
  
        -   Digitare la stringa di connessione direttamente nella casella di testo **Stringa di connessione** . Per un elenco di stringhe di connessione, vedere [Creare stringhe di connessione dati - Generatore report e SSRS](data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md).  
  
        -   Fare clic sul pulsante relativo all'espressione (**fx)** ) per creare un'espressione che restituisca una stringa di connessione. Nella finestra di dialogo **Espressione** digitare l'espressione nel riquadro relativo. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
        -   Fare clic su **Compila** per aprire la finestra di dialogo **Proprietà connessione** per il tipo di origine dati scelto nel passaggio 2.  
  
             Nei campi della finestra di dialogo **Proprietà connessione** inserire le informazioni appropriate per il tipo di origine dati. Le proprietà della connessione includono il tipo e il nome dell'origine dati e le credenziali da utilizzare. Dopo avere specificato i valori in questa finestra di dialogo, fare clic su **Test connessione** per verificare che l'origine dati sia disponibile e che le credenziali specificate siano corrette.  
  
4.  Fare clic su **Credenziali**.  
  
     Specificare le credenziali da utilizzare per questa origine dati. Il tipo di credenziali supportato viene determinato dal proprietario dell'origine dati. Per altre informazioni, vedere [Specificare le credenziali e le informazioni sulla connessione per le origini dati del report](specify-credential-and-connection-information-for-report-data-sources.md).  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     L'origine dati verrà visualizzata nel riquadro dei dati del report.  
  
## <a name="see-also"></a>Vedere anche  
 [Set di dati condivisi e incorporati del report &#40;Generatore report e SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)   
 [Specificare le credenziali e le informazioni sulla connessione per le origini dati del report](specify-credential-and-connection-information-for-report-data-sources.md)  
  
  
