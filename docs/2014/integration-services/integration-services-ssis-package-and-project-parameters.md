---
title: Parametri (SSIS) di Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 9ed9ca8e-8b1e-48d9-907d-285516d6562b
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: cfd6a65e1561f252574ff919c8b63b0bbd57876f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62892246"
---
# <a name="integration-services-ssis-parameters"></a>Parametri di Integration Services (SSIS)
  I parametri (SSIS) di[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] consentono di assegnare valori alle proprietà incluse nei pacchetti durante la fase di esecuzione. È possibile creare *parametri di progetto* al livello del progetto e *parametri di pacchetto* al livello del pacchetto. I parametri del progetto vengono utilizzati per fornire input esterno ricevuto dal progetto a uno o più pacchetti nel progetto. I parametri del pacchetto consentono di modificare l'esecuzione del pacchetto senza doverlo modificare e ridistribuire.  
  
 In [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] è possibile creare, modificare o eliminare i parametri di progetto utilizzando la finestra **Project.params** . Per creare, modificare ed eliminare i parametri di pacchetto, utilizzare la scheda **Parametri** in Progettazione [!INCLUDE[ssIS](../includes/ssis-md.md)] . Per associare un parametro nuovo o esistente a una proprietà di un'attività, utilizzare la finestra di dialogo **Imposta parametri** . Per altre informazioni sull'utilizzo della finestra **Project.params** e della scheda **Parametri** , vedere [Create Parameters](create-parameters.md). Per altre informazioni sulla finestra di dialogo **Imposta parametri** , vedere [Parameterize Dialog Box](parameterize-dialog-box.md).  
  
## <a name="parameters-and-package-deployment-model"></a>Parametri e modello di distribuzione del pacchetto  
 In generale, se un pacchetto viene distribuito mediante il relativo modello di distribuzione, è necessario utilizzare le configurazioni anziché i parametri.  
  
 Quando si distribuisce un pacchetto che contiene parametri utilizzando il modello di distribuzione del pacchetto e quindi si esegue il pacchetto, i parametri non vengono chiamati durante l'esecuzione. Se il pacchetto contiene espressioni e parametri di pacchetto all'interno del pacchetto, utilizzare i parametri per applicare i valori risultanti in fase di esecuzione. Se il pacchetto contiene parametri di progetto, è possibile che l'esecuzione del pacchetto non venga completata.  
  
