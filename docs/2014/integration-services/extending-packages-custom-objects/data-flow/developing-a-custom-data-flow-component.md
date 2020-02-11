---
title: Sviluppo di un componente del flusso di dati personalizzato | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
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
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 6c174fe5cdf1ebe1dbc9b0350a01fb6e8027effa
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62768967"
---
# <a name="developing-a-custom-data-flow-component"></a>Sviluppo di un componente del flusso di dati personalizzato
  L'attività Flusso di dati è costituita da componenti che si connettono a una varietà di origini dati, quindi trasformano e indirizzano i dati ad alta velocità. [!INCLUDE[msCoName](../../../includes/msconame-md.md)]fornisce un modello a oggetti estendibile che consente agli sviluppatori di creare origini, trasformazioni e destinazioni personalizzate che è [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] possibile utilizzare in e nei pacchetti distribuiti. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] In questa sezione sono inclusi argomenti che in cui viene illustrato lo sviluppo di componenti del flusso di dati personalizzati.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
 [Creazione di un componente flusso di dati personalizzato](creating-a-custom-data-flow-component.md)  
 Vengono descritti i passaggi iniziali per la creazione di un componente del flusso di dati personalizzato.  
  
 [Metodi della fase di progettazione di un componente flusso di dati](design-time-methods-of-a-data-flow-component.md)  
 Vengono descritti i metodi della fase di progettazione da implementare in un componente del flusso di dati personalizzato.  
  
 [Metodi di runtime di un componente flusso di dati](run-time-methods-of-a-data-flow-component.md)  
 Vengono descritti i metodi di runtime da implementare in un componente del flusso di dati personalizzato.  
  
 [Piano di esecuzione e allocazione di buffer](execution-plan-and-buffer-allocation.md)  
 Vengono descritti il piano di esecuzione del flusso di dati e l'allocazione di buffer di dati.  
  
 [Utilizzo di tipi di dati nel flusso di dati](working-with-data-types-in-the-data-flow.md)  
 Viene illustrato il mapping del flusso di dati dai tipi di dati di [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] ai tipi di dati gestiti di .NET Framework.  
  
 [Convalida di un componente del flusso di dati](validating-a-data-flow-component.md)  
 Vengono illustrati i metodi utilizzati per convalidare la configurazione del componente e per riconfigurare i metadati del componente.  
  
 [Implementazione di metadati esterni](implementing-external-metadata.md)  
 Viene illustrato l'utilizzo delle colonne di metadati esterni per la convalida dei dati.  
  
 [Generazione e definizione di eventi in un componente del flusso di dati](raising-and-defining-events-in-a-data-flow-component.md)  
 Viene illustrato come generare eventi predefiniti e personalizzati.  
  
 [Registrazione e definizione di voci di log in un componente del flusso di dati](logging-and-defining-log-entries-in-a-data-flow-component.md)  
 Viene illustrato come creare e scrivere in voci di log personalizzate.  
  
 [Utilizzo degli output degli errori in un componente del flusso di dati](using-error-outputs-in-a-data-flow-component.md)  
 Viene illustrato come reindirizzare le righe di errore a un output alternativo.  
  
 [Aggiornamento della versione di un componente del flusso di dati](upgrading-the-version-of-a-data-flow-component.md)  
 Viene illustrato come aggiornare i metadati del componente salvati quando viene utilizzata per la prima volta una nuova versione del componente.  
  
 [Sviluppo di un'interfaccia utente per un componente del flusso di dati](developing-a-user-interface-for-a-data-flow-component.md)  
 Viene illustrato come implementare un editor personalizzato per un componente.  
  
 [Sviluppo di tipi specifici di componenti del flusso di dati](../../extending-packages-custom-objects-data-flow-types/developing-specific-types-of-data-flow-components.md)  
 Contiene informazioni sullo sviluppo dei tre tipi di componenti del flusso di dati: origini, trasformazioni e destinazioni.  
  
## <a name="reference"></a>Riferimento  
 <xref:Microsoft.SqlServer.Dts.Pipeline>  
 Contiene le classi e le interfacce utilizzate per creare componenti del flusso di dati personalizzati.  
  
 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper>  
 Contiene le classi e le interfacce che costituiscono il modello a oggetti dell'attività Flusso di dati, utilizzato per creare componenti del flusso di dati personalizzati o per compilare un'attività Flusso di dati.  
  
 <xref:Microsoft.SqlServer.Dts.Pipeline.Design>  
 Contiene le classi e le interfacce utilizzate per creare l'interfaccia utente per i componenti del flusso di dati.  
  
 [Guida di riferimento ai messaggi e agli errori di Integration Services](../../integration-services-error-and-message-reference.md)  
 Vengono elencati i codici di errore predefiniti di [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] con i relativi nomi simbolici e le descrizioni.  
  
## <a name="related-sections"></a>Sezioni correlate  
  
### <a name="information-common-to-all-custom-objects"></a>Informazioni comuni per tutti gli oggetti personalizzati  
 Per informazioni comuni a tutti i tipi di oggetti personalizzati che è possibile creare in [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)], vedere gli argomenti seguenti:  
  
 [Sviluppo di oggetti personalizzati per Integration Services](../../extending-packages-custom-objects/developing-custom-objects-for-integration-services.md)  
 Vengono descritti i passaggi di base per implementare tutti i tipi di oggetti personalizzati in [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)].  
  
 [Persistenza degli oggetti personalizzati](../../extending-packages-custom-objects/persisting-custom-objects.md)  
 Viene descritta la persistenza personalizzata e vengono illustrati i casi in cui è necessaria.  
  
 [Compilazione, distribuzione e debug di oggetti personalizzati](../../extending-packages-custom-objects/building-deploying-and-debugging-custom-objects.md)  
 Vengono descritte le tecniche per la compilazione, la firma, la distribuzione e il debug di oggetti personalizzati.  
  
