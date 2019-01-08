---
title: Estensione di pacchetti tramite scripting | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- SQL Server Integration Services, scripting
- SSIS, scripting
- scripts [Integration Services], about scripting
ms.assetid: 67fe18ef-f3aa-41d4-9b9d-5defd4618c4b
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a8965921b37616e2e317167a41da0867097fc5de
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2018
ms.locfileid: "53363473"
---
# <a name="extending-packages-with-scripting"></a>Estensione di pacchetti tramite scripting
  Se i componenti predefiniti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] non soddisfano i propri requisiti, è possibile estendere le funzionalità di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] utilizzando il codice per definire estensioni personalizzate. Per l'estensione dei pacchetti sono disponibili due opzioni discrete: è possibile scrivere codice all'interno dei potenti wrapper forniti dall'attività Script e dal componente script oppure creare da zero estensioni personalizzate di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] derivando dalla classe di base fornita dal modello a oggetti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 In questa sezione viene esaminata la più semplice delle due opzioni, ovvero l'estensione di pacchetti con lo scripting.  
  
 Con poche righe di codice è possibile estendere il flusso di controllo e il flusso di dati di un pacchetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] utilizzando l'attività Script e il componente di script. Entrambi gli oggetti usano l'ambiente di sviluppo di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA) e il linguaggio di programmazione [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C# e sfruttano tutte le funzionalità della libreria di classi [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] e degli assembly personalizzati. L'attività Script e il componente script consentono allo sviluppatore di creare funzionalità personalizzate senza la necessità di scrivere tutto il codice dell'infrastruttura normalmente richiesto per lo sviluppo di un'attività personalizzata o di un componente del flusso di dati personalizzato.  
  
## <a name="in-this-section"></a>In questa sezione  
 [Confronto tra l'attività Script e il componente script](../extending-packages-scripting/comparing-the-script-task-and-the-script-component.md)  
 Vengono descritte le analogie e le differenze tra l'attività Script e il componente script.  
  
 [Confronto tra soluzioni di scripting e oggetti personalizzati](comparing-scripting-solutions-and-custom-objects.md)  
 Vengono descritti i criteri da utilizzare nella scelta tra una soluzione di scripting e lo sviluppo di un oggetto personalizzato.  
  
 [Riferimenti ad altri assembly nelle soluzioni di scripting](referencing-other-assemblies-in-scripting-solutions.md)  
 Vengono descritti i passaggi necessari per fare riferimento a e utilizzare assembly e spazi dei nomi esterni in un progetto di scripting.  
  
 [Estensione del pacchetto con l'attività Script](../extending-packages-scripting/task/extending-the-package-with-the-script-task.md)  
 Viene illustrato come creare attività personalizzate tramite l'attività Script. Un'attività viene in genere chiamata una volta per ogni esecuzione del pacchetto oppure una volta per ogni origine dati aperta da un pacchetto.  
  
 [Estensione del flusso di dati con il componente script](data-flow-script-component/extending-the-data-flow-with-the-script-component.md)  
 Viene descritto come creare origini, trasformazioni e destinazioni personalizzate del flusso di dati tramite il componente script. Un componente del flusso di dati viene in genere chiamato una volta per ogni riga di dati che viene elaborata.  
  
## <a name="reference"></a>Riferimenti  
 [Guida di riferimento ai messaggi e agli errori di Integration Services](../integration-services-error-and-message-reference.md)  
 Vengono elencati i codici di errore predefiniti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] con i relativi nomi simbolici e le descrizioni.  
  
## <a name="related-sections"></a>Sezioni correlate  
 [Estensione di pacchetti tramite oggetti personalizzati](../extending-packages-custom-objects/extending-packages-with-custom-objects.md)  
 Viene descritto come creare e programmare attività personalizzate, componenti del flusso di dati e altri oggetti di pacchetto da utilizzare in più pacchetti.  
  
 [Compilazione di pacchetti a livello di programmazione](../building-packages-programmatically/building-packages-programmatically.md)  
 Viene descritto come creare, configurare, eseguire, caricare, salvare e gestire pacchetti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] a livello di programmazione.  
  
![Icona di Integration Services (piccola)](../media/dts-16.gif "icona di Integration Services (piccola)")**rimangono fino a Date con Integration Services**<br /> Per i download, gli articoli, gli esempi e i video [!INCLUDE[msCoName](../../includes/msconame-md.md)] più recenti, oltre alle soluzioni selezionate dalla community, visitare la pagina [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] su MSDN:<br /><br /> [Visita la pagina di Integration Services su MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Per ricevere una notifica automatica su questi aggiornamenti, sottoscrivere i feed RSS disponibili nella pagina.  
  
## <a name="see-also"></a>Vedere anche  
 [SQL Server Integration Services](../sql-server-integration-services.md)  
  
  
