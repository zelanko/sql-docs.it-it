---
title: Estensione di pacchetti tramite oggetti personalizzati | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
ms.assetid: 26616eb8-9e80-434d-b22a-ece1b00f449d
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 57735e21847fdd28376ceaeb13faf3b47e2d10ec
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/26/2020
ms.locfileid: "85427538"
---
# <a name="extending-packages-with-custom-objects"></a>Estensione di pacchetti tramite oggetti personalizzati
  Se i componenti forniti in [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] non soddisfano i requisiti, è possibile estendere le funzionalità di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] utilizzando il codice per definire estensioni personalizzate. Per l'estensione dei pacchetti sono disponibili due opzioni discrete: è possibile scrivere codice all'interno dei potenti wrapper forniti dall'attività Script e dal componente script oppure creare da zero estensioni personalizzate di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] derivando dalla classe di base fornita dal modello a oggetti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 In questa sezione viene esaminata la più avanzata delle due opzioni, ovvero l'estensione di pacchetti tramite oggetti personalizzati.  
  
 Quando una soluzione [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] personalizzata richiede una maggiore flessibilità di quanto non forniscano l'attività Script e il componente script oppure quando è necessario un componente riutilizzabile in più pacchetti, il modello a oggetti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] consente di compilare completamente da zero attività personalizzate, componenti flusso di dati e altri oggetti del pacchetto in codice gestito.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
 [Sviluppo di oggetti personalizzati per Integration Services](developing-custom-objects-for-integration-services.md)  
 Vengono descritti gli oggetti personalizzati che è possibile creare per [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], con un riepilogo dei passaggi e delle impostazioni essenziali.  
  
 [Persistenza degli oggetti personalizzati](persisting-custom-objects.md)  
 Viene descritta la persistenza predefinita degli oggetti personalizzati e viene illustrato il relativo processo di implementazione.  
  
 [Compilazione, distribuzione e debug di oggetti personalizzati](building-deploying-and-debugging-custom-objects.md)  
 Vengono descritti gli approcci comuni per la compilazione, la distribuzione e il test di vari tipi di oggetti personalizzati.  
  
 [Sviluppo di un'attività personalizzata](task/developing-a-custom-task.md)  
 Viene descritto il processo di scrittura del codice di un'attività personalizzata.  
  
 [Sviluppo di una gestione connessione personalizzata](connection-manager/developing-a-custom-connection-manager.md)  
 Viene descritto il processo di scrittura del codice di una gestione connessione personalizzata.  
  
 [Sviluppo di un provider di log personalizzato](log-provider/developing-a-custom-log-provider.md)  
 Viene descritto il processo di scrittura del codice di un provider di log personalizzato.  
  
 [Sviluppo di un enumeratore Foreach personalizzato](foreach-enumerator/developing-a-custom-foreach-enumerator.md)  
 Viene descritto il processo di scrittura del codice di un enumeratore personalizzato.  
  
 [Sviluppo di un componente flusso di dati personalizzato](data-flow/developing-a-custom-data-flow-component.md)  
 Viene descritto come programmare origini, trasformazioni e destinazioni personalizzate del flusso di dati.  
  
## <a name="reference"></a>Riferimento  
 [Guida di riferimento ai messaggi e agli errori di Integration Services](../integration-services-error-and-message-reference.md)  
 Vengono elencati i codici di errore predefiniti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] con i relativi nomi simbolici e le descrizioni.  
  
## <a name="related-sections"></a>Sezioni correlate  
 [Estensione di pacchetti tramite scripting](../extending-packages-scripting/extending-packages-with-scripting.md)  
 Viene descritto come estendere il flusso di controllo utilizzando l'attività Script o il flusso di dati utilizzando il componente script.  
  
 [Compilazione di pacchetti a livello di programmazione](../building-packages-programmatically/building-packages-programmatically.md)  
 Viene descritto come creare, configurare, eseguire, caricare, salvare e gestire pacchetti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] a livello di programmazione.  
  
![Integration Services icona (piccola)](../media/dts-16.gif "Icona di Integration Services (piccola)")  **rimane aggiornata con Integration Services**<br /> Per i download, gli articoli, gli esempi e i video Microsoft più recenti, oltre alle soluzioni selezionate dalla community, visitare la pagina [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] sul sito MSDN:<br /><br /> [Visitare la pagina relativa a Integration Services su MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Per ricevere una notifica automatica su questi aggiornamenti, sottoscrivere i feed RSS disponibili nella pagina.  
  
## <a name="see-also"></a>Vedere anche  
 [Confronto tra soluzioni di scripting e oggetti personalizzati](../extending-packages-scripting/comparing-scripting-solutions-and-custom-objects.md)   
 [SQL Server Integration Services](../sql-server-integration-services.md)  
  
  
