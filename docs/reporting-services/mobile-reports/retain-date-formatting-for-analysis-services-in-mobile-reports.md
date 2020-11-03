---
title: Mantenere la formattazione della data per i dati di Analysis Services nei report per dispositivi mobili | Reporting Services | Microsoft Docs
description: In Mobile Report Publisher aggiungere una misura a un set di dati condiviso in Generatore report in modo che le date nelle origini dati di Analysis Services mantengano il tipo di dati.
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: mobile-reports
ms.topic: conceptual
ms.assetid: e9a9a199-40e3-4381-b250-1b99fb83aa62
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 5fef66452820975107e06e20a4085978163d957d
ms.sourcegitcommit: ea0bf89617e11afe85ad85309e0ec731ed265583
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/28/2020
ms.locfileid: "92907085"
---
# <a name="retain-date-formatting-for-analysis-services-in-mobile-reports"></a>Mantieni date (formattazione) per Analysis Services nei report per dispositivi mobili
Aggiungere una misura a un set di dati condiviso in Generatore report in modo che le date nelle origini dati di [!INCLUDE[ssASnoversion_md](../../includes/ssasnoversion-md.md)] mantengano il tipo di dati in [!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-short.md)].

Il tipo restituito predefinito per le query di [!INCLUDE[ssASnoversion_md](../../includes/ssasnoversion-md.md)] è una stringa.  Quando si compila un set di dati nel Generatore report di [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] , il tipo di stringa viene rispettato e salvato nel server. 

Tuttavia, quando il renderer della tabella JSON elabora il set di dati, legge il valore della colonna come stringa ed esegue il rendering delle stringhe.  Anche quando [!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-long.md)] recupera la tabella, visualizza solo stringhe.

La soluzione alternativa consiste nell'aggiungere un membro calcolato quando si crea un set di dati condiviso in Generatore report. Tale soluzione funziona con i modelli di [!INCLUDE[ssASnoversion_md](../../includes/ssasnoversion-md.md)] multidimensionali e tabulari.

## <a name="create-a-measure-to-retain-a-date-field-data-type"></a>Creare una misura per mantenere un tipo di dati del campo relativo alla data

1. Creare una misura per contenere il valore del campo relativo alla data in questione e nel campo relativo all'espressione scegliere il livello o la gerarchia della data e aggiungere **.CurrentMember.MemberValue**. Ad esempio:
 
   [Internet Sales].[Data spedizione].CurrentMember.MemberValue
   
   ![Screenshot della finestra di dialogo Generatore membri calcolati con la casella di testo Espressione evidenziata.](../../reporting-services/mobile-reports/media/ssas-calculated-member-report-builder.png)
   
2. A questo punto è possibile aggiungere il membro calcolato al set di colonne trascinandolo dall'elenco di membri calcolati in basso a sinistra e rilasciandolo nella griglia di colonne a destra.  

   ![Screenshot della finestra Progettazione query con la sezione Membri calcolati evidenziata.](../../reporting-services/mobile-reports/media/ssas-query-designer-calculated-member-report-builder.png) 
   
### <a name="see-also"></a>Vedere anche

-  [Dati per report di Reporting Services per dispositivi mobili](../../reporting-services/mobile-reports/data-for-reporting-services-mobile-reports.md)
-  [Preparare i dati per i report per dispositivi mobili di Reporting Services](../../reporting-services/mobile-reports/prepare-data-for-reporting-services-mobile-reports.md)
