---
title: Interfaccia utente di Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Integration Services, SSIS Designer
- tools [Integration Services], SSIS Designer
- SSIS Designer
- SSIS, SSIS Designer
- Integration Services, SSIS Designer
ms.assetid: d2c48cff-46f4-4c70-b1f3-c88f9b8757f3
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 55b09057927fa9c5102b8d816c42e1741bc0883a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/25/2020
ms.locfileid: "62767673"
---
# <a name="integration-services-user-interface"></a>Interfaccia utente di Integration Services
  Oltre alle aree di progettazione disponibili nelle schede di Progettazione [!INCLUDE[ssIS](../includes/ssis-md.md)] , l'interfaccia utente consente l'accesso alle seguenti finestre e finestre di dialogo per l'aggiunta di funzionalità ai pacchetti e per la configurazione delle proprietà degli oggetti di pacchetto:  
  
-   Finestre e finestre di dialogo che consentono di aggiungere ai pacchetti configurazioni e funzionalità, ad esempio la registrazione.  
  
-   Editor personalizzati per la configurazione delle proprietà degli oggetti di pacchetto. Quasi ogni tipo di contenitore, attività e flusso di dati dispone di un proprio editor personalizzato.  
  
-   Finestra di dialogo **Editor avanzato** , un editor generico che offre opzioni di configurazione più dettagliate per molti componenti flusso di dati.  
  
 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] sono inoltre disponibili finestre e finestre di dialogo per la configurazione dell'ambiente e l'uso dei pacchetti.  
  
## <a name="dialog-boxes-and-windows"></a>Finestre e finestre di dialogo  
 Dopo l'apertura o la creazione di un pacchetto in Progettazione [!INCLUDE[ssIS](../includes/ssis-md.md)] sono disponibili le finestre e finestre di dialogo seguenti.  
  
 In questa tabella vengono elencate le finestre di dialogo a cui è possibile accedere dal menu **SSIS** e dalle aree di progettazione di Progettazione [!INCLUDE[ssIS](../includes/ssis-md.md)] .  
  
|Finestra di dialogo|Scopo|Accesso|  
|----------------|-------------|------------|  
|**Per iniziare**|Consente di accedere a esempi, esercitazioni e video.|Nell'area di progettazione della scheda **Flusso di controllo** o **Flusso di dati** fare clic con il pulsante destro del mouse e scegliere **Attività iniziali**.<br /><br /> Per visualizzare automaticamente la finestra **Attività iniziali** quando si crea un nuovo progetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , selezionare **Always show in new project** (Mostra sempre nel nuovo progetto) nella parte inferiore della finestra.|  
|**Configura log SSIS**|Consente di configurare la registrazione per un pacchetto e le relative attività, tramite l'aggiunta di log e l'impostazione dei dettagli di registrazione.|Scegliere **Registrazione** dal menu **SSIS**.<br /><br /> -oppure-<br /><br /> Fare clic con il pulsante destro del mouse nell'area di progettazione della scheda **Flusso di controllo** e quindi scegliere **Registrazione**.|  
|**Libreria configurazioni pacchetto**|Consente di aggiungere e modificare le configurazioni dei pacchetti. Da questa finestra di dialogo è possibile eseguire Configurazione guidata pacchetto.|Scegliere **Configurazioni pacchetto** dal menu **SSIS**.<br /><br /> -oppure-<br /><br /> Fare clic con il pulsante destro del mouse nell'area di progettazione della scheda **Flusso di controllo** e scegliere **Configurazioni pacchetto**.|  
|**Firma digitale**|Consente di firmare o rimuovere la firma da un pacchetto.|Scegliere **Firma digitale** dal menu **SSIS**.<br /><br /> -oppure-<br /><br /> Fare clic con il pulsante destro del mouse nell'area di progettazione della scheda **Flusso di controllo** e quindi scegliere **Firma digitale**.|  
|**Impostare punti di interruzione**|Consente di attivare punti di interruzione sulle attività e impostarne le proprietà.|Nell'area di progettazione della scheda **Flusso di controllo** fare clic con il pulsante destro del mouse su un'attività o contenitore e quindi scegliere **Modifica punti di interruzione**. Per impostare un punto di interruzione per il pacchetto, fare clic con il pulsante destro del mouse nell'area di progettazione della scheda **Flusso di controllo** , quindi scegliere **Modifica punti di interruzione**.|  
  
 Nella finestra **Attività iniziali** sono disponibili collegamenti a esempi, esercitazioni e video. Per aggiungere collegamenti ad altro contenuto, modificare il file SamplesSites.xml incluso nella versione corrente di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]. È consigliabile non modificare il valore dell'elemento \<GettingStartedSamples> che specifica l'URL del feed RSS. Il file si trova nella cartella *\<unità>* :\Programmi\Microsoft SQL Server\110\DTS\Binn. In un computer a 64 bit il file si trova nella cartella *\<unità>* :\Programmi (x86)\Microsoft SQL Server\110\DTS\Binn  
  
 Se il file SamplesSites.xml è danneggiato, sostituire il codice xml nel file con il codice xml predefinito seguente.  
  
 `<?xml version="1.0" ?>`  
  
 `- <SamplesSites>`  
  
 `<GettingStartedSamples>https://go.microsoft.com/fwlink/?LinkID=203147</GettingStartedSamples>`  
  
 `- <ToolboxSamples>`  
  
 `<Site>https://go.microsoft.com/fwlink/?LinkID=203286&query=SSIS%20{0}</Site>`  
  
 `</ToolboxSamples>`  
  
 `</SamplesSites>`  
  
 In questa tabella vengono elencate le finestre a cui è possibile accedere dai menu **SSIS** e **Visualizza** , nonché dalle aree di progettazione di Progettazione [!INCLUDE[ssIS](../includes/ssis-md.md)] .  
  
