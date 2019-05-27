---
title: 'Lesson 1: Creating a Report Server Project (Reporting Services) (Lezione 1: Creazione di un progetto server report (Reporting Services)) | Microsoft Docs'
ms.date: 05/01/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: 675671ca-e6c9-48a2-82e9-386778f3a49f
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: c3a32b6b27a8919d729c95bfe29f50c2bda81db8
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 05/06/2019
ms.locfileid: "65095849"
---
# <a name="lesson-1-creating-a-report-server-project-reporting-services"></a>Lezione 1: Creazione di un progetto server report (Reporting Services)

In questa lezione si creano un *progetto server di report* e un file di *definizione del report (con estensione rdl)* usando *Progettazione report*.

> [!NOTE]
> [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] è un ambiente [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] per la creazione di soluzioni di Business Intelligence. SSDT vanta l'ambiente di creazione Progettazione report in cui è possibile aprire, modificare, visualizzare in anteprima, salvare e distribuire definizioni impaginate di [!INCLUDE[ssrsnoversion_md](../includes/ssrsnoversion-md.md)] , origini dati condivise, set di dati condivisi e parti di report.

Quando si creano report con Progettazione report, viene creato un progetto server di report contenente i file di report e gli altri file di risorse usati dai report.

## <a name="to-create-a-report-server-project"></a>Per creare un progetto server di report
  
1. Scegliere **Nuovo** > **Progetto** dal menu **File**.  

    ![ssrs-ssdt-file-01-new-project](../reporting-services/media/ssrs-ssdt-file-01-new-project.png)
  
2. Nella colonna più a sinistra selezionare **Reporting Services** sotto **Installati**. In alcuni casi si può trovare nel gruppo **Business Intelligence**.

    ![select-report-server-project-template](../reporting-services/media/lesson-1-creating-a-report-server-project-reporting-services/select-report-server-project-template.png)

    > [!IMPORTANT]
    > Per Visual Studio, se Reporting Services non è disponibile nella colonna a sinistra, aggiungere Progettazione report installando il carico di lavoro SSDT. Scegliere **Ottieni strumenti e funzionalità** dal menu **Strumenti** e quindi selezionare **SQL Server Data Tools** nei carichi di lavoro visualizzati. Se nella colonna centrale non vengono visualizzati gli oggetti Reporting Services, aggiungere le estensioni di Reporting Services. Scegliere **Estensioni e aggiornamenti** > **Online** dal menu **Strumenti**. Nella colonna centrale selezionare **Microsoft Reporting Services Projects** (Progetti di Microsoft Reporting Services) > **Download** nelle estensioni visualizzate. Per SSDT, vedere [Scaricare SQL Server Data Tools (SSDT)](../ssdt/download-sql-server-data-tools-ssdt.md).

3. Selezionare l'icona di **Progetto server di report** &nbsp;&nbsp;![ssrs_ssdt_report_server_project](media/ssrs-ssdt-report-server-project.png) &nbsp;&nbsp;nella colonna centrale della finestra di dialogo **Nuovo progetto**.

4. Nella casella di testo **Nome** digitare "Tutorial" come nome del progetto. Per impostazione predefinita, nella casella di testo **Percorso** viene visualizzato il percorso della cartella "Documenti\Visual Studio 20xx\Projects\". Progettazione report crea una cartella denominata Tutorial in questo percorso e il progetto Tutorial in tale cartella. Se il progetto non appartiene a una soluzione di Visual Studio, Visual Studio crea anche un file di soluzione con estensione sln.

5. Selezionare **OK** per creare il progetto. Il progetto Tutorial verrà visualizzato nel riquadro **Esplora soluzioni** a destra.
  
## <a name="creating-a-report-definition-file-rdl"></a>Creazione di un file di definizione del report (RDL)  
  
1. Nel riquadro **Esplora soluzioni** fare clic con il pulsante destro del mouse sulla cartella **Report**. Se il riquadro **Esplora soluzioni** non è visualizzato, scegliere **Esplora soluzioni** dal menu **Visualizza**.

2. Scegliere **Aggiungi** > **Nuovo elemento**.

    ![ssrs_ssdt_add_report](../reporting-services/media/ssrs-ssdt-add-report.png)

3. Nella finestra **Aggiungi nuovo elemento** selezionare l'icona **Report**.

4. Digitare "Sales Orders.rdl" nella casella di testo **Nome**.

5. Selezionare il pulsante **Aggiungi** in basso a destra nella finestra di dialogo **Aggiungi nuovo elemento** per completare il processo. Il nuovo file di report Sales Orders verrà aperto in Progettazione report nella visualizzazione Progettazione.

    ![ssrs-ssdt-01-new-report-designer](media/ssrs-ssdt-01-new-report-designer.png)

## <a name="next-steps"></a>Passaggi successivi

Sono stati così creati il progetto report Tutorial e il report Sales Orders. Nelle lezioni rimanenti verranno illustrate le procedure per:

- Configurare un'origine dati per il report
- Creare un set di dati dall'origine dati
- Progettare e formattare il layout del report

Passare a [Lezione 2: Specifica delle informazioni di connessione &#40;Reporting Services&#41;](../reporting-services/lesson-2-specifying-connection-information-reporting-services.md).
