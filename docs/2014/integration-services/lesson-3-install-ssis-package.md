---
title: 'Lezione 3: Installazione dei pacchetti | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
ms.assetid: 87bc4d82-39d8-424f-886f-98cf1e4bb07a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: da763e2385c64a09279c9dd6ff537993c2cd6a30
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62767573"
---
# <a name="lesson-3-installing-packages"></a>Lezione 3: Installazione dei pacchetti
  Nella [Lezione 2: Creazione del pacchetto di distribuzione](../integration-services/lesson-2-create-the-deployment-bundle-in-ssis.md), è stata compilata un'utilità di distribuzione e creazione del pacchetto di distribuzione che contiene gli elementi che è necessario installare i pacchetti in un altro computer. È stato inoltre verificato l'elenco dei file inclusi nel pacchetto di distribuzione ed è stato esaminato il contenuto del file manifesto creato contestualmente all'utilità di distribuzione.  
  
 In questa lezione si procederà alla copia del pacchetto di distribuzione nel computer di destinazione e quindi all'esecuzione dell'Installazione guidata pacchetti per installare i pacchetti, le rispettive dipendenze e i file ausiliari nel computer. I pacchetti verranno installati nel database **msdb** di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e gli altri elementi nel file system. Dopo aver completato l'installazione dei pacchetti, questi ultimi verranno eseguiti in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] mediante l'Utilità di esecuzione pacchetti allo scopo di testare la distribuzione.  
  
 **Tempo stimato per il completamento della lezione:** 30 minuti  
  
## <a name="lesson-tasks"></a>Argomenti della lezione  
 In questa lezione sono incluse le attività seguenti:  
  
-   [Passaggio 1: Copia del pacchetto di distribuzione](../integration-services/lesson-3-1-copying-the-deployment-bundle.md)  
  
-   [Passaggio 2: Esecuzione dell'Installazione guidata pacchetti](../integration-services/lesson-3-2-running-the-package-installation-wizard.md)  
  
-   [Passaggio 3: Test dei pacchetti distribuiti](../integration-services/lesson-3-3-testing-the-deployed-packages.md)  
  
## <a name="start-the-lesson"></a>Inizio della lezione  
 [Passaggio 1: Copia del pacchetto di distribuzione](../integration-services/lesson-3-1-copying-the-deployment-bundle.md)  
  
![Icona di Integration Services (piccola)](media/dts-16.gif "icona di Integration Services (piccola)")**rimangono fino a Date con Integration Services**<br /> Per i download, gli articoli, gli esempi e i video Microsoft più recenti, oltre alle soluzioni selezionate dalla community, visitare la pagina [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] sul sito MSDN:<br /><br /> [Visita la pagina di Integration Services su MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Per ricevere una notifica automatica su questi aggiornamenti, sottoscrivere i feed RSS disponibili nella pagina.  
  
  
