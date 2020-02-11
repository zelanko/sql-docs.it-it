---
title: Aggiungere e verificare una connessione dati o un'origine dati (Generatore report e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 1d3b2573-e29d-480d-9dde-d26379c86618
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ca1e5d039a7ea7aacd930f47eb99f854cbce8cac
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66107514"
---
# <a name="add-and-verify-a-data-connection-or-data-source-report-builder-and-ssrs"></a>Aggiungere e verificare una connessione dati o un'origine dati (Generatore report e SSRS)
  In Generatore report è possibile aggiungere un'origine dati condivisa dal server di report o creare un'origine dati incorporata per il report in uso. In Progettazione report è possibile creare un'origine dati condivisa o un'origine dati incorporata e distribuirla a un server di report.  
  
 Per aggiungere un'origine dati condivisa al report, accedere a un server di report e selezionare un'origine dati condivisa. L'origine dati condivisa del report punta alla definizione dell'origine dati condivisa nel server di report.  
  
 Per creare un'origine dati incorporata, l'utente deve disporre delle informazioni di connessione all'origine esterna di dati oltre a dover conoscere le autorizzazioni necessarie per l'accesso ai dati. Queste informazioni provengono solitamente dal proprietario dell'origine dati. Per verificare che le credenziali specificate siano sufficienti si può testare la connessione.  
  
 Per ulteriori informazioni, vedere [connessioni dati, origini dati e stringhe di connessione in Generatore report](../data-connections-data-sources-and-connection-strings-in-report-builder.md) e [specificare le credenziali in Generatore report](../specify-credentials-in-report-builder.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-create-a-reference-to-a-shared-data-source"></a>Per creare un riferimento a un'origine dati condivisa  
  
1.  Sulla barra degli strumenti nel riquadro dei dati del report fare clic su **nuovo** e quindi su **origine dati**. Verrà visualizzata la finestra di dialogo **Proprietà origine dati** .  
  
2.  Nella casella di testo **Nome** digitare un nome per l'origine dei dati.  
  
    > [!NOTE]  
    >  Questo nome viene salvato nella definizione del report locale e non viene utilizzato per denominare l'origine dati condivisa nel server di report.  
  
3.  Selezionare **Usa una connessione condivisa o un modello di report**. Verrà visualizzato l'elenco delle origini dati condivise e dei modelli di report utilizzati di recente. Per selezionarne una da un server di report fare clic su **Sfoglia** e scegliere la cartella nel server di report in cui sono disponibili le origini dati condivise.  
  
4.  Selezionare l'origine dati condivisa e quindi fare clic su **Apri**.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
 L'origine dati verrà visualizzata nel riquadro dei dati del report.  
  
### <a name="to-create-an-embedded-data-source"></a>Per creare un'origine dati incorporata  
  
1.  Sulla barra degli strumenti nel riquadro dei dati del report fare clic su **nuovo**e quindi su **origine dati**. Verrà visualizzata la finestra di dialogo **Proprietà origine dati** .  
  
2.  Nella casella di testo **Nome** digitare un nome per l'origine dati oppure accettare quello predefinito.  
  
3.  Verificare che l'opzione **Usa una connessione incorporata nel report** sia selezionata.  
  
    1.  Dall'elenco a discesa **Seleziona tipo di connessione** selezionare un tipo di origine dati, ad esempio **Microsoft SQL Server** o **OLE DB**.  
  
    2.  Specificare una stringa di connessione utilizzando una delle alternative seguenti:  
  
    -   Digitare la stringa di connessione direttamente nella casella di testo **Stringa di connessione** . Per esempi di stringhe di connessione, vedere [Connessioni dati, origini dati e stringhe di connessione in Generatore report](../data-connections-data-sources-and-connection-strings-in-report-builder.md).  
  
    -   Fare clic sul pulsante relativo all'espressione (**fx)** ) per creare un'espressione che restituisca una stringa di connessione. Nella finestra di dialogo **Espressione** digitare l'espressione nel riquadro relativo. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
    -   Fare clic su **Compila** per aprire la finestra di dialogo **Proprietà connessione** per il tipo di origine dati scelto nel passaggio 2.  
  
         Nei campi della finestra di dialogo **Proprietà connessione** inserire le informazioni appropriate per il tipo di origine dati. Le proprietà della connessione includono il tipo e il nome dell'origine dati e le credenziali da utilizzare. Dopo avere specificato i valori in questa finestra di dialogo, fare clic su **Test connessione** per verificare che l'origine dati sia disponibile e che le credenziali specificate siano corrette.  
  
4.  Fare clic su **Credenziali**.  
  
     Specificare le credenziali da utilizzare per questa origine dati. Il tipo di credenziali supportato viene determinato dal proprietario dell'origine dati. In alcuni casi, il proprietario dell'origine dati gestisce un'origine dati condivisa su un server di report e configura l'origine dati con le credenziali che è possibile utilizzare. Per queste informazioni, rivolgersi al proprietario dell'origine dati. Per altre informazioni, vedere [Specifica di credenziali in Generatore report](../specify-credentials-in-report-builder.md).  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
 L'origine dati verrà visualizzata nel riquadro dei dati del report.  
  
### <a name="to-verify-a-data-connection"></a>Per verificare una connessione dati  
  
1.  Sulla barra degli strumenti del riquadro dei dati del report fare doppio clic sull'origine dati. Verrà visualizzata la finestra di dialogo **Proprietà origine dati** .  
  
2.  Fare clic su **Test connessione**.  
  
3.  Se la connessione riesce, verrà visualizzato il messaggio seguente: "Creazione connessione completata". [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
4.  In caso contrario, verrà visualizzato il messaggio: "Impossibile connettersi all'origine dati".  
  
5.  Fare clic su **Dettagli**e utilizzare le informazioni per risolvere il problema.  
  
     Per altre informazioni, vedere [Specifica di credenziali in Generatore report](../specify-credentials-in-report-builder.md).  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Aggiungere dati a un report &#40;Generatore report e SSRS&#41;](report-datasets-ssrs.md)   
 [Set di dati condivisi e incorporati del report &#40;Generatore report e SSRS&#41;](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)   
 [Ricerca, visualizzazione e gestione dei report &#40;Generatore report e SSRS&#41;](../report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)   
 [Connessioni dati, origini dati e stringhe di connessione in Generatore report](../data-connections-data-sources-and-connection-strings-in-report-builder.md)  
  
  
