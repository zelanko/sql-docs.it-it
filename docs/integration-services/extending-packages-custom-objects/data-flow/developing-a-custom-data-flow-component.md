---
title: Sviluppo di un componente del flusso di dati personalizzato | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data flow task [Integration Services], extending
- data flow [Integration Services], extending
- extending data flow task [Integration Services]
- components [Integration Services], data flow
ms.assetid: be126913-2a9a-41c9-9bf5-a7b0a0aea2f8
author: chugugrace
ms.author: chugu
ms.openlocfilehash: cd3ef168c8d3c58fb387787e8635ef94c512a475
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "71297242"
---
# <a name="developing-a-custom-data-flow-component"></a>Sviluppo di un componente del flusso di dati personalizzato

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  L'attività Flusso di dati è costituita da componenti che si connettono a una varietà di origini dati, quindi trasformano e indirizzano i dati ad alta velocità. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] offre un modello a oggetti estendibile che consente agli sviluppatori di creare origini, trasformazioni e destinazioni personalizzate da usare in [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] e nei pacchetti distribuiti. In questa sezione sono inclusi argomenti che in cui viene illustrato lo sviluppo di componenti del flusso di dati personalizzati.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
 [Creazione di un componente flusso di dati personalizzato](../../../integration-services/extending-packages-custom-objects/data-flow/creating-a-custom-data-flow-component.md)  
 Vengono descritti i passaggi iniziali per la creazione di un componente del flusso di dati personalizzato.  
  
 [Metodi della fase di progettazione di un componente flusso di dati](../../../integration-services/extending-packages-custom-objects/data-flow/design-time-methods-of-a-data-flow-component.md)  
 Vengono descritti i metodi della fase di progettazione da implementare in un componente del flusso di dati personalizzato.  
  
 [Metodi di runtime di un componente flusso di dati](../../../integration-services/extending-packages-custom-objects/data-flow/run-time-methods-of-a-data-flow-component.md)  
 Vengono descritti i metodi di runtime da implementare in un componente del flusso di dati personalizzato.  
  
 [Piano di esecuzione e allocazione di buffer](../../../integration-services/extending-packages-custom-objects/data-flow/execution-plan-and-buffer-allocation.md)  
 Vengono descritti il piano di esecuzione del flusso di dati e l'allocazione di buffer di dati.  
  
 [Utilizzo di tipi di dati nel flusso di dati](../../../integration-services/extending-packages-custom-objects/data-flow/working-with-data-types-in-the-data-flow.md)  
 Viene illustrato il mapping del flusso di dati dai tipi di dati di [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] ai tipi di dati gestiti di .NET Framework.  
  
 [Convalida di un componente flusso di dati](../../../integration-services/extending-packages-custom-objects/data-flow/validating-a-data-flow-component.md)  
 Vengono illustrati i metodi utilizzati per convalidare la configurazione del componente e per riconfigurare i metadati del componente.  
  
 [Implementazione di metadati esterni](../../../integration-services/extending-packages-custom-objects/data-flow/implementing-external-metadata.md)  
 Viene illustrato l'utilizzo delle colonne di metadati esterni per la convalida dei dati.  
  
 [Generazione e definizione di eventi in un componente flusso di dati](../../../integration-services/extending-packages-custom-objects/data-flow/raising-and-defining-events-in-a-data-flow-component.md)  
 Viene illustrato come generare eventi predefiniti e personalizzati.  
  
 [Registrazione e definizione di voci di log in un componente flusso di dati](../../../integration-services/extending-packages-custom-objects/data-flow/logging-and-defining-log-entries-in-a-data-flow-component.md)  
 Viene illustrato come creare e scrivere in voci di log personalizzate.  
  
 [Uso degli output degli errori in un componente flusso di dati](../../../integration-services/extending-packages-custom-objects/data-flow/using-error-outputs-in-a-data-flow-component.md)  
 Viene illustrato come reindirizzare le righe di errore a un output alternativo.  
  
 [Aggiornamento della versione di un componente flusso di dati](../../../integration-services/extending-packages-custom-objects/data-flow/upgrading-the-version-of-a-data-flow-component.md)  
 Viene illustrato come aggiornare i metadati del componente salvati quando viene utilizzata per la prima volta una nuova versione del componente.  
  
 [Sviluppo di un'interfaccia utente per un componente flusso di dati](../../../integration-services/extending-packages-custom-objects/data-flow/developing-a-user-interface-for-a-data-flow-component.md)  
 Viene illustrato come implementare un editor personalizzato per un componente.  
  
 [Sviluppo di tipi specifici di componenti del flusso di dati](../../../integration-services/extending-packages-custom-objects-data-flow-types/developing-specific-types-of-data-flow-components.md)  
 Contiene informazioni sullo sviluppo dei tre tipi di componenti del flusso di dati: origini, trasformazioni e destinazioni.  
  
## <a name="reference"></a>Informazioni di riferimento  
 <xref:Microsoft.SqlServer.Dts.Pipeline>  
 Contiene le classi e le interfacce utilizzate per creare componenti del flusso di dati personalizzati.  
  
 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper>  
 Contiene le classi e le interfacce che costituiscono il modello a oggetti dell'attività Flusso di dati, utilizzato per creare componenti del flusso di dati personalizzati o per compilare un'attività Flusso di dati.  
  
 <xref:Microsoft.SqlServer.Dts.Pipeline.Design>  
 Contiene le classi e le interfacce utilizzate per creare l'interfaccia utente per i componenti del flusso di dati.  
  
 [Guida di riferimento ai messaggi e agli errori di Integration Services](../../../integration-services/integration-services-error-and-message-reference.md)  
 Vengono elencati i codici di errore predefiniti di [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] con i relativi nomi simbolici e le descrizioni.  
  
## <a name="related-sections"></a>Sezioni correlate  
  
### <a name="information-common-to-all-custom-objects"></a>Informazioni comuni per tutti gli oggetti personalizzati  
 Per informazioni comuni a tutti i tipi di oggetti personalizzati che è possibile creare in [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)], vedere gli argomenti seguenti:  
  
 [Sviluppo di oggetti personalizzati per Integration Services](../../../integration-services/extending-packages-custom-objects/developing-custom-objects-for-integration-services.md)  
 Vengono descritti i passaggi di base per implementare tutti i tipi di oggetti personalizzati in [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)].  
  
 [Persistenza degli oggetti personalizzati](../../../integration-services/extending-packages-custom-objects/persisting-custom-objects.md)  
 Viene descritta la persistenza personalizzata e vengono illustrati i casi in cui è necessaria.  
  
 [Compilazione, distribuzione e debug di oggetti personalizzati](../../../integration-services/extending-packages-custom-objects/building-deploying-and-debugging-custom-objects.md)  
 Vengono descritte le tecniche per la compilazione, la firma, la distribuzione e il debug di oggetti personalizzati.  
  
