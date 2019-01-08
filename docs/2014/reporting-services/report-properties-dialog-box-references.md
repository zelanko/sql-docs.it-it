---
title: Finestra di dialogo Proprietà report riferimenti | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10530"
- sql12.rtp.rptdesigner.reportproperties.references.f1
ms.assetid: 4639d368-9918-4bb1-9953-7a724ca78dea
author: maggiesmsft
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 628a94ec8e8c79ec88f8427fd2ea41f158ae6c38
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52539786"
---
# <a name="report-properties-dialog-box-references"></a>Finestra di dialogo Proprietà report, Riferimenti
  Selezionare **Riferimenti** nella finestra di dialogo **Proprietà report** per aggiungere o rimuovere riferimenti ad assembly personalizzati o altri assembly esterni e a istanze di classe personalizzate utilizzate da espressioni nella definizione del report.  
  
## <a name="options"></a>Opzioni  
 **Aggiungi o Rimuovi assembly**  
 Consente di visualizzare l'elenco degli assembly a cui il report fa riferimento. È necessario che l'assembly sia disponibile sia nel computer in cui è installato lo strumento utilizzato per progettare il report, sia nel server di report. Il nome del riferimento deve corrispondere il contenuto del  **\<CodeModule >** esattamente i tag nel file di Report Definition Language (RDL).  
  
 **Aggiungi**  
 Fare clic per aggiungere un assembly. Fare clic sul pulsante con puntini di sospensione (...) per aprire la **aprire** nella finestra di dialogo e selezionare gli assembly necessari per completare la valutazione dell'espressione e l'elaborazione report.  
  
 **Elimina**  
 Per rimuovere un riferimento all'assembly dall'elenco, selezionare il nome dell'assembly e fare clic sul pulsante **Rimuovi** .  
  
 **Aggiungi o Rimuovi classi**  
 Consente di visualizzare l'elenco delle istanze di classe utilizzate dal report. L'elenco delle classi viene utilizzato solo dai membri basati sull'istanza e non dai membri statici.  
  
 **Aggiungi**  
 Fare clic per aggiungere un riferimento alle classi. Fare clic sul pulsante con puntini di sospensione (...) per aprire la **aprire** nella finestra di dialogo e selezionare le classi necessarie per completare la valutazione dell'espressione e l'elaborazione report.  
  
 **Elimina**  
 Per eliminare l'istanza di classe, selezionarla e fare clic sul pulsante **Rimuovi** .  
  
 **Su**  
 Per le classi con dipendenze, è possibile spostare il riferimento in un livello superiore dell'elenco.  
  
 **Giù**  
 Per le classi con dipendenze, è possibile spostare il riferimento in un livello inferiore dell'elenco.  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimenti a codice personalizzato e ad assembly in espressioni in Progettazione report &#40;SSRS&#41;](report-design/custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs.md)   
 [Riferimenti a raccolte di variabili di report e di gruppo &#40;Generatore report e SSRS&#41;](report-design/built-in-collections-report-and-group-variables-references-report-builder.md)   
 [Esempi di espressioni &#40;Generatore report e SSRS&#41;](report-design/expression-examples-report-builder-and-ssrs.md)  
  
  
