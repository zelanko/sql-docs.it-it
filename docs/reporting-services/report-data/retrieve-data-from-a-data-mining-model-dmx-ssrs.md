---
title: Recuperare i dati da un modello di data mining (DMX) | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
helpviewer_keywords:
- retrieving report data
- datasets [Reporting Services], with DMX queries
- datasets [Reporting Services], Analysis Services
- queries [Reporting Services], data mining prediction
ms.assetid: d9cd3624-1594-4707-8887-55437dd7e07c
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 3b49ed7ad49555f83a80ece77f2ba23d2d4252a8
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "77081814"
---
# <a name="retrieve-data-from-a-data-mining-model-dmx-ssrs"></a>Recuperare i dati da un modello di data mining (DMX) (SSRS)
  Per usare dati da un modello di data mining di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in un report, è necessario definire un'origine dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e uno o più set di dati del report. Quando si crea la definizione dell'origine dati, è necessario specificare una stringa di connessione e le credenziali, in modo da poter accedere all'origine dati dal computer client.  
  
 È possibile creare una definizione di origine dati incorporata per l'utilizzo da un solo report oppure una definizione di origine dati condivisa che può essere utilizzata da più report. Le procedure in questo argomento descrivono come creare un'origine dati incorporata. Per altre informazioni sulle origini dati condivise, vedere [Connessioni dati o origini dati condivise e incorporate &#40;Generatore report e SSRS&#41;](https://msdn.microsoft.com/library/f417782c-b85a-4c4d-8a40-839176daba56) e [Creare, modificare ed eliminare origini dati condivise &#40;SSRS&#41;](../../reporting-services/report-data/create-modify-and-delete-shared-data-sources-ssrs.md).  
  
 Dopo aver creato un'origine dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], è possibile creare uno o più set di dati. Per ogni set di dati, viene utilizzata una finestra Progettazione query DMX (Data Mining Prediction Expression) che consente di creare una query DMX che specifica la raccolta di campi. Per altre informazioni, vedere [Interfaccia utente di Progettazione query DMX di Analysis Services](../../reporting-services/report-data/analysis-services-dmx-query-designer-user-interface.md).  
  
 Una volta creato un set di dati, il relativo nome viene visualizzato nel riquadro dei dati del report sotto forma di nodo dell'origine dati corrispondente.  
  
 Dopo aver pubblicato il report, potrebbe essere necessario modificare le credenziali per l'origine dati affinché quando il report viene eseguito nel server di report, le autorizzazioni per il recupero dei dati risultino valide.  
  
### <a name="to-create-an-embedded-microsoft-sql-server-analysis-services-data-source"></a>Per creare un'origine dati incorporata di Microsoft SQL Server Analysis Services  
  
1.  Nel riquadro dei dati del report della barra degli strumenti fare clic su **Nuova**, quindi su **Origine dati**.  
  
2.  Nella finestra di dialogo **Proprietà origine dati** digitare un nome nella casella di testo **Nome** o accettare il nome predefinito.  
  
3.  Verificare che l'opzione **Connessione incorporata** sia selezionata.  
  
4.  Nell'elenco a discesa **Tipo** selezionare **Microsoft SQL Server Analysis Services**.  
  
5.  Specificare una stringa di connessione appropriata per l'origine dati di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
     Contattare l'amministratore del database per ottenere le informazioni di connessione e le credenziali da utilizzare per connettersi all'origine dati. La stringa di connessione di esempio seguente specifica il database [!INCLUDE[ssSampleDBDWobject](../../includes/sssampledbdwobject-md.md)] di esempio nel client locale.  
  
    ```  
    Data Source=localhost;Initial Catalog=AdventureWorksDW2012  
    ```  
  
6.  Fare clic su **Credenziali**.  
  
     Impostare le credenziali da utilizzare per la connessione all'origine dati. Per altre informazioni, vedere [Specificare le credenziali e le informazioni sulla connessione per le origini dati del report](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md).  
  
    > [!NOTE]  
    >  Per testare la connessione all'origine dati, fare clic su **Modifica**. Nella finestra di dialogo **Proprietà connessione** fare clic su **Test connessione**. Se il test ha esito positivo, verrà visualizzato il messaggio informativo "Test della connessione completato". Se il test non riesce, verrà visualizzato un messaggio di avviso con ulteriori informazioni sui motivi dell'esito negativo del test.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     L'origine dati verrà visualizzata nel riquadro dei dati del report.  
  
### <a name="to-create-a-dataset-for-a-microsoft-sql-server-analysis-services"></a>Per creare un set di dati per un'origine dati di Microsoft SQL Server Analysis Services  
  
1.  Nel riquadro **Dati report** fare clic con il pulsante destro del mouse sul nome dell'origine dati che si connette a un'origine dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e quindi scegliere **Aggiungi set di dati**.  
  
2.  Nella finestra di dialogo **Proprietà set di dati** digitare un nome nella casella di testo **Nome** .  
  
3.  Nella casella **Origine dati**verificare che il nome corrisponda a quello di un'origine dati che si connette a un'origine dati di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
4.  Fare clic su **Progettazione query** per aprire la finestra Progettazione query con interfaccia grafica e creare una query in modo interattivo. Se la finestra si apre in modalità MDX, fare clic su **Tipo di comando DMX** (![Passa alla visualizzazione linguaggio query DMX](../../reporting-services/report-data/media/rsqdicon-commandtypedmx.gif "Passaggio alla visualizzazione linguaggio di query DMX")) sulla barra degli strumenti per passare alla finestra Progettazione query relativa alla funzionalità di data mining. Per altre informazioni, vedere [Interfaccia utente di Progettazione query DMX di Analysis Services](../../reporting-services/report-data/analysis-services-dmx-query-designer-user-interface.md).  
  
     In alternativa, per importare una query DMX esistente da un altro report, fare clic su **Importa**e quindi passare al file RDL contenente la query DMX. L'importazione di una query da un file con estensione dmx non è supportata.  
  
5.  Dopo avere creato ed eseguito la query per visualizzare i risultati di esempio, fare clic su **OK**.  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     Il set di dati e la relativa raccolta di campi verranno visualizzati nel riquadro dei dati del report sotto il nodo dell'origine dati.  
  
## <a name="see-also"></a>Vedere anche  
 [Tipo di connessione di Analysis Services per DMX &#40;SSRS&#41;](../../reporting-services/report-data/analysis-services-connection-type-for-dmx-ssrs.md)   
 [Creare stringhe di connessione dati - Generatore report e SSRS](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)   
 [Raccolta di campi del set di dati &#40;Generatore report e SSRS&#41;](../../reporting-services/report-data/dataset-fields-collection-report-builder-and-ssrs.md)   
 [Set di dati condivisi e incorporati del report &#40;Generatore report e SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
  
  
