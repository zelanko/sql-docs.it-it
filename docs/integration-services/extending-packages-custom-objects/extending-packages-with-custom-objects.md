---
description: Estensione di pacchetti tramite oggetti personalizzati
title: Estensione di pacchetti tramite oggetti personalizzati | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
ms.assetid: 26616eb8-9e80-434d-b22a-ece1b00f449d
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 3837f3fe73a3ee9d099199e959d65afd1df4e95b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88430573"
---
# <a name="extending-packages-with-custom-objects"></a>Estensione di pacchetti tramite oggetti personalizzati

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Se i componenti forniti in [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] non soddisfano i requisiti, è possibile estendere le funzionalità di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] utilizzando il codice per definire estensioni personalizzate. Per l'estensione dei pacchetti sono disponibili due opzioni discrete: è possibile scrivere codice all'interno dei potenti wrapper forniti dall'attività Script e dal componente script oppure creare da zero estensioni personalizzate di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] derivando dalla classe di base fornita dal modello a oggetti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 In questa sezione viene esaminata la più avanzata delle due opzioni, ovvero l'estensione di pacchetti tramite oggetti personalizzati.  
  
 Quando una soluzione [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] personalizzata richiede una maggiore flessibilità di quanto non forniscano l'attività Script e il componente script oppure quando è necessario un componente riutilizzabile in più pacchetti, il modello a oggetti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] consente di compilare completamente da zero attività personalizzate, componenti flusso di dati e altri oggetti del pacchetto in codice gestito.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
 [Sviluppo di oggetti personalizzati per Integration Services](../../integration-services/extending-packages-custom-objects/developing-custom-objects-for-integration-services.md)  
 Vengono descritti gli oggetti personalizzati che è possibile creare per [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], con un riepilogo dei passaggi e delle impostazioni essenziali.  
  
 [Persistenza degli oggetti personalizzati](../../integration-services/extending-packages-custom-objects/persisting-custom-objects.md)  
 Viene descritta la persistenza predefinita degli oggetti personalizzati e viene illustrato il relativo processo di implementazione.  
  
 [Compilazione, distribuzione e debug di oggetti personalizzati](../../integration-services/extending-packages-custom-objects/building-deploying-and-debugging-custom-objects.md)  
 Vengono descritti gli approcci comuni per la compilazione, la distribuzione e il test di vari tipi di oggetti personalizzati.  
  
 [Sviluppo di un'attività personalizzata](../../integration-services/extending-packages-custom-objects/task/developing-a-custom-task.md)  
 Viene descritto il processo di scrittura del codice di un'attività personalizzata.  
  
 [Sviluppo di una gestione connessione personalizzata](../../integration-services/extending-packages-custom-objects/connection-manager/developing-a-custom-connection-manager.md)  
 Viene descritto il processo di scrittura del codice di una gestione connessione personalizzata.  
  
 [Sviluppo di un provider di log personalizzato](../../integration-services/extending-packages-custom-objects/log-provider/developing-a-custom-log-provider.md)  
 Viene descritto il processo di scrittura del codice di un provider di log personalizzato.  
  
 [Sviluppo di un enumeratore Foreach personalizzato](../../integration-services/extending-packages-custom-objects/foreach-enumerator/developing-a-custom-foreach-enumerator.md)  
 Viene descritto il processo di scrittura del codice di un enumeratore personalizzato.  
  
 [Sviluppo di un componente flusso di dati personalizzato](../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md)  
 Viene descritto come programmare origini, trasformazioni e destinazioni personalizzate del flusso di dati.  
  
## <a name="reference"></a>Informazioni di riferimento  
 [Guida di riferimento ai messaggi e agli errori di Integration Services](../../integration-services/integration-services-error-and-message-reference.md)  
 Vengono elencati i codici di errore predefiniti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] con i relativi nomi simbolici e le descrizioni.  
  
## <a name="related-sections"></a>Sezioni correlate  
 [Estensione di pacchetti tramite scripting](../../integration-services/extending-packages-scripting/extending-packages-with-scripting.md)  
 Viene descritto come estendere il flusso di controllo utilizzando l'attività Script o il flusso di dati utilizzando il componente script.  
  
 [Compilazione di pacchetti a livello di programmazione](../../integration-services/building-packages-programmatically/building-packages-programmatically.md)  
 Viene descritto come creare, configurare, eseguire, caricare, salvare e gestire pacchetti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] a livello di programmazione.  
  
## <a name="see-also"></a>Vedere anche  
 [Confronto tra soluzioni di scripting e oggetti personalizzati](../../integration-services/extending-packages-scripting/comparing-scripting-solutions-and-custom-objects.md)   
 [SQL Server Integration Services](../../integration-services/sql-server-integration-services.md)  
  
  
