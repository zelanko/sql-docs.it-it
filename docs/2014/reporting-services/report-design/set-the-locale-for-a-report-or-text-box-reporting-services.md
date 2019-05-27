---
title: Definire le impostazioni locali per un report o una casella di testo (Reporting Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- locales [Reporting Services]
ms.assetid: df115b01-184b-47f0-b5ec-0ad965ff9bee
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: d65c02df74cb89fca3d861f01c01da87ff589e3a
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66104984"
---
# <a name="set-the-locale-for-a-report-or-text-box-reporting-services"></a>Definizione delle impostazioni locali per un report o una casella di testo (Reporting Services)
  Nella proprietà **Language** di un report o di una casella di testo sono contenute le impostazioni locali che determinano i formati predefiniti per la visualizzazione dei dati del report che differiscono in base alla lingua e al paese, ad esempio i valori relativi alla data o alla valuta o quelli numerici. La proprietà **Language** di una casella di testo ha la priorità rispetto alla proprietà **Language** impostata per il report. Se non viene specificato alcun valore per **Language**, in Reporting Services vengono utilizzate le impostazioni locali del sistema operativo nel server di report per i report pubblicati o del computer di creazione di report per l'anteprima del report.  
  
 Per i report HTML, è possibile ignorare il valore **Language** predefinito e usare la lingua specificata dall'intestazione HTTP del client del browser utilizzando il campo predefinito User!Language in un'espressione per la proprietà **Language** di un report o di una casella di testo.  
  
 È inoltre possibile specificare la proprietà **Language** per un report in un URL. Per altre informazioni, vedere [Impostare la lingua per i parametri del report in un URL](../set-the-language-for-report-parameters-in-a-url.md).  
  
### <a name="to-set-the-locale-for-a-report"></a>Per definire le impostazioni locali per un report  
  
1.  Nella visualizzazione della struttura fare clic all'esterno dell'area di progettazione del report per selezionarlo.  
  
2.  Nel riquadro Proprietà digitare o selezionare per la proprietà **Language** la lingua da utilizzare per il report.  
  
### <a name="to-set-the-locale-for-a-text-box"></a>Per definire le impostazioni locali per una casella di testo  
  
1.  Nella visualizzazione della struttura selezionare la casella di testo cui si desidera applicare le impostazioni locali.  
  
2.  Nel riquadro Proprietà effettuare le operazioni seguenti:  
  
    -   Per la proprietà **Calendar** , digitare o selezionare il calendario che si desidera utilizzare per le date.  
  
    -   Per la proprietà **Direction** digitare o selezionare la direzione in cui è scritto il testo.  
  
    -   Per la proprietà **Language** , digitare o selezionare la lingua che si desidera utilizzare per la casella di testo. Questo valore ha la priorità rispetto alla proprietà **Language** per il report.  
  
    -   Per la proprietà **NumeralLanguage** , digitare o selezionare il formato da utilizzare per i numeri presenti nella casella di testo.  
  
    -   Per la proprietà **NumeralVariant** digitare o selezionare la variante del formato da utilizzare per i numeri nella casella di testo.  
  
    -   Per la proprietà **UnicodeBiDi** selezionare il livello di incorporamento bidirezionale da utilizzare nella casella di testo.  
  
## <a name="see-also"></a>Vedere anche  
 [Utilizzo delle espressioni nei report &#40;Generatore report e SSRS&#41;](expression-uses-in-reports-report-builder-and-ssrs.md)  
  
  
