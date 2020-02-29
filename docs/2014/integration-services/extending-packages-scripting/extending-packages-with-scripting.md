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
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: bb567bffe0c184907ca61bd583eb5666948a0f03
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/28/2020
ms.locfileid: "78176183"
---
# <a name="extending-packages-with-scripting"></a>Estensione di pacchetti tramite scripting
  Se i componenti predefiniti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] non soddisfano i propri requisiti, è possibile estendere le funzionalità di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] utilizzando il codice per definire estensioni personalizzate. Per l'estensione dei pacchetti sono disponibili due opzioni discrete: è possibile scrivere codice all'interno dei potenti wrapper forniti dall'attività Script e dal componente script oppure creare da zero estensioni personalizzate di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] derivando dalla classe di base fornita dal modello a oggetti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].

 In questa sezione viene esaminata la più semplice delle due opzioni, ovvero l'estensione di pacchetti con lo scripting.

 Con poche righe di codice è possibile estendere il flusso di controllo e il flusso di dati di un pacchetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] utilizzando l'attività Script e il componente di script. Entrambi gli oggetti usano l'ambiente di sviluppo di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA) e il linguaggio di programmazione [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C# e sfruttano tutte le funzionalità della libreria di classi [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] e degli assembly personalizzati. L'attività Script e il componente script consentono allo sviluppatore di creare funzionalità personalizzate senza la necessità di scrivere tutto il codice dell'infrastruttura normalmente richiesto per lo sviluppo di un'attività personalizzata o di un componente del flusso di dati personalizzato.

## <a name="in-this-section"></a>Contenuto della sezione
 [Confronto tra l'attività script e il componente script](../extending-packages-scripting/comparing-the-script-task-and-the-script-component.md) Vengono illustrate le analogie e le differenze tra l'attività script e il componente script.

 [Confronto tra soluzioni di scripting e oggetti personalizzati](comparing-scripting-solutions-and-custom-objects.md) Vengono illustrati i criteri da utilizzare nella scelta tra una soluzione di scripting e lo sviluppo di un oggetto personalizzato.

 [Riferimento ad altri assembly nelle soluzioni di scripting](referencing-other-assemblies-in-scripting-solutions.md) Vengono illustrati i passaggi necessari per fare riferimento e utilizzare gli assembly esterni e gli spazi dei nomi in un progetto di scripting.

 [Estensione del pacchetto con l'attività script](../extending-packages-scripting/task/extending-the-package-with-the-script-task.md) Viene illustrato come creare attività personalizzate tramite l'attività script. Un'attività viene in genere chiamata una volta per ogni esecuzione del pacchetto oppure una volta per ogni origine dati aperta da un pacchetto.

 [Estensione del flusso di dati con il componente script](data-flow-script-component/extending-the-data-flow-with-the-script-component.md) Viene illustrato come creare origini, trasformazioni e destinazioni personalizzate del flusso di dati utilizzando il componente script. Un componente del flusso di dati viene in genere chiamato una volta per ogni riga di dati che viene elaborata.

## <a name="reference"></a>Informazioni di riferimento
 [Integration Services riferimento a errori e messaggi](../integration-services-error-and-message-reference.md) Elenca i codici di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] errore predefiniti con i relativi nomi simbolici e le descrizioni.

## <a name="related-sections"></a>Sezioni correlate
 [Estensione di pacchetti con oggetti personalizzati](../extending-packages-custom-objects/extending-packages-with-custom-objects.md) Viene illustrato come creare attività personalizzate del programma, componenti del flusso di dati e altri oggetti di pacchetto da utilizzare in più pacchetti.

 [Compilazione di pacchetti a livello di programmazione](../building-packages-programmatically/building-packages-programmatically.md) Viene descritto come creare, configurare, eseguire, caricare, salvare e gestire [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] pacchetti a livello di programmazione.

![Integration Services icona (piccola)](../media/dts-16.gif "Icona di Integration Services (piccola)")  **rimane aggiornata con Integration Services**<br /> Per i download, gli articoli, gli esempi e i video [!INCLUDE[msCoName](../../includes/msconame-md.md)] più recenti, oltre alle soluzioni selezionate dalla community, visitare la pagina [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] su MSDN:<br /><br /> [Visita la pagina Integration Services su MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Per ricevere una notifica automatica su questi aggiornamenti, sottoscrivere i feed RSS disponibili nella pagina.

## <a name="see-also"></a>Vedere anche
 [SQL Server Integration Services](../sql-server-integration-services.md)