### <a name="information-about-other-custom-objects"></a>Informazioni su altri oggetti personalizzati  
 Per informazioni sugli altri tipi di oggetti personalizzati che è possibile creare in [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)], vedere gli argomenti seguenti:  
  
 [Sviluppo di un'attività personalizzata](../../../integration-services/extending-packages-custom-objects/task/developing-a-custom-task.md)  
 Viene descritto come programmare attività personalizzate.  
  
 [Sviluppo di una gestione connessione personalizzata](../../../integration-services/extending-packages-custom-objects/connection-manager/developing-a-custom-connection-manager.md)  
 Viene descritto come programmare gestioni connessioni personalizzate.  
  
 [Sviluppo di un provider di log personalizzato](../../../integration-services/extending-packages-custom-objects/log-provider/developing-a-custom-log-provider.md)  
 Viene descritto come programmare provider di log personalizzati.  
  
 [Sviluppo di un enumeratore Foreach personalizzato](../../../integration-services/extending-packages-custom-objects/foreach-enumerator/developing-a-custom-foreach-enumerator.md)  
 Viene descritto come programmare enumeratori personalizzati.  
  
## <a name="see-also"></a>Vedere anche  
 [Estensione del flusso di dati con il componente script](../../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md)   
 [Confronto tra soluzioni di scripting e oggetti personalizzati](../../../integration-services/extending-packages-scripting/comparing-scripting-solutions-and-custom-objects.md)  
  
  
