---
title: Editor attività Esegui pacchetto | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.executepackagetask.parameter.F1
- sql12.dts.designer.executepackagetask.package.f1
- sql12.dts.designer.executepackagetask.general.f1
ms.assetid: c2c96b4f-eb10-4d8b-be34-88edfd0785fb
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: ff63c6568f0a34a43caf6765e7e01ce8022e10f0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62769837"
---
# <a name="execute-package-task-editor"></a>Editor attività Esegui pacchetto
  Utilizzare l'editor attività Esegui pacchetto per configurare la relativa attività. L'attività Esegui pacchetto permette di estendere le funzionalità aziendali di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] consentendo ai pacchetti di eseguire altri pacchetti nell'ambito di un flusso di lavoro.  
  
 **Per saperne di più**  
  
-   [Aprire l'editor attività Esegui pacchetto](#open)  
  
-   [Impostare le opzioni nella pagina Generale](#general)  
  
-   [Impostare le opzioni nella pagina Pacchetto](#package)  
  
-   [Impostare le opzioni nella pagina Associazioni di parametro](#parameter)  
  
##  <a name="open"></a> Aprire l'editor attività Esegui pacchetto  
  
1.  Aprire un progetto [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] in [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] contenente un'attività Esegui pacchetto.  
  
2.  Fare clic con il pulsante destro del mouse sull'attività disponibile in Progettazione SSIS, quindi scegliere **Modifica**.  
  
##  <a name="general"></a> Impostare le opzioni nella pagina Generale  
 **Name**  
 Specificare un nome univoco per l'attività Esegui pacchetto. Tale nome viene utilizzato come etichetta nell'icona dell'attività.  
  
> [!NOTE]  
>  I nomi delle attività devono essere univoci all'interno di un pacchetto.  
  
 **Descrizione**  
 Digitare una descrizione dell'attività Esegui pacchetto.  
  
##  <a name="package"></a> Impostare le opzioni nella pagina Pacchetto  
 **ReferenceType**  
 Selezionare **Riferimento al progetto** per pacchetti figlio inclusi nel progetto. Selezionare **Riferimento esterno** per pacchetti figlio posizionati esternamente al pacchetto  
  
> [!NOTE]  
>  L'opzione **ReferenceType** è di sola lettura e viene impostata su **Riferimento esterno** se il progetto in cui è contenuto il pacchetto non è stato convertito nel modello di distribuzione del progetto. Per altre informazioni sulla conversione, vedere [Distribuire progetti nel server Integration Services](../../2014/integration-services/deploy-projects-to-integration-services-server.md).  
  
 **Password**  
 Se il pacchetto figlio è protetto con password, specificare la password del pacchetto figlio oppure fare clic sul pulsante con i puntini di sospensione (...) per creare una nuova password per il pacchetto figlio.  
  
 `ExecuteOutOfProcess`  
 Specificare se il pacchetto figlio viene eseguito nel processo del pacchetto padre o in un processo a parte. Per impostazione predefinita, la proprietà ExecuteOutOfProcess dell'attività Esegui pacchetto è impostata su `False`, e il pacchetto figlio viene eseguito nello stesso processo del pacchetto padre. Se si imposta questa proprietà su `true`, il pacchetto figlio viene eseguito in un processo separato. In questo modo è possibile che l'avvio del pacchetto figlio sia rallentato. Inoltre, se la proprietà viene impostata su `true`, non è possibile eseguire il debug del pacchetto in un'installazione di soli strumenti, ma è necessario installare il prodotto [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]. Per altre informazioni, vedere [Installazione di Integration Services](install-windows/install-integration-services.md).  
  
### <a name="referencetype-dynamic-options"></a>Opzioni dinamiche relative a ReferenceType  
  
#### <a name="referencetype--external-reference"></a>ReferenceType = Riferimento esterno  
 **Percorso**  
 Selezionare il percorso del pacchetto figlio. Per questa proprietà sono disponibili le opzioni elencate nella tabella seguente.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**SQL Server**|Impostare il percorso su un'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].|  
|**File system**|Impostare il percorso sul file system.|  
  
 **Connessione**  
 Selezionare il tipo di posizione di archiviazione del pacchetto figlio.  
  
 **PackageNameReadOnly**  
 Viene visualizzato il nome del pacchetto.  
  
#### <a name="referencetype--project-reference"></a>ReferenceType = Riferimento al progetto  
 **PackageNameFromProjectReference**  
 Selezionare un pacchetto contenuto nel progetto affinché sia considerato il pacchetto figlio.  
  
### <a name="location-dynamic-options"></a>Opzioni dinamiche relative al percorso  
  
#### <a name="location--sql-server"></a>Percorso = SQL Server  
 **Connessione**  
 Selezionare una gestione connessione OLE DB nell'elenco o fare clic su \<**Nuova connessione...**> per creare una nuova gestione connessione.  
  
 **Argomenti correlati:** [Gestione connessione OLE DB](connection-manager/ole-db-connection-manager.md), [Configura gestione connessione OLE DB](../../2014/integration-services/configure-ole-db-connection-manager.md)  
  
 **PackageName**  
 Digitare il nome del pacchetto figlio oppure fare clic sul pulsante con i puntini di sospensione (...) e quindi individuare il pacchetto.  
  
#### <a name="location--file-system"></a>Percorso = File system  
 **Connessione**  
 Selezionare una gestione connessione file nell'elenco o fare clic su \<**Nuova connessione**> per creare una nuova gestione connessione.  
  
 **Argomenti correlati:** [Gestione connessione file](connection-manager/file-connection-manager.md), [Editor gestione connessione file](../../2014/integration-services/file-connection-manager-editor.md)  
  
 **PackageNameReadOnly**  
 Viene visualizzato il nome del pacchetto.  
  
##  <a name="parameter"></a> Impostare le opzioni nella pagina Associazioni di parametro  
 È possibile passare i valori del pacchetto padre o del progetto al pacchetto figlio. Il progetto deve utilizzare il modello di distribuzione del progetto e il pacchetto figlio deve essere contenuto nello stesso progetto in cui è contenuto il pacchetto padre.  
  
 Per informazioni sulla conversione dei progetti nel modello di distribuzione del progetto, vedere [Distribuire progetti nel server Integration Services](../../2014/integration-services/deploy-projects-to-integration-services-server.md).  
  
 **Parametro del pacchetto figlio**  
 Immettere o selezionare un nome per il parametro del pacchetto figlio.  
  
 **Parametro o variabile di associazione**  
 Selezionare il parametro o la variabile contenente il valore che si desidera passare al pacchetto figlio.  
  
 **Aggiungi**  
 Fare clic su questa opzione per eseguire il mapping di un parametro o una variabile a un parametro del pacchetto figlio.  
  
 **Rimuovi**  
 Fare clic su questa opzione per rimuovere un mapping tra un parametro o una variabile e un parametro del pacchetto figlio.  
  
  
