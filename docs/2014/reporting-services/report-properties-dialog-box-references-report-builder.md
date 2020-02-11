---
title: Finestra di dialogo Proprietà report, riferimenti (Generatore report) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10082"
ms.assetid: 3414c857-8ea6-4fc4-a6d5-b4883c039efa
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 99fe80a22f380bbe1406d357846c4103eeb0083e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66104385"
---
# <a name="report-properties-dialog-box-references-report-builder"></a>Finestra di dialogo Proprietà report, Riferimenti (Generatore report)
  Selezionare **Riferimenti** nella finestra di dialogo **Proprietà report** per aggiungere o rimuovere riferimenti ad assembly personalizzati o altri assembly esterni e a istanze di classe personalizzate utilizzate da espressioni nella definizione del report. Gli assembly personalizzati non sono supportati in modalità locale in Generatore report. Per creare report che utilizzano assembly personalizzati, utilizzare Progettazione report in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
## <a name="options"></a>Opzioni  
 **Aggiungi o rimuovi assembly**  
 Consente di visualizzare l'elenco degli assembly a cui il report fa riferimento. È necessario che l'assembly sia disponibile sia nel computer in cui è installato lo strumento utilizzato per progettare il report, sia nel server di report. Il nome del riferimento deve corrispondere esattamente al contenuto dei tag ** \<CodeModule>** nel file di report Definition Language (con estensione rdl).  
  
 **Aggiungere**  
 Fare clic per aggiungere un assembly. Fare clic sul pulsante con i puntini di sospensione (...) per aprire la finestra di dialogo **Apri** e selezionare gli assembly necessari per completare l'elaborazione del report e la valutazione dell'espressione.  
  
 **Rimuovi**  
 Per rimuovere un riferimento all'assembly dall'elenco, selezionare il nome dell'assembly e fare clic sul pulsante **Rimuovi** .  
  
 **Aggiungi o rimuovi classi**  
 Consente di visualizzare l'elenco delle istanze di classe utilizzate dal report. L'elenco delle classi viene utilizzato solo dai membri basati sull'istanza e non dai membri statici.  
  
 **Aggiungere**  
 Fare clic per aggiungere un riferimento alle classi. Fare clic sul pulsante con i puntini di sospensione (...) per aprire la finestra di dialogo **Apri** e selezionare le classi necessarie per completare l'elaborazione del report e la valutazione dell'espressione.  
  
 **Rimuovi**  
 Per eliminare l'istanza di classe, selezionarla e fare clic sul pulsante **Rimuovi** .  
  
 **Attivo**  
 Per le classi con dipendenze, è possibile spostare il riferimento in un livello superiore dell'elenco.  
  
 **Giù**  
 Per le classi con dipendenze, è possibile spostare il riferimento in un livello inferiore dell'elenco.  
  
## <a name="see-also"></a>Vedere anche  
 [Guida Generatore report per finestre di dialogo, riquadri e procedure guidate](../../2014/reporting-services/report-builder-help-for-dialog-boxes-panes-and-wizards.md)   
 [Espressioni &#40;Generatore report e SSRS&#41;](report-design/expressions-report-builder-and-ssrs.md)  
  
  
