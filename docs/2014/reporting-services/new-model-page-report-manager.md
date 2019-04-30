---
title: Pagina nuovo modello (gestione Report) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 27d5bf66-b0e7-489e-a830-ffe2ec8e5350
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: b0d571210c44026fc34ab43cb07e18bbd8526ed5
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63188422"
---
# <a name="new-model-page-report-manager"></a>Pagina Nuovo modello (Gestione report)
  Questa pagina consente di generare un modello di report predefinito da un'origine dati condivisa. È possibile generare modelli di report solo da origini dati multidimensionali di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , origini dati relazionali di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e origini dati relazionali di Oracle.  
  
 I modelli generati in Gestione report sono basati sullo schema dell'origine dati condivisa. Per tutte le tabelle e le colonne nell'origine dati vengono creati entità, cartelle e campi. Non è possibile escludere elementi, né impostare opzioni che determinano come viene generato il modello. Se si desidera personalizzare o modificare un modello, è invece necessario utilizzare Progettazione modelli.  
  
## <a name="navigation"></a>Navigazione  
 Utilizzare la procedura riportata di seguito per navigare fino a questo percorso nell'interfaccia utente.  
  
###### <a name="to-open-the-new-model-page"></a>Per aprire la pagina Nuovo modello  
  
1.  Aprire Gestione report e individuare l'origine dati condivisa per la quale si desidera generare un modello.  
  
2.  Passare con il puntatore del mouse sull'origine dati, quindi fare clic sulla freccia a discesa.  
  
3.  Nel menu a discesa, eseguire uno dei passaggi seguenti:  
  
    -   Fare clic su **Genera modello di report** per aprire la pagina Nuovo modello.  
  
    -   Fare clic su **Gestisci** per aprire la pagina delle proprietà Generale per il report. Successivamente, fare clic su **Genera modello** per aprire la pagina Nuovo modello.  
  
## <a name="options"></a>Opzioni  
 **Name**  
 Consente di specificare il nome del modello. Il nome deve includere almeno un carattere alfanumerico. È inoltre possibile utilizzare spazi e alcuni simboli. Il nome non può contenere i caratteri seguenti:  
  
 ; ? : \@ & = + , $ / * \< > | " /  
  
 **Descrizione**  
 Indica una descrizione del modello. Gli utenti che visualizzano questo elemento tramite Gestione report possono vedere questa descrizione durante l'esplorazione della gerarchia di cartelle.  
  
 **Cambia percorso**  
 Consente di visualizzare il percorso della cartella per il nuovo modello. È possibile fare clic sul pulsante **Cambia percorso** per selezionare un percorso diverso.  
  
  
