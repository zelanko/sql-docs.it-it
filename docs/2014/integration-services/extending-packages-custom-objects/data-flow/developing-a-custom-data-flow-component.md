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
author: chugugrace
ms.author: chugu
ms.openlocfilehash: ee2b30cf0796953d12f976745fb195169de86c68
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/26/2020
ms.locfileid: "85437078"
---
# <a name="developing-a-custom-data-flow-component"></a>Sviluppo di un componente del flusso di dati personalizzato
  L'attività Flusso di dati è costituita da componenti che si connettono a una varietà di origini dati, quindi trasformano e indirizzano i dati ad alta velocità. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] offre un modello a oggetti estendibile che consente agli sviluppatori di creare origini, trasformazioni e destinazioni personalizzate da usare in [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] e nei pacchetti distribuiti. In questa sezione sono inclusi argomenti che in cui viene illustrato lo sviluppo di componenti del flusso di dati personalizzati.

## <a name="in-this-section"></a>Contenuto della sezione
 [Creazione di un componente flusso di dati personalizzato](creating-a-custom-data-flow-component.md) Vengono descritti i passaggi iniziali della creazione di un componente del flusso di dati personalizzato.

 [Metodi della fase di progettazione di un componente flusso di dati](design-time-methods-of-a-data-flow-component.md) Vengono descritti i metodi della fase di progettazione da implementare in un componente del flusso di dati personalizzato.

 [Metodi di runtime di un componente flusso di dati](run-time-methods-of-a-data-flow-component.md) Vengono descritti i metodi di runtime da implementare in un componente del flusso di dati personalizzato.

 [Piano di esecuzione e allocazione di buffer](execution-plan-and-buffer-allocation.md) Descrive il piano di esecuzione del flusso di dati e l'allocazione dei buffer di dati.

 [Utilizzo di tipi di dati nel flusso di dati](working-with-data-types-in-the-data-flow.md) Viene illustrato come il flusso di dati esegue il mapping dei [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] tipi di dati a .NET Framework tipi di dati gestiti.

 [Convalida di un componente flusso di dati](validating-a-data-flow-component.md) Vengono illustrati i metodi utilizzati per convalidare la configurazione del componente e per riconfigurare i metadati del componente.

 [Implementazione di metadati esterni](implementing-external-metadata.md) Viene illustrato come utilizzare le colonne di metadati esterne per la convalida dei dati.

 [Generazione e definizione di eventi in un componente flusso di dati](raising-and-defining-events-in-a-data-flow-component.md) Viene illustrato come generare eventi predefiniti e personalizzati.

 [Registrazione e definizione di voci di log in un componente flusso di dati](logging-and-defining-log-entries-in-a-data-flow-component.md) Viene illustrato come creare e scrivere in voci di log personalizzate.

 [Uso degli output degli errori in un componente flusso di dati](using-error-outputs-in-a-data-flow-component.md) Viene illustrato come reindirizzare le righe di errore a un output alternativo.

 [Aggiornamento della versione di un componente flusso di dati](upgrading-the-version-of-a-data-flow-component.md) Viene illustrato come aggiornare i metadati del componente salvati quando viene usata per la prima volta una nuova versione del componente.

 [Sviluppo di un'interfaccia utente per un componente flusso di dati](developing-a-user-interface-for-a-data-flow-component.md) Viene illustrato come implementare un editor personalizzato per un componente.

 [Sviluppo di tipi specifici di componenti del flusso di dati](../../extending-packages-custom-objects-data-flow-types/developing-specific-types-of-data-flow-components.md) Sono incluse informazioni sullo sviluppo dei tre tipi di componenti del flusso di dati, ovvero origini, trasformazioni e destinazioni.

## <a name="reference"></a>Informazioni di riferimento
 <xref:Microsoft.SqlServer.Dts.Pipeline>Contiene le classi e le interfacce utilizzate per creare componenti del flusso di dati personalizzati.

 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper>Contiene le classi e le interfacce che costituiscono il modello a oggetti dell'attività flusso di dati e viene utilizzato per creare componenti flusso di dati personalizzati o per compilare un'attività flusso di dati.

 <xref:Microsoft.SqlServer.Dts.Pipeline.Design>Contiene le classi e le interfacce utilizzate per creare l'interfaccia utente per i componenti del flusso di dati.

 [Integration Services riferimento a errori e messaggi](../../integration-services-error-and-message-reference.md) Elenca i [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] codici di errore predefiniti con i relativi nomi simbolici e le descrizioni.

## <a name="related-sections"></a>Sezioni correlate

### <a name="information-common-to-all-custom-objects"></a>Informazioni comuni per tutti gli oggetti personalizzati
 Per informazioni comuni a tutti i tipi di oggetti personalizzati che è possibile creare in [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)], vedere gli argomenti seguenti:

 [Sviluppo di oggetti personalizzati per Integration Services](../../extending-packages-custom-objects/developing-custom-objects-for-integration-services.md) Vengono descritti i passaggi di base per l'implementazione di tutti i tipi di oggetti personalizzati per [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] .

 [Salvataggio permanente di oggetti personalizzati](../../extending-packages-custom-objects/persisting-custom-objects.md) Viene descritta la persistenza personalizzata e viene spiegato quando è necessario.

 [Compilazione, distribuzione e debug di oggetti personalizzati](../../extending-packages-custom-objects/building-deploying-and-debugging-custom-objects.md) Vengono descritte le tecniche per la compilazione, la firma, la distribuzione e il debug di oggetti personalizzati.

### <a name="information-about-other-custom-objects"></a>Informazioni su altri oggetti personalizzati
 Per informazioni sugli altri tipi di oggetti personalizzati che è possibile creare in [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)], vedere gli argomenti seguenti:

 [Sviluppo di un'attività personalizzata](../../extending-packages-custom-objects/task/developing-a-custom-task.md) Viene illustrato come programmare attività personalizzate.

 [Sviluppo di una gestione connessione personalizzata](../../extending-packages-custom-objects/connection-manager/developing-a-custom-connection-manager.md) Viene illustrato come programmare gestioni connessioni personalizzate.

 [Sviluppo di un provider di log personalizzato](../../extending-packages-custom-objects/log-provider/developing-a-custom-log-provider.md) Viene illustrato come programmare i provider di log personalizzati.

 [Sviluppo di un enumeratore Foreach personalizzato](../../extending-packages-custom-objects/foreach-enumerator/developing-a-custom-foreach-enumerator.md) Viene illustrato come programmare gli enumeratori personalizzati.

![Integration Services icona (piccola)](../../media/dts-16.gif "Icona di Integration Services (piccola)")  **rimane aggiornata con Integration Services**<br /> Per i download, gli articoli, gli esempi e i video Microsoft più recenti, oltre alle soluzioni selezionate dalla community, visitare la pagina [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] sul sito MSDN:<br /><br /> [Visitare la pagina relativa a Integration Services su MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Per ricevere una notifica automatica su questi aggiornamenti, sottoscrivere i feed RSS disponibili nella pagina.

## <a name="see-also"></a>Vedere anche
 [Estensione del flusso di dati con il componente script] (.. /.. /Extending-Packages-scripting/Data-Flow-Script-Component/Extending-the-data-flow-with-the-script-component.MD [confronto tra soluzioni di scripting e oggetti personalizzati](../../extending-packages-scripting/comparing-scripting-solutions-and-custom-objects.md)


