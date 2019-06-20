---
title: Per gli sviluppatori&#39;Guida (Integration Services) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Integration Services, programming
- SSIS, programming
- SQL Server Integration Services, programming
- packages [Integration Services], programming
ms.assetid: 60fe148b-a7c4-4289-ae3e-2e949fc1886c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 3fc7c93f8e499fb063e0d01c9132606f3ddfa3f7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62892413"
---
# <a name="developer39s-guide-integration-services"></a>Per gli sviluppatori&#39;Guida (Integration Services)
  In [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] è disponibile un modello a oggetti completamente riscritto, potenziato con diverse funzionalità grazie alle quali l'estensione e la programmazione di pacchetti diventano operazioni più semplici, flessibili ed efficaci. Gli sviluppatori possono estendere e programmare quasi ogni aspetto dei pacchetti di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].  
  
 Gli sviluppatori di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] possono adottare due approcci fondamentali per la programmazione di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]:  
  
-   È possibile estendere i pacchetti scrivendo componenti che diventano disponibili in Progettazione [!INCLUDE[ssIS](../includes/ssis-md.md)] per fornire funzionalità personalizzate.  
  
-   È possibile creare, configurare ed eseguire i pacchetti a livello di programmazione dalle applicazioni.  
  
 Se i componenti predefiniti di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] non soddisfano i propri requisiti, è possibile estendere le funzionalità di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] utilizzando il codice per definire estensioni personalizzate. Questo approccio rende disponibili due opzioni discrete:  
  
-   Per l'utilizzo ad hoc in un singolo pacchetto, è possibile creare un'attività personalizzata scrivendo codice nell'attività Script o un componente del flusso di dati personalizzato scrivendo codice nel componente script, che può essere configurato come origine, trasformazione o destinazione. Questi potenti wrapper scrivono il codice dell'infrastruttura e consentono agli sviluppatori di concentrarsi esclusivamente sullo sviluppo di funzionalità personalizzate. Tuttavia, non sono facilmente riutilizzabili altrove.  
  
-   Per l'utilizzo in più pacchetti, è possibile creare estensioni di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] personalizzate, ad esempio gestioni connessioni, attività, enumeratori, provider di log e componenti del flusso di dati. Il modello a oggetti gestiti di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] contiene classi di base che forniscono un punto iniziale e semplificano lo sviluppo di estensioni personalizzate.  
  
 Se si desidera creare pacchetti in modo dinamico oppure gestire ed eseguire pacchetti di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] all'esterno dell'ambiente di sviluppo, è possibile modificare i pacchetti a livello di programmazione. È possibile caricare, modificare ed eseguire pacchetti esistenti oppure creare ed eseguire pacchetti interamente nuovi a livello di programmazione. Questo approccio rende disponibili diverse opzioni:  
  
-   Caricare ed eseguire un pacchetto esistente senza modifiche.  
  
-   Caricare un pacchetto esistente, riconfigurarlo (ad esempio specificando un'origine dati diversa) ed eseguirlo.  
  
-   Creare un nuovo pacchetto, aggiungere e configurare i componenti, apportare modifiche oggetto per oggetto e proprietà per proprietà, salvarlo ed eseguirlo.  
  
 Questi approcci alla programmazione di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] vengono descritti e illustrati con esempi in questa sezione.  
  
## <a name="in-this-section"></a>In questa sezione  
 [Panoramica della programmazione di Integration Services](integration-services-programming-overview.md)  
 Vengono descritti i ruoli del flusso di controllo e del flusso di dati nello sviluppo di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].  
  
 [Informazioni sulle trasformazioni sincrone e asincrone](understanding-synchronous-and-asynchronous-transformations.md)  
 Vengono descritte le importanti differenze tra output sincroni e asincroni e vengono illustrati i componenti che li utilizzano nel flusso di dati.  
  
 [Utilizzo di gestioni connessioni a livello di programmazione](working-with-connection-managers-programmatically.md)  
 Sono elencate le gestioni connessioni che è possibile utilizzare dal codice gestito e i valori restituiti quando viene chiamato il metodo `AcquireConnection`.  
  
 [Estensione di pacchetti tramite scripting](extending-packages-scripting/extending-packages-with-scripting.md)  
 Viene descritto come estendere il flusso di controllo utilizzando l'attività Script o il flusso di dati utilizzando il componente script.  
  
 [Estensione di pacchetti tramite oggetti personalizzati](extending-packages-custom-objects/extending-packages-with-custom-objects.md)  
 Viene descritto come creare e programmare attività personalizzate, componenti del flusso di dati e altri oggetti di pacchetto da utilizzare in più pacchetti.  
  
 [Compilazione di pacchetti a livello di programmazione](building-packages-programmatically/building-packages-programmatically.md)  
 Viene descritto come creare, configurare e salvare pacchetti di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] a livello di programmazione.  
  
 [Esecuzione e gestione dei pacchetti a livello di programmazione](run-manage-packages-programmatically/running-and-managing-packages-programmatically.md)  
 Viene descritto come enumerare, eseguire e gestire i pacchetti di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] a livello di programmazione.  
  
## <a name="reference"></a>Riferimenti  
 [Guida di riferimento ai messaggi e agli errori di Integration Services](integration-services-error-and-message-reference.md)  
 Vengono elencati i codici di errore predefiniti di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)], oltre ai relativi nomi simbolici e descrizioni.  
  
## <a name="related-sections"></a>Sezioni correlate  
 [Strumenti per la risoluzione dei problemi relativi allo sviluppo dei pacchetti](troubleshooting/troubleshooting-tools-for-package-development.md)  
 Descrive le funzionalità e gli strumenti disponibili in [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] per la risoluzione di problemi relativi ai pacchetti che si verificano durante lo sviluppo.  
  
## <a name="external-resources"></a>Risorse esterne  
  
-   Esempi CodePlex relativi ai [prodotti di Integration Services](https://go.microsoft.com/fwlink/?LinkID=131204) sul sito Web www.codeplex.com/MSFTISProdSamples  
  
## <a name="see-also"></a>Vedere anche  
 [SQL Server Integration Services](sql-server-integration-services.md)  
  
  
