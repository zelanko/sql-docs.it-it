---
title: 'Lezione 1: Creare un progetto server di report | Microsoft Docs'
description: In questa lezione si creano un progetto server di report e un file di definizione del report (con estensione rdl) usando Progettazione report.
ms.date: 12/09/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: 675671ca-e6c9-48a2-82e9-386778f3a49f
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: ac84fb8cf355103b28fbac8f5411943aa4ee51a8
ms.sourcegitcommit: 22e97435c8b692f7612c4a6d3fe9e9baeaecbb94
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/27/2020
ms.locfileid: "92679055"
---
# <a name="lesson-1-create-a-report-server-project-reporting-services"></a>Lezione 1: Creare un progetto server di report (Reporting Services)

In questa lezione si creano un *progetto server di report* e un file di *definizione del report (con estensione rdl)* usando *Progettazione report*.

> [!NOTE]
> [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] è un ambiente [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] per la creazione di soluzioni di Business Intelligence. SSDT vanta l'ambiente di creazione Progettazione report in cui è possibile aprire, modificare, visualizzare in anteprima, salvare e distribuire definizioni impaginate di [!INCLUDE[ssrsnoversion_md](../includes/ssrsnoversion-md.md)] , origini dati condivise, set di dati condivisi e parti di report.

Quando si creano report con Progettazione report, viene creato un progetto server di report contenente i file di report e gli altri file di risorse usati dai report.

## <a name="to-create-a-report-server-project"></a>Per creare un progetto server di report
  
1. Scegliere **Nuovo** > **Progetto** dal menu **File**.  

    ![Screenshot di Visual Studio con il menu File > Nuovo > Progetto selezionato.](../reporting-services/media/ssrs-ssdt-file-01-new-project.png)
  
2. Nella colonna più a sinistra selezionare **Reporting Services** sotto **Installati**. In alcuni casi si può trovare nel gruppo **Business Intelligence**.

    ![Screenshot della finestra di dialogo Nuovo progetto che mostra Reporting Services selezionato e il modello Progetto server di report evidenziato.](../reporting-services/media/lesson-1-creating-a-report-server-project-reporting-services/select-report-server-project-template.png)

    > [!IMPORTANT]
    > Per Visual Studio, se Reporting Services non è disponibile nella colonna a sinistra, aggiungere Progettazione report installando il carico di lavoro SSDT. Scegliere **Ottieni strumenti e funzionalità** dal menu **Strumenti** e quindi selezionare **SQL Server Data Tools** nei carichi di lavoro visualizzati. Se nella colonna centrale non vengono visualizzati gli oggetti Reporting Services, aggiungere le estensioni di Reporting Services. Scegliere **Estensioni e aggiornamenti** > **Online** dal menu **Strumenti**. Nella colonna centrale selezionare **Microsoft Reporting Services Projects** (Progetti di Microsoft Reporting Services) > **Download** nelle estensioni visualizzate. Per SSDT, vedere [Scaricare SQL Server Data Tools (SSDT)](../ssdt/download-sql-server-data-tools-ssdt.md). In Visual Studio 2019, se i passaggi precedenti non funzionano, provare a installare l'[estensione Microsoft Reporting Service Project](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftReportProjectsforVisualStudio).


3. Selezionare l'icona di **Progetto server di report**&nbsp;&nbsp;![ssrs_ssdt_report_server_project](media/ssrs-ssdt-report-server-project.png) &nbsp;&nbsp;nella colonna centrale della finestra di dialogo **Nuovo progetto**.

4. Nella casella di testo **Nome** digitare "Tutorial" come nome del progetto. Per impostazione predefinita, nella casella di testo **Percorso** viene visualizzato il percorso della cartella "Documenti\Visual Studio 20xx\Projects\". Progettazione report crea una cartella denominata Tutorial in questo percorso e il progetto Tutorial in tale cartella. Se il progetto non appartiene a una soluzione di Visual Studio, Visual Studio crea anche un file di soluzione con estensione sln.

5. Selezionare **OK** per creare il progetto. Il progetto Tutorial verrà visualizzato nel riquadro **Esplora soluzioni** a destra.
  
## <a name="creating-a-report-definition-file-rdl"></a>Creazione di un file di definizione del report (RDL)  
  
1. Nel riquadro **Esplora soluzioni** fare clic con il pulsante destro del mouse sulla cartella **Report**. Se il riquadro **Esplora soluzioni** non è visualizzato, scegliere **Esplora soluzioni** dal menu **Visualizza**.

2. Scegliere **Aggiungi** > **Nuovo elemento**.

    ![Screenshot di Esplora soluzioni con il menu Report > Aggiungi > Nuovo elemento selezionato.](../reporting-services/media/ssrs-ssdt-add-report.png)

3. Nella finestra **Aggiungi nuovo elemento** selezionare l'icona **Report**.

4. Digitare "Sales Orders.rdl" nella casella di testo **Nome**.

5. Selezionare il pulsante **Aggiungi** in basso a destra nella finestra di dialogo **Aggiungi nuovo elemento** per completare il processo. Il nuovo file di report Sales Orders verrà aperto in Progettazione report nella visualizzazione Progettazione.

    ![Screenshot di Visual Studio che mostra Progettazione report con il report Sales Orders nella visualizzazione Progettazione.](media/ssrs-ssdt-01-new-report-designer.png)

## <a name="next-steps"></a>Passaggi successivi

Sono stati così creati il progetto report Tutorial e il report Sales Orders. Nelle lezioni rimanenti verranno illustrate le procedure per:

- Configurare un'origine dati per il report
- Creare un set di dati dall'origine dati
- Progettare e formattare il layout del report

Passare a [Lezione 2: Specifica delle informazioni di connessione &#40;Reporting Services&#41;](../reporting-services/lesson-2-specifying-connection-information-reporting-services.md).