|Finestra|Scopo|Accesso|  
|------------|-------------|------------|  
|**Variabili**|Consente di aggiungere e gestire variabili personalizzate.|Scegliere **Variabili** dal menu **SSIS**.<br /><br /> -oppure-<br /><br /> Fare clic con il pulsante destro del mouse nell'area di progettazione della scheda **Flusso di controllo** o **Flusso di dati** e quindi scegliere **Variabili**.<br /><br /> -oppure-<br /><br /> Scegliere **Altre finestre** dal menu **Visualizza**e quindi fare clic su **Variabili**.|  
|**Registra eventi**|Consente di visualizzare le voci di log durante la fase di esecuzione.|Scegliere **Registra eventi** dal menu **SSIS**.<br /><br /> -oppure-<br /><br /> Fare clic con il pulsante destro del mouse nell'area di progettazione della scheda **Flusso di controllo** o **Flusso di dati** e quindi scegliere **Registra eventi**.<br /><br /> -oppure-<br /><br /> Scegliere **Altre finestre** dal menu **Visualizza**e quindi fare clic su **Registra eventi**.|  
  
## <a name="custom-editors"></a>Editor personalizzati  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] include finestre di dialogo personalizzate per la maggior parte dei contenitori, delle attività, delle origini, delle trasformazioni e delle destinazioni.  
  
 Nella tabella seguente viene descritto come accedere alle finestre di dialogo personalizzate.  
  
|Tipo di editor|Accesso|  
|-----------------|------------|  
|Contenitore. Per altre informazioni, vedere [Contenitori in Integration Services](control-flow/integration-services-containers.md).|Nell'area di progettazione della scheda **Flusso di controllo** fare doppio clic sul contenitore.|  
|Attività. Per altre informazioni, vedere [Attività di Integration Services](control-flow/integration-services-tasks.md).|Nell'area di progettazione della scheda **Flusso di controllo** fare doppio clic sull'attività.|  
|Origine.|Nell'area di progettazione della scheda **Flusso di dati** fare doppio clic sull'origine.|  
|Trasformazione. Per altre informazioni, vedere [Trasformazioni di Integration Services](data-flow/transformations/integration-services-transformations.md).|Nell'area di progettazione della scheda **Flusso di dati** fare doppio clic sulla trasformazione.|  
|Destinazione.|Nell'area di progettazione della scheda **Flusso di dati** fare doppio clic sulla destinazione.|  
  
## <a name="advanced-editor"></a>Editor avanzato  
 La finestra di dialogo **Editor avanzato** è un'interfaccia utente per la configurazione dei componenti flusso di dati. Elenca le proprietà del componente utilizzando un layout generico. La finestra di dialogo **Editor avanzato** non è disponibile per le trasformazioni di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] che includono più input.  
  
 Per aprire questo editor, fare clic su **Visualizza editor avanzato** nella finestra **Proprietà** oppure fare clic con il pulsante destro del mouse su un componente flusso di dati e quindi scegliere **Visualizza editor avanzato**.  
  
 Se si crea un'origine, una trasformazione o una destinazione personalizzata, ma non si desidera generare un'interfaccia utente personalizzata, è possibile usare la finestra di dialogo **Editor avanzato** .  
  
## <a name="sql-server-data-tools-features"></a>Funzionalità di SQL Server Data Tools  
 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] sono inclusi finestre, finestre di dialogo e comandi di menu per l'uso di pacchetti di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
 Nell'elenco seguente vengono riepilogati le finestre e i menu disponibili:  
  
-   Nella finestra **Esplora soluzioni** vengono elencati i progetti, compreso il progetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] da usare per lo sviluppo dei pacchetti di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , e i file di progetto.  
  
     Per ordinare per nome i pacchetti contenuti in un progetto, fare clic con il pulsante destro del mouse sul nodo **Pacchetti SSIS** , quindi scegliere **Ordina per nome**.  
  
-   Nella **Casella degli strumenti** vengono elencati gli elementi dei flussi di controllo e dei flussi di dati da usare per la compilazione dei flussi.  
  
-   Nella finestra **Proprietà** vengono elencate le proprietà degli oggetti.  
  
-   Il menu **Formato** include opzioni per il ridimensionamento e l'allineamento dei controlli in un pacchetto.  
  
-   Il menu **Modifica** include funzionalità di copia e incolla che consentono di copiare oggetti nelle aree di progettazione.  
  
-   Il menu **Visualizza** include opzioni che consentono di modificare la rappresentazione grafica degli oggetti in Progettazione [!INCLUDE[ssIS](../includes/ssis-md.md)]  
  
 Per ulteriori informazioni su altri menu e finestre, vedere la documentazione di Visual Studio.  
  
## <a name="related-tasks"></a>Attività correlate  
 Per informazioni su come creare pacchetti in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], vedere [Creare pacchetti in SQL Server Data Tools](create-packages-in-sql-server-data-tools.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Progettazione SSIS](ssis-designer.md)  
  
  