## <a name="parameters-and-project-deployment-model"></a>Parametri e modello di distribuzione del progetto  
 Quando si distribuisce un progetto nel server [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , è possibile utilizzare viste, stored procedure e l'interfaccia utente di [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] per gestire i parametri di progetto e di pacchetto. Per ulteriori informazioni, vedere gli argomenti seguenti.  
  
-   [Viste &#40;catalogo di Integration Services&#41;](/sql/integration-services/system-views/views-integration-services-catalog)  
  
-   [Stored procedure &#40;catalogo di Integration Services&#41;](/sql/integration-services/system-stored-procedures/stored-procedures-integration-services-catalog)  
  
-   [Finestra di dialogo Configura](catalog/configure-dialog-box.md)  
  
-   [Finestra di dialogo Esecuzione pacchetto](../../2014/integration-services/execute-package-dialog-box.md)  
  
### <a name="parameter-values"></a>Valori di parametri  
 È possibile assegnare fino a tre tipi diversi di valori a un parametro. Quando viene avviata l'esecuzione di un pacchetto, viene utilizzato un solo valore per il parametro e il parametro viene risolto nel relativo valore letterale finale.  
  
 Nella tabella riportata di seguito sono elencati i tipi di valori.  
  
|Nome del valore|Descrizione|Tipo di valore|  
|----------------|-----------------|-------------------|  
|Valore di esecuzione|Valore assegnato a un'istanza specifica di esecuzione del pacchetto. Questa assegnazione esegue l'override di tutti gli altri valori, tuttavia è applicabile a una sola istanza di esecuzione del pacchetto.|Valore letterale|  
|Valore del server|Valore assegnato al parametro nell'ambito del progetto, dopo la distribuzione di quest'ultimo nel server [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . Questo valore esegue l'override del valore predefinito di progettazione.|Valore letterale o riferimento a una variabile di ambiente|  
|Valore di progettazione|Valore assegnato al parametro durante la creazione o modifica del progetto in [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]. Questo valore rimane persistente nel progetto.|Valore letterale|  
  
 È possibile utilizzare un solo parametro per assegnare un valore a più proprietà del pacchetto. A una singola proprietà del pacchetto è possibile assegnare un valore solo da un singolo parametro.  
  
###  <a name="executions"></a> Esecuzioni e valori dei parametri  
 L' *esecuzione* è un oggetto che rappresenta una singola istanza di esecuzione del pacchetto. Quando si crea un'esecuzione, è possibile specificare tutti i dettagli necessari per l'esecuzione di un pacchetto, ad esempio i valori dei parametri di esecuzione. Inoltre, è possibile modificare i valori dei parametri per le esecuzioni esistenti.  
  
 Quando si imposta in modo esplicito un valore del parametro di esecuzione, tale valore è applicabile unicamente a quell'istanza particolare di esecuzione. Anziché un valore del server o un valore di progettazione viene utilizzato un valore di esecuzione. Se non si imposta in modo esplicito un valore di esecuzione ed è stato specificato un valore del server, viene utilizzato quest'ultimo.  
  
 Se un parametro è contrassegnato come obbligatorio, è necessario specificare per tale parametro un valore del server o un valore di esecuzione. In caso contrario, il pacchetto corrispondente non viene eseguito. Sebbene al parametro sia associato un valore predefinito in fase di progettazione, non sarà mai utilizzato dopo la distribuzione del progetto.  
  
#### <a name="environment-variables"></a>Variabili di ambiente  
 Se un parametro fa riferimento a una variabile di ambiente, il valore letterale di tale variabile viene risolto attraverso il riferimento all'ambiente specificato e applicato al parametro. Il valore del parametro letterale finale utilizzato per l'esecuzione del pacchetto è definito valore del parametro di esecuzione. Il riferimento all'ambiente per un'esecuzione viene specificato tramite la finestra di dialogo **Esegui** .  
  
 Se un parametro del progetto fa riferimento a una variabile di ambiente e il valore letterale della variabile non può essere risolto in fase di esecuzione, viene utilizzato il valore di progettazione. Il valore del server non viene utilizzato.  
  
 Per visualizzare le variabili di ambiente assegnate ai valori del parametro, eseguire una query sulla vista catalog.object_parameters. Per altre informazioni, vedere [catalog.object_parameters &#40;database SSISDB&#41;](/sql/integration-services/system-views/catalog-object-parameters-ssisdb-database).  
  
#### <a name="determining-execution-parameter-values"></a>Determinazione dei valori dei parametri di esecuzione  
 Le stored procedure e le viste Transact-SQL seguenti possono essere utilizzate per visualizzare e impostare i valori di parametri.  
  
 [catalog.execution_parameter_values &#40;database SSISDB&#41;](/sql/integration-services/system-views/catalog-execution-parameter-values-ssisdb-database)(vista)  
 Consente di visualizzare i valori di parametri effettivi che verranno utilizzati da un'esecuzione specifica  
  
 [catalog.get_parameter_values &#40;database SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-get-parameter-values-ssisdb-database) (stored procedure)  
 Consente di risolvere e visualizzare i valori effettivi per il riferimento all'ambiente e al pacchetto specificato  
  
 [catalog.object_parameters &#40;database SSISDB&#41;](/sql/integration-services/system-views/catalog-object-parameters-ssisdb-database) (vista)  
 Consente di visualizzare i parametri e le proprietà per tutti i pacchetti e i progetti nel catalogo di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , inclusi i valori predefiniti del server e i valori predefiniti di progettazione.  
  
 [catalog.set_execution_parameter_value &#40;database SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database)  
 Imposta il valore di un parametro per un'istanza di esecuzione nel catalogo di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
 È inoltre possibile utilizzare la finestra di dialogo **Esegui pacchetto** in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] per modificare il valore di un parametro. Per altre informazioni, vedere [Execute Package Dialog Box](../../2014/integration-services/execute-package-dialog-box.md).  
  
 È inoltre possibile utilizzare l'opzione dtexec `/Parameter` per modificare il valore di un parametro. Per altre informazioni, vedere [dtexec Utility](packages/dtexec-utility.md).  
  
### <a name="parameter-validation"></a>Convalida dei parametri  
 Se i valori dei parametri non possono essere risolti, il pacchetto corrispondente non viene eseguito. Per evitare errori, è possibile convalidare progetti e pacchetti mediante la finestra di dialogo **Convalida** in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Tramite la convalida è possibile confermare che tutti i parametri dispongono dei valori necessari o che possono risolvere i valori necessari con riferimenti all'ambiente specifici. Durante la convalida vengono inoltre verificati altri problemi comuni relativi ai pacchetti.  
  
 Per altre informazioni, vedere [Validate Dialog Box](catalog/validate-dialog-box.md).  
  
### <a name="parameter-example"></a>Esempio di parametro  
 In questo esempio viene descritto un parametro denominato **pkgOptions** utilizzato per specificare opzioni per il pacchetto in cui risiede.  
  
 Durante la fase di progettazione, quando il parametro è stato creato in [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], il valore predefinito 1 è stato assegnato al parametro. Questo valore predefinito è noto come valore predefinito di progettazione. Se il progetto è stato distribuito nel catalogo SSISDB e non sono stati assegnati altri valori al parametro, durante l'esecuzione del pacchetto alla proprietà del pacchetto corrispondente al parametro **pkgOptions** verrà assegnato il valore 1. Il valore predefinito di progettazione viene reso persistente nel progetto per tutto il ciclo di vita.  
  
 Durante la preparazione di un'istanza specifica di esecuzione del pacchetto, il valore 5 viene assegnato al parametro **pkgOptions** . A questo valore viene fatto riferimento come valore di esecuzione perché si applica al parametro solo per quell'istanza specifica dell'esecuzione. All'avvio dell'esecuzione, alla proprietà del pacchetto corrispondente al parametro **pkgOptions** viene assegnato il valore 5.  
  
## <a name="related-tasks"></a>Attività correlate  
 [Crea parametri](create-parameters.md)  
  
 [Impostare i valori dei parametri dopo la distribuzione del progetto](../../2014/integration-services/set-parameter-values-after-the-project-is-deployed.md)  
  
## <a name="related-content"></a>Contenuto correlato  
 Post di blog [SSIS Quick Tip: Required Parameters](https://go.microsoft.com/fwlink/?LinkId=239781) (Suggerimenti rapido per SSIS: parametri necessari) nel sito Web mattmasson.com.  
  
  
