---
title: 'Lezione 1: Creazione di un progetto server di report (Reporting Services) | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 675671ca-e6c9-48a2-82e9-386778f3a49f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 52050b9513de2638cacc394309f7e87d6ba77709
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63143276"
---
# <a name="lesson-1-creating-a-report-server-project-reporting-services"></a>Lezione 1: Creazione di un progetto server di report (Reporting Services)
  Per creare un report in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], è innanzitutto necessario creare un progetto server di report in cui verranno salvati il file della definizione del report (con estensione rdl) e altri file di risorse necessari per il report. Verrà quindi creato il file della definizione del report, verranno definiti un'origine dei dati per il report, un set di dati e il layout del report. Quando si esegue il report, i dati effettivi vengono recuperati e combinati con il layout, e quindi visualizzati sullo schermo. Sarà quindi possibile esportarli, stamparli o salvarli.  
  
 In questa lezione verranno descritte le procedure per creare il progetto server di report in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Un progetto server di report consente di creare report che vengono eseguiti in un server di report.  
  
### <a name="to-create-a-report-server-project"></a>Per creare un progetto server di report  
  
1.  Fare clic su **avviare**, scegliere **tutti i programmi**, scegliere [!INCLUDE[ssCurrentUI](../includes/sscurrentui-md.md)], quindi fare clic su **SQL Server Data Tools**. Se questa è la prima volta che è stato aperto [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], fare clic su **Impostazioni Business Intelligence** per le impostazioni di ambiente predefinite.  
  
2.  Scegliere **Nuovo** dal menu **File**e quindi fare clic su **Progetto**.  
  
3.  Nell'elenco **Modelli installati** fare clic su **Business Intelligence**.  
  
4.  Fare clic su **progetto Server di Report**.  
  
5.  In **Nome**digitare **Esercitazione**.  
  
6.  Fare clic su **OK** per creare il progetto.  
  
     In Esplora soluzioni verrà visualizzato il progetto Esercitazione.  
  
### <a name="to-create-a-new-report-definition-file"></a>Per creare un nuovo file di definizione del report  
  
1.  In Esplora soluzioni fare doppio clic su **Reports**, scegliere **Add**, fare clic su **nuovo elemento**.  
  
    > [!NOTE]  
    >  Se la finestra **Esplora soluzioni** non è visualizzata, scegliere **Esplora soluzioni** dal menu **Visualizza**.  
  
2.  Nel **Aggiungi nuovo elemento** nella finestra di dialogo **modelli**, fare clic su **Report**.  
  
3.  Digitare **Sales Orders.rdl**in **Nome** , quindi fare clic su **Aggiungi**.  
  
     Verranno visualizzati Progettazione report e il nuovo file con estensione rdl nella visualizzazione Progettazione.  
  
 Progettazione report è il componente di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] eseguito in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] e ha due viste: **Progettazione** e **Anteprima**. Fare clic sulla scheda corrispondente per cambiare la vista.  
  
 I dati vengono definiti nel riquadro **Dati report** . Il layout dei report viene definito nella vista **Progettazione** . Dopo aver eseguito il report, è possibile vederne l'aspetto nella vista **Anteprima** .  
  
## <a name="next-task"></a>Attività successiva  
 In questo modo è stato creato un progetto di report denominato Esercitazione, cui è stato aggiunto un file di definizione del report (con estensione rdl). Il passaggio successivo consiste nello specificare un'origine dei dati per il report. Vedere [Lezione 2: Definizione delle informazioni di connessione &#40;Reporting Services&#41;](lesson-2-specifying-connection-information-reporting-services.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Creare un report tabella semplice &#40;esercitazione su SSRS&#41;](create-a-basic-table-report-ssrs-tutorial.md)  
  
  
