---
title: Aprire un report per dispositivi mobili con parametri della stringa di query specifici | Microsoft Docs
description: Per un report per dispositivi mobili di Reporting Services con parametri e un'origine dati, è possibile usare i parametri di query nell'URL del report per aprirlo con i valori specificati.
ms.date: 10/25/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: mobile-reports
ms.topic: conceptual
ms.assetid: 4eeb3204-e207-4ac0-aff3-bfc4926e5754
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: abcdda5a396451508df78610eeb4f7bc417484d5
ms.sourcegitcommit: ea0bf89617e11afe85ad85309e0ec731ed265583
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/28/2020
ms.locfileid: "92907349"
---
# <a name="open-a-mobile-report-with-specific-query-string-parameters--reporting-services"></a>Aprire un report per dispositivi mobili con parametri della stringa di query specifici | Reporting Services
Se si ha un report per dispositivi mobili [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] con parametri e [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] o [!INCLUDE[ssASnoversion_md](../../includes/ssasnoversion-md.md)] come origine dati, è possibile includere i parametri della stringa di query nell'URL del report in modo che si apra automaticamente con i valori specificati. 
1.  Creare un [report per dispositivi mobili con parametri](../../reporting-services/mobile-reports/add-parameters-to-a-mobile-report-reporting-services.md).

2. Aprire il report in Mobile Report Publisher e selezionare la scheda Dati. 

2. Trovare il nome del set di dati nella scheda nella parte inferiore della tabella e il nome del campo desiderato. 
    
    ![Screenshot della visualizzazione dati del parametro in Mobile Report Publisher.](../../reporting-services/mobile-reports/media/mobile-report-publisher-parameter-data-view.png)
    
2.  La sintassi dell'URL dipende dall'origine dati. 

     **Se l'origine dati è SQL Server Analysis Services** : Creare un URL con un parametro della stringa di query in questo formato:

    `https://<servername>/reports/<report-folder-name>/<report-name>?<dataset-name>.<field-name>=<parameter-value>`

    Ad esempio:
    
    `https://sampleserver/reports/adventureworks-reports/adventureworks-load-on-demand?TimeChartLoD.category=Clothing` 
    
     **Se l'origine dati è SQL Server** : il parametro della stringa di query è quasi uguale, ma presenta il simbolo \@ davanti al nome del campo:

    `https://<servername>/reports/<report-folder-name>/<report-name>?<dataset-name>.@<field-name>=<parameter-value>`

    Ad esempio:
    
      `https://sampleserver/reports/adventureworks-reports/adventureworks-load-on-demand?TimeChartLoD.@category=Clothing` 

    
3.  Questo URL aprirà il report nel server, filtrato automaticamente in base al valore del parametro specificato.

    ![Screenshot della visualizzazione portale Web del parametro in Mobile Report Publisher con una freccia che punta all'URL e un riquadro attorno al testo: ?TimeChartLoD.@category=Clothing.](../../reporting-services/mobile-reports/media/mobile-report-publisher-parameter-web-portal-view.png)

### <a name="see-also"></a>Vedere anche

[Aggiungere parametri a un report per dispositivi mobili](../../reporting-services/mobile-reports/add-parameters-to-a-mobile-report-reporting-services.md)

