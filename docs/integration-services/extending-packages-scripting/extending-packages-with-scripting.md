---
title: Estensione di pacchetti tramite scripting | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- SQL Server Integration Services, scripting
- SSIS, scripting
- scripts [Integration Services], about scripting
ms.assetid: 67fe18ef-f3aa-41d4-9b9d-5defd4618c4b
author: chugugrace
ms.author: chugu
ms.openlocfilehash: e7721e38ca3f9e19ecf3d8d4ee6113f1768427b4
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/22/2020
ms.locfileid: "86915955"
---
# <a name="extending-packages-with-scripting"></a>Estensione di pacchetti tramite scripting

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Se i componenti predefiniti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] non soddisfano i propri requisiti, è possibile estendere le funzionalità di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] utilizzando il codice per definire estensioni personalizzate. Per l'estensione dei pacchetti sono disponibili due opzioni discrete: è possibile scrivere codice all'interno dei potenti wrapper forniti dall'attività Script e dal componente script oppure creare da zero estensioni personalizzate di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] derivando dalla classe di base fornita dal modello a oggetti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 In questa sezione viene esaminata la più semplice delle due opzioni, ovvero l'estensione di pacchetti con lo scripting.  
  
 Con poche righe di codice è possibile estendere il flusso di controllo e il flusso di dati di un pacchetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] utilizzando l'attività Script e il componente di script. Entrambi gli oggetti usano l'ambiente di sviluppo di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA) e il linguaggio di programmazione [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C# e sfruttano tutte le funzionalità della libreria di classi [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] e degli assembly personalizzati. L'attività Script e il componente script consentono allo sviluppatore di creare funzionalità personalizzate senza la necessità di scrivere tutto il codice dell'infrastruttura normalmente richiesto per lo sviluppo di un'attività personalizzata o di un componente del flusso di dati personalizzato.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
 [Confronto tra l'attività Script e il componente script](../../integration-services/extending-packages-scripting/comparing-the-script-task-and-the-script-component.md)  
 Vengono descritte le analogie e le differenze tra l'attività Script e il componente script.  
  
 [Confronto tra soluzioni di scripting e oggetti personalizzati](../../integration-services/extending-packages-scripting/comparing-scripting-solutions-and-custom-objects.md)  
 Vengono descritti i criteri da utilizzare nella scelta tra una soluzione di scripting e lo sviluppo di un oggetto personalizzato.  
  
 [Riferimenti ad altri assembly nelle soluzioni di scripting](../../integration-services/extending-packages-scripting/referencing-other-assemblies-in-scripting-solutions.md)  
 Vengono descritti i passaggi necessari per fare riferimento a e utilizzare assembly e spazi dei nomi esterni in un progetto di scripting.  
  
 [Estensione del pacchetto con l'attività Script](../../integration-services/extending-packages-scripting/task/extending-the-package-with-the-script-task.md)  
 Viene illustrato come creare attività personalizzate tramite l'attività Script. Un'attività viene in genere chiamata una volta per ogni esecuzione del pacchetto oppure una volta per ogni origine dati aperta da un pacchetto.  
  
 [Estensione del flusso di dati con il componente script](../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md)  
 Viene descritto come creare origini, trasformazioni e destinazioni personalizzate del flusso di dati tramite il componente script. Un componente del flusso di dati viene in genere chiamato una volta per ogni riga di dati che viene elaborata.  
  
## <a name="reference"></a>Riferimento  
 [Guida di riferimento ai messaggi e agli errori di Integration Services](../../integration-services/integration-services-error-and-message-reference.md)  
 Vengono elencati i codici di errore predefiniti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] con i relativi nomi simbolici e le descrizioni.  
  
## <a name="related-sections"></a>Sezioni correlate  
 [Estensione di pacchetti tramite oggetti personalizzati](../../integration-services/extending-packages-custom-objects/extending-packages-with-custom-objects.md)  
 Viene descritto come creare e programmare attività personalizzate, componenti del flusso di dati e altri oggetti di pacchetto da utilizzare in più pacchetti.  
  
 [Compilazione di pacchetti a livello di programmazione](../../integration-services/building-packages-programmatically/building-packages-programmatically.md)  
 Viene descritto come creare, configurare, eseguire, caricare, salvare e gestire pacchetti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] a livello di programmazione.  
  
## <a name="see-also"></a>Vedere anche  
 [SQL Server Integration Services](../../integration-services/sql-server-integration-services.md)  
  
  
