---
title: 'Lezione 1: Creazione di un progetto server di report (Reporting Services) | Microsoft Docs'
ms.date: 11/30/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: 675671ca-e6c9-48a2-82e9-386778f3a49f
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 72d337f441d3aabb5dc1ee8801a5cec200904d23
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/15/2019
ms.locfileid: "56292349"
---
# <a name="lesson-1-creating-a-report-server-project-reporting-services"></a>Lezione 1: Creazione di un progetto server di report (Reporting Services)

In questa lezione si creerà un *progetto server di report* e un file di *definizione del report (con estensione rdl)* in [!INCLUDE[ssBIDevStudio_md](../includes/ssbidevstudio-md.md)] all'interno di Visual Studio. 

Per creare un report con [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], è innanzitutto necessario creare un progetto server di report in cui è possibile salvare il file della definizione del report (con estensione rdl) e altri file di risorse necessari per il report. 

Nelle lezioni successive verranno definiti un'origine dati per il report, un set di dati e il layout del report. Quando si esegue il report, i dati vengono recuperati e combinati con il layout, quindi visualizzati sullo schermo, da dove sarà possibile esportarli, stamparli o salvarli.  
  
  
  
## <a name="to-create-a-report-server-project"></a>Per creare un progetto server di report  
  
1.  Aprire [!INCLUDE[ssBIDevStudio_md](../includes/ssbidevstudio-md.md)].  
  
2.  Nel menu **File** > **Nuovo** > **Progetto**.  

    ![ssrs-ssdt-file-01-new-project](../reporting-services/media/ssrs-ssdt-file-01-new-project.png)
  
3.  In **Installato** > **Modelli** > **Business Intelligence**fare clic su **Reporting Services**.

    ![ssrs-ssdt-01-new-rs-project](../reporting-services/media/ssrs-ssdt-01-new-rs-project.png)

5. Fare clic su **Progetto server di report** ![ssrs_ssdt_report_server_project](../reporting-services/media/ssrs-ssdt-report-server-project.png). 

   >**Nota**: se non vengono visualizzate le opzioni **Business Intelligence** o **Progetto server di report**, è necessario aggiornare SSDT con i modelli di Business Intelligence. Vedere [Scaricare SQL Server Data Tools (SSDT)](../ssdt/download-sql-server-data-tools-ssdt.md)  
  
5.  In **Nome**digitare **Esercitazione**.  

    Per impostazione predefinita, viene creato nella cartella Visual Studio 2015\Projects in una nuova directory.
    
    ![ssrs-ssdt-01-solution-location](../reporting-services/media/ssrs-ssdt-01-solution-location.png)
  
6.  Fare clic su **OK** per creare il progetto.  
  
    Il progetto Esercitazione viene visualizzato sul lato destro del riquadro Esplora soluzioni.  
  
## <a name="to-create-a-new-report-definition-file"></a>Per creare un nuovo file di definizione del report  
  
1.  Nel riquadro **Esplora soluzioni** fare clic con il pulsante destro del mouse su **Report** > **Aggiungi** > **Nuovo elemento**. 

    >**Suggerimento**: se non viene visualizzato il riquadro **Esplora soluzioni**, scegliere **Esplora soluzioni** dal menu **Visualizza**. 

    ![ssrs_ssdt_add_report](../reporting-services/media/ssrs-ssdt-add-report.png)
  
2.  Nella finestra **Aggiungi nuovo elemento** fare clic su **Report** ![ssrs_ssdt_report](../reporting-services/media/ssrs-ssdt-report.png).  
  
3.  Digitare **Sales Orders.rdl**in **Nome** , quindi fare clic su **Aggiungi**.  
  
    Verranno visualizzati Progettazione report e il nuovo file con estensione rdl nella visualizzazione Progettazione.  
    
    ![ssrs-ssdt-01-new-report-designer](../reporting-services/media/ssrs-ssdt-01-new-report-designer.png)
  
     Progettazione report è il componente di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] eseguito in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] e ha due viste: **Progettazione** e **Anteprima**. Fare clic sulla scheda corrispondente per cambiare la vista.  
  
    I dati vengono definiti nel riquadro **Dati report** . Il layout dei report viene definito nella vista **Progettazione** . Dopo aver eseguito il report, è possibile vederne l'aspetto nella vista **Anteprima** .  
  
## <a name="next-lesson"></a>Lezione successiva  
In questo modo è stato creato un progetto di report denominato Esercitazione, cui è stato aggiunto un file di definizione del report (con estensione rdl). Il passaggio successivo consiste nello specificare un'origine dei dati per il report. Vedere [Lezione 2: Definizione delle informazioni di connessione &#40;Reporting Services&#41;](../reporting-services/lesson-2-specifying-connection-information-reporting-services.md).  
  
## <a name="see-also"></a>Vedere anche  
[Creare un report tabella semplice &#40;esercitazione su SSRS&#41;](../reporting-services/create-a-basic-table-report-ssrs-tutorial.md)  
  

