---
title: Impostare e configurare le unità di misura (Generatore report e SSRS) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: a15a96c3-7d2c-433e-a440-4ea051e967a9
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 48700208f4ff67c9f6b6932537558c283df13ee6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65576660"
---
# <a name="set-and-configure-measurement-units-report-builder-and-ssrs"></a>Impostare e configurare le unità di misura (Generatore report e SSRS)
  In un report impaginato di [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] gli indicatori usano una di due unità di misure, ovvero percentuale o numerica.   
    
  Per impostazione predefinita, gli indicatori vengono configurati in modo da utilizzare le percentuali come unità di misura. Pertanto i valori dell'indicatore assegnati a ogni icona nel set di indicatori sono determinati da un intervallo di percentuale. Gli intervalli di percentuale sono divisi uniformemente tra le icone nel set di indicatori. Ogni icona rappresenta uno stato dell'indicatore. È possibile modificare le percentuali per ogni icona nel set di indicatori specificando percentuali di inizio e di fine differenti. Gli indicatori rilevano automaticamente anche i valori minimo e massimo nei dati.  
  
 L'unità di misura può essere cambiata in valore numerico. In tal caso, non è possibile specificare i valori minimo o massimo per i dati; al contrario, vengono forniti solo i valori iniziali e finali per ogni icona utilizzata dall'indicatore.  
  
 Opzioni come le unità di misura possono essere impostate tramite espressioni. Per altre informazioni, vedere [Espressioni &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md).  
  
## <a name="to-use-the-numeric-state-measurement-unit"></a>Per utilizzare l'unità di misura di stato numerica  
  
1.  Fare clic con il pulsante destro del mouse sull'indicatore da modificare e scegliere **Proprietà indicatore**.  
  
2.  Fare clic su **Valori e stati** nel riquadro sinistro.  
  
3.  Nell'elenco **Unità di misura stati** fare clic su **Numerico**.  
  
     Facoltativamente, fare clic sul pulsante **Espressione** (*fx*) per modificare un'espressione che consente di impostare il valore per l'opzione.  
  
4.  Per ogni icona nel set di indicatori, aggiornare i valori nelle caselle di testo **Iniziale** e **Finale** .  
  
     Facoltativamente, fare clic sul pulsante **Espressione** (*fx*) per modificare un'espressione che consente di impostare i valori delle opzioni **Iniziale** e **Finale** .  
  
    > [!NOTE]  
    >  I valori nelle caselle di testo **Iniziale** e **Finale** devono essere numerici.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="to-use-the-percentage-measurement-unit"></a>Per utilizzare l'unità di misura espressa in percentuale  
  
1.  Fare clic con il pulsante destro del mouse sull'indicatore da modificare e scegliere **Proprietà indicatore**.  
  
2.  Scegliere **Valori e stati** dal riquadro sinistro.  
  
3.  Nell'elenco **Unità di misura stati** fare clic su **Percentuale**.  
  
     Facoltativamente, fare clic sul pulsante **Espressione** (*fx*) per modificare un'espressione che consente di impostare il valore per l'opzione.  
  
4.  Facoltativamente, modificare le opzioni **Minimo** e **Massimo** per usare valori specifici invece di rilevare automaticamente i valori minimo e massimo dei dati usati dall'indicatore. Il valore di **Minimo** deve essere minore di quello indicato dal valore di **Massimo**.  
  
    > [!NOTE]  
    >  Se si impostano in modo esplicito i valori minimo e massimo, quell'intervallo di valori viene utilizzato dall'indicatore indipendentemente dai valori minimo e massimo effettivi nei dati. Pertanto, i valori inferiori al valore minimo e superiori a quello massimo sono esclusi dalla valutazione che determina quale icona dell'indicatore mostrare nel report.  
  
     Facoltativamente, fare clic sul pulsante **Espressione** (*fx*) per modificare un'espressione che consente di impostare i valori per l'opzione.  
  
5.  Per ogni icona nel set di indicatori, aggiornare i valori nelle caselle di testo **Iniziale** e **Finale** .  
  
     Facoltativamente, fare clic sul pulsante **Espressione** (*fx*) per modificare un'espressione che consente di impostare i valori delle opzioni **Iniziale** e **Finale** .  
  
    > [!NOTE]  
    >  I valori nelle caselle di testo **Iniziale** e **Finale** devono essere numerici.  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Indicatori &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/indicators-report-builder-and-ssrs.md)  
  
  
