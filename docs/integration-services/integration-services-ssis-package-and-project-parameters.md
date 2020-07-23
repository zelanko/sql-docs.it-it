---
title: Parametri del pacchetto e del progetto | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.designer.parameter.f1
- sql13.dts.designer.parameterwindow.f1
ms.assetid: 9ed9ca8e-8b1e-48d9-907d-285516d6562b
author: chugugrace
ms.author: chugu
ms.openlocfilehash: de9ceed1aa019b82bc943a1985f0f251ad82b1fa
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/22/2020
ms.locfileid: "86917530"
---
# <a name="integration-services-ssis-package-and-project-parameters"></a>Parametri del pacchetto e del progetto di Integration Services (SSIS)

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]


  I parametri (SSIS) di[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] consentono di assegnare valori alle proprietà incluse nei pacchetti durante la fase di esecuzione. È possibile creare *parametri di progetto* al livello del progetto e *parametri di pacchetto* al livello del pacchetto. I parametri del progetto vengono utilizzati per fornire input esterno ricevuto dal progetto a uno o più pacchetti nel progetto. I parametri del pacchetto consentono di modificare l'esecuzione del pacchetto senza doverlo modificare e ridistribuire.  
  
 In [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] è possibile creare, modificare o eliminare i parametri di progetto utilizzando la finestra **Project.params** . Per creare, modificare ed eliminare i parametri di pacchetto, utilizzare la scheda **Parametri** in Progettazione [!INCLUDE[ssIS](../includes/ssis-md.md)] . Per associare un parametro nuovo o esistente a una proprietà di un'attività, utilizzare la finestra di dialogo **Imposta parametri** . Per altre informazioni sull'utilizzo della finestra **Project.params** e della scheda **Parametri** , vedere [Create Parameters](https://msdn.microsoft.com/library/cd5d675b-dd5d-49cc-8b1f-dc717a973f99). Per altre informazioni sulla finestra di dialogo **Imposta parametri** , vedere [Parameterize Dialog Box](https://msdn.microsoft.com/library/fac02b6d-d247-447a-8940-e8700c7ac350).  
  
## <a name="parameters-and-package-deployment-model"></a>Parametri e modello di distribuzione del pacchetto  
 In generale, se un pacchetto viene distribuito mediante il relativo modello di distribuzione, è necessario utilizzare le configurazioni anziché i parametri.  
  
 Quando si distribuisce un pacchetto che contiene parametri utilizzando il modello di distribuzione del pacchetto e quindi si esegue il pacchetto, i parametri non vengono chiamati durante l'esecuzione. Se il pacchetto contiene espressioni e parametri di pacchetto all'interno del pacchetto, utilizzare i parametri per applicare i valori risultanti in fase di esecuzione. Se il pacchetto contiene parametri di progetto, è possibile che l'esecuzione del pacchetto non venga completata.  
  
## <a name="parameters-and-project-deployment-model"></a>Parametri e modello di distribuzione del progetto  
 Quando si distribuisce un progetto nel server Integration Services (SSIS), è possibile usare viste, stored procedure e l'interfaccia utente di [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] per gestire i parametri di progetto e di pacchetto. Per ulteriori informazioni, vedere gli argomenti seguenti.  
  
-   [Viste &#40;catalogo di Integration Services&#41;](../integration-services/system-views/views-integration-services-catalog.md)  
  
-   [Stored procedure &#40;catalogo di Integration Services&#41;](../integration-services/system-stored-procedures/stored-procedures-integration-services-catalog.md)  
  
-   [Finestra di dialogo Configura](../integration-services/service/configure-dialog-box.md)  
  
-   [Finestra di dialogo Esecuzione pacchetto](../integration-services/packages/run-integration-services-ssis-packages.md#execute_package_dialog)  
  
### <a name="parameter-values"></a>Valori di parametri  
 È possibile assegnare fino a tre tipi diversi di valori a un parametro. Quando viene avviata l'esecuzione di un pacchetto, viene utilizzato un solo valore per il parametro e il parametro viene risolto nel relativo valore letterale finale.  
  
 Nella tabella riportata di seguito sono elencati i tipi di valori.  
  
|Nome del valore|Descrizione|Tipo di valore|  
|----------------|-----------------|-------------------|  
|Valore di esecuzione|Valore assegnato a un'istanza specifica di esecuzione del pacchetto. Questa assegnazione esegue l'override di tutti gli altri valori, tuttavia è applicabile a una sola istanza di esecuzione del pacchetto.|Literal (Valore letterale)|  
|Valore del server|Valore assegnato al parametro nell'ambito del progetto, dopo la distribuzione del progetto nel server Integration Services. Questo valore esegue l'override del valore predefinito di progettazione.|Valore letterale o riferimento a una variabile di ambiente|  
|Valore di progettazione|Valore assegnato al parametro durante la creazione o modifica del progetto in [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]. Questo valore rimane persistente nel progetto.|Literal (Valore letterale)|  
  
 È possibile utilizzare un solo parametro per assegnare un valore a più proprietà del pacchetto. A una singola proprietà del pacchetto è possibile assegnare un valore solo da un singolo parametro.  
  
###  <a name="executions-and-parameter-values"></a><a name="executions"></a> Esecuzioni e valori dei parametri  
 L' *esecuzione* è un oggetto che rappresenta una singola istanza di esecuzione del pacchetto. Quando si crea un'esecuzione, è possibile specificare tutti i dettagli necessari per l'esecuzione di un pacchetto, ad esempio i valori dei parametri di esecuzione. Inoltre, è possibile modificare i valori dei parametri per le esecuzioni esistenti.  
  
 Quando si imposta in modo esplicito un valore del parametro di esecuzione, tale valore è applicabile unicamente a quell'istanza particolare di esecuzione. Anziché un valore del server o un valore di progettazione viene utilizzato un valore di esecuzione. Se non si imposta in modo esplicito un valore di esecuzione ed è stato specificato un valore del server, viene utilizzato quest'ultimo.  
  
 Se un parametro è contrassegnato come obbligatorio, è necessario specificare per tale parametro un valore del server o un valore di esecuzione. In caso contrario, il pacchetto corrispondente non viene eseguito. Sebbene al parametro sia associato un valore predefinito in fase di progettazione, non sarà mai utilizzato dopo la distribuzione del progetto.  
  
#### <a name="environment-variables"></a>Variabili di ambiente  
 Se un parametro fa riferimento a una variabile di ambiente, il valore letterale di tale variabile viene risolto attraverso il riferimento all'ambiente specificato e applicato al parametro. Il valore del parametro letterale finale utilizzato per l'esecuzione del pacchetto è definito valore del parametro di esecuzione. Il riferimento all'ambiente per un'esecuzione viene specificato tramite la finestra di dialogo **Esegui** .  
  
 Se un parametro del progetto fa riferimento a una variabile di ambiente e il valore letterale della variabile non può essere risolto in fase di esecuzione, viene utilizzato il valore di progettazione. Il valore del server non viene utilizzato.  
  
 Per visualizzare le variabili di ambiente assegnate ai valori del parametro, eseguire una query sulla vista catalog.object_parameters. Per altre informazioni, vedere [catalog.object_parameters &#40;database SSISDB&#41;](../integration-services/system-views/catalog-object-parameters-ssisdb-database.md).  
  
#### <a name="determining-execution-parameter-values"></a>Determinazione dei valori dei parametri di esecuzione  
 Le stored procedure e le viste Transact-SQL seguenti possono essere utilizzate per visualizzare e impostare i valori di parametri.  
  
 [catalog.execution_parameter_values &#40;database SSISDB&#41;](../integration-services/system-views/catalog-execution-parameter-values-ssisdb-database.md)(vista)  
 Consente di visualizzare i valori di parametri effettivi che verranno utilizzati da un'esecuzione specifica  
  
 [catalog.get_parameter_values &#40;database SSISDB&#41;](../integration-services/system-stored-procedures/catalog-get-parameter-values-ssisdb-database.md) (stored procedure)  
 Consente di risolvere e visualizzare i valori effettivi per il riferimento all'ambiente e al pacchetto specificato  
  
 [catalog.object_parameters &#40;database SSISDB&#41;](../integration-services/system-views/catalog-object-parameters-ssisdb-database.md) (vista)  
 Consente di visualizzare i parametri e le proprietà per tutti i pacchetti e i progetti nel catalogo di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , inclusi i valori predefiniti del server e i valori predefiniti di progettazione.  
  
 [catalog.set_execution_parameter_value &#40;database SSISDB&#41;](../integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md)  
 Imposta il valore di un parametro per un'istanza di esecuzione nel catalogo di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
 È inoltre possibile utilizzare la finestra di dialogo **Esegui pacchetto** in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] per modificare il valore di un parametro. Per altre informazioni, vedere [Execute Package Dialog Box](../integration-services/packages/run-integration-services-ssis-packages.md#execute_package_dialog).  
  
 È inoltre possibile utilizzare l'opzione dtexec **/Parameter** per modificare il valore di un parametro. Per altre informazioni, vedere [dtexec Utility](../integration-services/packages/dtexec-utility.md).  
  
### <a name="parameter-validation"></a>Convalida dei parametri  
 Se i valori dei parametri non possono essere risolti, il pacchetto corrispondente non viene eseguito. Per evitare errori, è possibile convalidare progetti e pacchetti mediante la finestra di dialogo **Convalida** in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Tramite la convalida è possibile confermare che tutti i parametri dispongono dei valori necessari o che possono risolvere i valori necessari con riferimenti all'ambiente specifici. Durante la convalida vengono inoltre verificati altri problemi comuni relativi ai pacchetti.  
  
 Per altre informazioni, vedere [Validate Dialog Box](../integration-services/service/validate-dialog-box.md).  
  
### <a name="parameter-example"></a>Esempio di parametro  
 In questo esempio viene descritto un parametro denominato **pkgOptions** utilizzato per specificare opzioni per il pacchetto in cui risiede.  
  
 Durante la fase di progettazione, quando il parametro è stato creato in [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], il valore predefinito 1 è stato assegnato al parametro. Questo valore predefinito è noto come valore predefinito di progettazione. Se il progetto è stato distribuito nel catalogo SSISDB e non sono stati assegnati altri valori al parametro, durante l'esecuzione del pacchetto alla proprietà del pacchetto corrispondente al parametro **pkgOptions** verrà assegnato il valore 1. Il valore predefinito di progettazione viene reso persistente nel progetto per tutto il ciclo di vita.  
  
 Durante la preparazione di un'istanza specifica di esecuzione del pacchetto, il valore 5 viene assegnato al parametro **pkgOptions** . A questo valore viene fatto riferimento come valore di esecuzione perché si applica al parametro solo per quell'istanza specifica dell'esecuzione. All'avvio dell'esecuzione, alla proprietà del pacchetto corrispondente al parametro **pkgOptions** viene assegnato il valore 5.  
  
## <a name="create-parameters"></a>Creare un parametro
Usare [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] per creare parametri di progetto e parametri di pacchetto. Le procedure riportate di seguito contengono istruzioni dettagliate per la creazione di parametri di pacchetto/progetto.  
  
> **NOTA:** Se si converte un progetto creato con una versione precedente di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] nel modello di distribuzione del progetto, è possibile usare la **Conversione guidata progetto di Integration Services** per creare parametri basati su configurazioni. Per altre informazioni, vedere [Distribuire progetti e pacchetti di Integration Services (SSIS)](../integration-services/packages/deploy-integration-services-ssis-projects-and-packages.md).  
  
### <a name="create-package-parameters"></a>Creare parametri del pacchetto  
  
1.  Aprire il pacchetto in [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] e quindi fare clic sulla scheda **Parametri** in Progettazione SSIS.  
  
     ![Scheda Parametri del pacchetto](../integration-services/media/denali-package-parameters.gif "Scheda Parametri del pacchetto")  
  
2.  Fare clic sul pulsante **Aggiungi parametro** sulla barra degli strumenti.  
  
     ![Pulsante Aggiungi parametro della barra degli strumenti](../integration-services/media/denali-parameter-add.gif "Pulsante Aggiungi parametro della barra degli strumenti")  
  
3.  Immettere i valori per le proprietà **Nome**, **Tipo di dati**, **Valore**, **Sensibile** e **Richiesto** nell'elenco stesso o nella finestra **Proprietà**. Nella tabella seguente vengono descritte tali proprietà.  
  
    |Proprietà|Descrizione|  
    |--------------|-----------------|  
    |Nome|Nome del parametro.|  
    |Tipo di dati|Tipo di dati del parametro.|  
    |Valore predefinito|Valore predefinito del parametro assegnato in fase di progettazione. Noto anche come valore predefinito di progettazione.|  
    |Sensibili|I valori di parametri sensibili sono crittografati nel catalogo e risultano NULL quando vengono visualizzati con Transact-SQL o con SQL Server Management Studio.|  
    |Obbligatoria|Richiede che un valore diverso dal valore predefinito di progettazione venga specificato prima dell'esecuzione del pacchetto.|  
    |Descrizione|Per manutenzione, la descrizione del parametro. In [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], impostare la descrizione del parametro nella finestra Proprietà di Visual Studio quando il parametro viene selezionato nella finestra dei parametri applicabile.|  
  
    > **NOTA:** quando si distribuisce un progetto nel catalogo, molte più proprietà vengono associate al progetto. Per visualizzare tutte le proprietà di tutti i parametri nel catalogo, usare la vista [catalog.object_parameters &#40;database SSISDB&#41;](../integration-services/system-views/catalog-object-parameters-ssisdb-database.md).  
  
4.  Salvare il progetto per salvare le modifiche ai parametri. I valori dei parametri vengono archiviati nel file di progetto.  
  
    > **AVVISO** È possibile modificare direttamente l'elenco oppure usare la finestra **Proprietà** per modificare i valori delle proprietà dei parametri. È possibile eliminare un parametro tramite il pulsante **Elimina (X)** . Utilizzando l'ultimo pulsante della barra degli strumenti, è possibile specificare un valore per un parametro utilizzato solo quando si esegue il pacchetto in [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)].  
  
    > **NOTA:** se si riapre il file di pacchetto senza aprire il progetto in [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], la scheda **Parametri** sarà vuota e disabilitata.  
  
### <a name="create-project-parameters"></a>Creare parametri del progetto  
  
1.  Aprire il progetto in [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)].  
  
2.  Fare clic con il pulsante destro del mouse su **Project.params** in Esplora soluzioni e quindi scegliere **Apri** (OPPURE) fare doppio clic su **Project.params** per aprirlo.  
  
     ![Finestra dei parametri del progetto](../integration-services/media/denali-project-parameters.gif "Finestra dei parametri del progetto")  
  
3.  Fare clic sul pulsante **Aggiungi parametro** sulla barra degli strumenti.  
  
     ![Pulsante Aggiungi parametro della barra degli strumenti](../integration-services/media/denali-parameter-add.gif "Pulsante Aggiungi parametro della barra degli strumenti")  
  
4.  Immettere valori per le proprietà **Nome**, **Tipo di dati**, **Valore**, **Sensibile** e **Richiesto**.  
  
    |Proprietà|Descrizione|  
    |--------------|-----------------|  
    |Nome|Nome del parametro.|  
    |Tipo di dati|Tipo di dati del parametro.|  
    |Valore predefinito|Valore predefinito del parametro assegnato in fase di progettazione. Noto anche come valore predefinito di progettazione.|  
    |Sensibili|I valori di parametri sensibili sono crittografati nel catalogo e risultano NULL quando vengono visualizzati con Transact-SQL o con SQL Server Management Studio.|  
    |Obbligatoria|Richiede che un valore diverso dal valore predefinito di progettazione venga specificato prima dell'esecuzione del pacchetto.|  
    |Descrizione|Per manutenzione, la descrizione del parametro. In [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], impostare la descrizione del parametro nella finestra Proprietà di Visual Studio quando il parametro viene selezionato nella finestra dei parametri applicabile.|  
  
5.  Salvare il progetto per salvare le modifiche ai parametri. I valori dei parametri sono archiviati nelle configurazioni del file di progetto. Salvare il file di progetto per eseguire il commit al disco delle eventuali modifiche apportate ai valori dei parametri.  
  
    > **AVVISO** È possibile modificare direttamente l'elenco oppure usare la finestra **Proprietà** per modificare i valori delle proprietà dei parametri. È possibile eliminare un parametro tramite il pulsante **Elimina (X)** . Usando l'ultimo pulsante della barra degli strumenti per aprire la finestra di dialogo **Gestione dei valori dei parametri**, è possibile specificare un valore per un parametro usato solo quando si esegue il pacchetto in [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)].  
    
## <a name="parameterize-dialog-box"></a>Parameterize Dialog Box
La finestra di dialogo **Imposta parametri** consente di associare un parametro nuovo o esistente a una proprietà di un'attività. È possibile aprire la finestra di dialogo facendo clic con il pulsante destro del mouse su un'attività o sulla scheda Flusso di controllo in Progettazione [!INCLUDE[ssIS](../includes/ssis-md.md)], quindi selezionando **Imposta parametri**. Nell'elenco seguente vengono descritti gli elementi dell'interfaccia utente della finestra di dialogo. Per altre informazioni sui parametri, vedere [Parametri di Integration Services (SSIS)](https://msdn.microsoft.com/library/hh213214.aspx).
  
### <a name="options"></a>Opzioni  
 **Proprietà**  
 Selezionare la proprietà dell'attività che si desidera associare a un parametro. Questo elenco viene popolato con tutte le proprietà che è possibile impostare come parametri.  
  
 **Usa parametro esistente**  
 Selezionare questa opzione per associare la proprietà dell'attività a un parametro esistente, quindi selezionare il parametro dall'elenco a discesa.  
  
 **Non utilizzare il parametro**  
 Selezionare questa opzione per rimuovere un riferimento a un parametro. Il parametro non viene eliminato.  
  
 **Crea nuovo parametro**  
 Selezionare questa opzione per creare un nuovo parametro che si desidera associare alla proprietà dell'attività.  
  
 **Nome**  
 Specificare il nome del parametro che si desidera creare.  
  
 **Descrizione**  
 Specificare la descrizione per il parametro.  
  
 **Valore**  
 Specificare il valore predefinito per il parametro. Definito anche valore predefinito per la progettazione, potrà essere sostituito in seguito in fase di distribuzione.  
  
 **Ambito**  
 Specificare l'ambito del parametro selezionando l'opzione **Progetto** o **Pacchetto**. I parametri del progetto vengono utilizzati per fornire input esterno ricevuto dal progetto a uno o più pacchetti nel progetto. I parametri del pacchetto consentono di modificare l'esecuzione del pacchetto senza doverlo modificare e ridistribuire.  
  
 **Sensibile**  
 Specificare se il parametro è sensibile selezionando o deselezionando la casella di controllo. I valori di parametri sensibili sono crittografati nel catalogo e risultano NULL quando vengono visualizzati con Transact-SQL o con SQL Server Management Studio.  
  
 **Obbligatorio**  
 Specificare se il parametro richiede che un valore diverso dal valore predefinito per la progettazione venga specificato prima dell'esecuzione del pacchetto.  
 
## <a name="set-parameter-values-after-the-project-is-deployed"></a>Impostare i valori dei parametri dopo la distribuzione del progetto
La Distribuzione guidata consente di impostare i valori dei parametri predefiniti quando si distribuisce il progetto nel catalogo. Quando il progetto si trova nel catalogo, è possibile utilizzare Transact-SQL o Esplora oggetti di SQL Server Management Studio (SSMS) per impostare i valori predefiniti del server.  
  
### <a name="set-server-defaults-with-ssms-object-explorer"></a>Impostare i valori predefiniti del server con Esplora oggetti di SSMS  
  
1.  Selezionare e fare clic con il pulsante destro del mouse sul progetto nel nodo **Integration Services**.  
  
2.  Per aprire la finestra di dialogo **Proprietà progetto** fare clic su **Proprietà** .  
  
3.  Aprire la pagina dei parametri facendo clic su **Parametri** in **Selezione pagina**.  
  
4.  Selezionare il parametro desiderato nell'elenco **Parametri** . Nota: la colonna **Contenitore** consente di distinguere tra i parametri del progetto e i parametri del pacchetto.  
  
5.  Nella colonna **Valore** specificare il valore del parametro predefinito del server desiderato.  

### <a name="set-server-defaults-with-transact-sql"></a>Impostare i valori predefiniti del server con Transact-SQL  
 Per impostare valori predefiniti del server con Transact-SQL, usare la stored procedure [catalog.set_object_parameter_value &#40;database SSISDB&#41;](../integration-services/system-stored-procedures/catalog-set-object-parameter-value-ssisdb-database.md). Per visualizzare i valori predefiniti del server corrente, eseguire una query nella vista [catalog.object_parameters &#40;database SSISDB&#41;](../integration-services/system-views/catalog-object-parameters-ssisdb-database.md). Per cancellare un valore predefinito del server, usare la stored procedure [catalog.clear_object_parameter_value &#40;database SSISDB&#41;](../integration-services/system-stored-procedures/catalog-clear-object-parameter-value-ssisdb-database.md).  
  
## <a name="related-content"></a>Contenuto correlato  
 Intervento nel blog riguardante un [suggerimento rapido relativo ai parametri obbligatori in SQL Server Integration Services](https://go.microsoft.com/fwlink/?LinkId=239781)sul sito Web mattmasson.com.  
  
  
