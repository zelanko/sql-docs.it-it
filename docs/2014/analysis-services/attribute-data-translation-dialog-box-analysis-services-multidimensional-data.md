---
title: Finestra di dialogo Traduzione dati attributo (Analysis Services-Dati multidimensionali) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.dimensiondesigner.dimensionstoragesettings.f1
helpviewer_keywords:
- Attribute Data Translation dialog box
ms.assetid: bed286de-1e9b-49de-b09e-3cd076aba152
author: minewiskan
ms.author: owend
ms.openlocfilehash: 76af68a7f9668b46a55a3bf28f9cf07dd64766aa
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/08/2020
ms.locfileid: "84527927"
---
# <a name="attribute-data-translation-dialog-box-analysis-services---multidimensional-data"></a>Finestra di dialogo Traduzione dati attributo (Analysis Services - Dati multidimensionali)
  Usare la finestra di dialogo **Traduzione dati attributo** per impostare la colonna contenente i dati della didascalia della traduzione, nonché le regole di confronto e il tipo di ordinamento da usare per i dati tradotti. Per visualizzare la finestra di dialogo **Traduzione dati attributo** , è possibile:  
  
-   Fare clic su **Nuova colonna didascalia** o **Modifica colonna didascalia** nel riquadro **Barra degli strumenti** della scheda **Traduzioni** di **Progettazione dimensioni**.  
  
-   Fare clic con il pulsante destro del mouse sul riquadro relativo ai **dettagli di traduzione** della scheda **Traduzioni** di **Progettazione dimensioni** e scegliere **Nuova colonna didascalia** o **Modifica colonna didascalia**.  
  
## <a name="options"></a>Opzioni  
 **Attributo**  
 Consente di visualizzare l'attributo selezionato.  
  
 **Lingua**  
 Consente di visualizzare la lingua selezionata.  
  
 **Didascalia tradotta**  
 Consente di impostare la didascalia tradotta corrente per l'attributo selezionato.  
  
 **Colonne per la traduzione**  
 Consente di impostare la colonna in cui vengono archiviati i dati della didascalia della traduzione. È possibile selezionare solo una colonna. Verranno visualizzate tutte le tabelle correlate a cui fa riferimento la tabella primaria delle dimensioni.  
  
 **Designazione regole di confronto**  
 Consente di impostare la designazione delle regole di confronto per l'attributo selezionato. Per impostazione predefinita, sono selezionate le regole di confronto di Windows. Fare clic sulla freccia rivolta verso il basso per eseguire una selezione dalle regole di confronto disponibili.  
  
 **Binario**  
 Selezionare questa opzione per ordinare e confrontare i dati in base agli schemi di bit definiti per ogni carattere. Il tipo di ordinamento binario prevede la distinzione tra maiuscole e minuscole, ovvero i caratteri minuscoli precedono quelli maiuscoli, e la distinzione tra caratteri accentati e non accentati. Si tratta del tipo di ordinamento più rapido.  
  
 Se questa opzione non è selezionata, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] segue le regole di ordinamento e confronto definite nei dizionari relativi alla lingua o all'alfabeto associato.  
  
> [!NOTE]  
>  La selezione di questa opzione comporta la disabilitazione delle opzioni **Maiuscole/minuscole**, **Accentati/non accentati**, **Distinzione Kana**e **Distinzione larghezza** .  
  
 **Distinzione maiuscole/minuscole**  
 Selezionare questa opzione per ordinare e confrontare i dati in base alle regole del dizionario specificate per la lingua o l'alfabeto associato, nonché per distinguere tra lettere maiuscole e minuscole.  
  
 Se l'opzione non viene selezionata, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] considera uguali le versioni maiuscole e minuscole delle lettere. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]non definisce se le lettere minuscole vengono ordinate più in basso o più in alto rispetto alle lettere maiuscole quando la **distinzione tra maiuscole** e minuscole non è selezionata.  
  
 **supportano la distinzione tra caratteri accentati e non accentati**  
 Selezionare questa opzione per ordinare e confrontare i dati in base alle regole del dizionario specificate per la lingua o l'alfabeto associato, nonché per distinguere tra lettere accentate e non accentate. Il carattere 'a' non viene ad esempio considerato uguale ad 'à'.  
  
 Se l'opzione non viene selezionata, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] considera uguali le versioni accentate e non accentate delle lettere.  
  
 **Distinzione Kana**  
 Selezionare questa opzione per ordinare e confrontare i dati in base alle regole del dizionario specificate per la lingua o l'alfabeto associato, nonché per distinguere tra i due tipi di caratteri Kana giapponesi, ovvero Hiragana e Katakana.  
  
 Se l'opzione non viene selezionata, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] considera uguali i caratteri Hiragana e Katakana.  
  
 **Distinzione larghezza**  
 Selezionare questa opzione per eseguire l'ordinamento e il confronto in base alle regole del dizionario specificate per la lingua o l'alfabeto associato, nonché per distinguere tra la rappresentazione a un byte, ovvero a metà larghezza, e la rappresentazione a due byte, ovvero a larghezza intera, dello stesso carattere.  
  
 Se questa opzione non è selezionata, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] SQL Server considera uguali la rappresentazione a un byte e quella a due byte dello stesso carattere.  
  
## <a name="see-also"></a>Vedere anche  
 [Finestre di progettazione e finestre di dialogo Analysis Services &#40;dati multidimensionali&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [Dettagli traduzione &#40;scheda Traduzioni, Progettazione dimensioni&#41; &#40;Analysis Services Dati multidimensionali&#41;](translation-details-dimension-designer-analysis-services-multidimensional-data.md)  
  
  
