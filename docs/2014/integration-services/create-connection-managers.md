---
title: Creazione di gestioni connessioni | Microsoft Docs
ms.custom: ''
ms.date: 08/22/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.connectionmanager.f1
helpviewer_keywords:
- Integration Services packages, connections
- SSIS packages, connections
- packages [Integration Services], connections
- connection managers [Integration Services], creating
- SQL Server Integration Services packages, connections
ms.assetid: 6ca317b8-0061-4d9d-b830-ee8c21268345
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: a82ef5c249dd1bc15bc91e9ccc502ebffe3f1728
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66060116"
---
# <a name="create-connection-managers"></a>Creazione di gestioni connessioni
  In [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] è disponibile un'ampia gamma di gestioni connessioni che consentono di soddisfare le esigenze di attività che si connettono a diversi tipi di server e origini dati. Le gestioni connessioni vengono utilizzate dai componenti del flusso di dati che estraggono e caricano dati in diversi tipi di archivi dati e dai provider di log che scrivono log in un server, in una tabella di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] o in un file. Un pacchetto che include un'attività Invia messaggi, ad esempio, utilizza un tipo di gestione connessione SMTP (Simple Mail Transfer Protocol) per connettersi a un server SMTP. Un pacchetto che include un'attività Esegui SQL può usare una gestione connessione OLE DB per connettersi a un database di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Per altre informazioni, vedere [Connessioni in Integration Services &#40;SSIS&#41;](connection-manager/integration-services-ssis-connections.md).  
  
 Per creare e configurare automaticamente gestioni connessioni durante la creazione di un nuovo pacchetto, è possibile usare Importazione/Esportazione guidata [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. La procedura guidata consente anche di creare e configurare le origini e le destinazioni che usano le gestioni connessioni. Per altre informazioni, vedere [Creare pacchetti in SQL Server Data Tools](create-packages-in-sql-server-data-tools.md).  
  
 Per creare manualmente una nuova gestione connessione e aggiungerla a un pacchetto esistente, è possibile usare l'area **Gestioni connessioni** disponibile nelle schede **Flusso di controllo**, **Flusso di dati** e **Gestori eventi** di Progettazione [!INCLUDE[ssIS](../includes/ssis-md.md)]. Dall'area **Gestione connessione** è possibile scegliere il tipo di gestione connessione da creare e quindi impostare le proprietà della gestione connessione utilizzando la finestra di dialogo disponibile in Progettazione [!INCLUDE[ssIS](../includes/ssis-md.md)]. Per ulteriori informazioni, vedere la sezione "Utilizzo dell'area Gestioni connessioni" più avanti in questo argomento.  
  
 Dopo avere aggiunto la gestione connessione a un pacchetto è possibile utilizzarla in attività, contenitori Ciclo Foreach, origini, trasformazioni e destinazioni. Per altre informazioni, vedere [Attività di Integration Services](control-flow/integration-services-tasks.md), [Contenitore Ciclo Foreach](control-flow/foreach-loop-container.md) e [Flusso di dati](data-flow/data-flow.md).  
  
## <a name="using-the-connection-managers-area"></a>Utilizzo dell'area Gestioni connessioni  
 È possibile creare gestioni connessioni quando è attiva la scheda **Flusso di controllo**, **Flusso di dati** o **Gestori eventi** di Progettazione [!INCLUDE[ssIS](../includes/ssis-md.md)].  
  
 Nella figura seguente viene illustrata l'area **Gestioni connessioni** della scheda **Flusso di controllo** di Progettazione [!INCLUDE[ssIS](../includes/ssis-md.md)].  
  
 ![Schermata della finestra di progettazione del flusso di controllo con pacchetto](media/samplecontrolflow.gif "Schermata della finestra di progettazione del flusso di controllo con pacchetto")  
  
#### <a name="to-add-configure-or-delete-a-connection-manager-in-ssis-designer"></a>Per aggiungere, configurare o eliminare una gestione connessione in Progettazione SSIS  
  
-   [Aggiunta, eliminazione o condivisione di una gestione connessione in un pacchetto](../../2014/integration-services/add-delete-or-share-a-connection-manager-in-a-package.md)  
  
-   [Impostazione delle proprietà di una gestione connessione](../../2014/integration-services/set-the-properties-of-a-connection-manager.md)  
  
## <a name="32-bit-and-64-bit-providers-for-connection-managers"></a>Provider a 32 e 64 bit per le gestioni connessioni  
 Molti dei provider utilizzati dalle gestioni connessioni sono disponibili sia in versione a 32 bit che in versione a 64 bit. Poiché l'ambiente di progettazione [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] è a 32 bit, durante la progettazione dei pacchetti in tale ambiente sono disponibili solo provider a 32 bit. Pertanto è possibile solo configurare una gestione connessione in modo da utilizzare uno specifico provider a 64 bit, se nel computer è installata anche la versione a 32 bit dello stesso provider.  
  
 In fase di esecuzione viene utilizzata la versione corretta, anche se in fase di progettazione era stata specificata la versione a 32 bit del provider. È possibile eseguire la versione a 64 bit del provider anche se il pacchetto viene eseguito in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
 Entrambe le versioni del provider hanno lo stesso ID. Per specificare se il runtime [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] deve usare la versione a 64 bit del provider, è necessario impostare la proprietà Run64BitRuntime del progetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]. Se la proprietà Run64BitRuntime è impostata su `true`, il runtime trova e utilizza il provider a 64 bit; Se Run64BitRuntime è `false`, il runtime trova e utilizza il provider a 32 bit. Per altre informazioni sulle proprietà che è possibile impostare per i progetti di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)], vedere [Integration Services &#40;SSIS&#41; e ambienti Studio](integration-services-ssis-development-and-management-tools.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Flusso di controllo](control-flow/control-flow.md)   
 [Flusso di dati](data-flow/data-flow.md)   
 [Gestori eventi di Integration Services &#40;SSIS&#41;](integration-services-ssis-event-handlers.md)  
  
  