### <a name="information-about-other-custom-objects"></a>Informazioni su altri oggetti personalizzati  
 Per informazioni sugli altri tipi di oggetti personalizzati che è possibile creare in [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)], vedere gli argomenti seguenti:  
  
 [Sviluppo di un'attività personalizzata](../../extending-packages-custom-objects/task/developing-a-custom-task.md)  
 Viene descritto come programmare attività personalizzate.  
  
 [Sviluppo di una gestione connessione personalizzata](../../extending-packages-custom-objects/connection-manager/developing-a-custom-connection-manager.md)  
 Viene descritto come programmare gestioni connessioni personalizzate.  
  
 [Sviluppo di un provider di log personalizzato](../../extending-packages-custom-objects/log-provider/developing-a-custom-log-provider.md)  
 Viene descritto come programmare provider di log personalizzati.  
  
 [Sviluppo di un enumeratore Foreach personalizzato](../../extending-packages-custom-objects/foreach-enumerator/developing-a-custom-foreach-enumerator.md)  
 Viene descritto come programmare enumeratori personalizzati.  
  
![Integration Services icona (piccola)](../../media/dts-16.gif "Icona di Integration Services (piccola)")  **rimane aggiornata con Integration Services**<br /> Per i download, gli articoli, gli esempi e i video Microsoft più recenti, oltre alle soluzioni selezionate dalla community, visitare la pagina [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] sul sito MSDN:<br /><br /> [Visita la pagina Integration Services su MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Per ricevere una notifica automatica su questi aggiornamenti, sottoscrivere i feed RSS disponibili nella pagina.  
  
## <a name="see-also"></a>Vedere anche  
 [Estensione del flusso di dati con il componente script] (.. /.. /extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md   
 [Confronto tra soluzioni di scripting e oggetti personalizzati](../../extending-packages-scripting/comparing-scripting-solutions-and-custom-objects.md)  
  
  
