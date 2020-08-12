---
title: Concetti relativi ai parametri di report (Generatore report) | Microsoft Docs
description: Come aggiungere parametri per collegare report correlati, controllare l'aspetto di un report, filtrare i dati del report o limitare l'ambito in Generatore report.
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: b0aa2159-4e49-4713-8824-5ef9a9edbc62
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: e6e6419e43991ff2dfe28ea0e3f6b2033693b9c3
ms.sourcegitcommit: 02b22274da4a103760a376c4ddf26c4829018454
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/11/2020
ms.locfileid: "84681600"
---
# <a name="report-parameters-concepts-report-builder-and-ssrs"></a>Concetti relativi ai parametri di report (Generatore report e SSRS)
  È possibile aggiungere parametri a un report per collegare report correlati, controllare l'aspetto del report, filtrare i dati del report o per limitare l'ambito di un report a percorsi o utenti specifici.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
 I parametri di report vengono creati nei modi seguenti:  
  
-   Automaticamente, quando si definisce la query del set di dati contenente le variabili di query. Per ogni variabile di query, vengono creati un parametro del report e un parametro di query del set di dati con lo stesso nome. Un parametro di query può essere un riferimento a una variabile do query o a un parametro di input per una stored procedure.  
  
-   Automaticamente, quando si aggiunge un riferimento a un set di dati condiviso contenente parametri di query.  
  
-   Manualmente, quando si creano parametri del report nel riquadro dei dati del report. I parametri rappresentano una delle raccolte predefinite che è possibile includere in un'espressione di un report. Poiché le espressioni sono usate per definire valori nell'intera definizione di un report, è possibile usare i parametri per controllare l'aspetto del report o per passare i valori ai sottoreport o report correlati che usano anch'essi i parametri.  
  
 Per ulteriori informazioni, vedere la pagina relativa al [Parametri report &#40;Generatore report e Progettazione report&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md).  
  
 I parametri sono usati di frequente per filtrare i dati del report sia prima che dopo la restituzione dei dati al report. Per altre informazioni, vedere [Filtro, raggruppamento e ordinamento di dati &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md).  
  
 Quando si progetta un report, i parametri corrispondenti vengono salvati nella definizione del report. Quando si pubblica un report, i parametri corrispondenti vengono salvati e gestiti separatamente della definizione del report. Una volta salvato il report nel server di report, è possibile eseguire le operazioni seguenti:  
  
-   Modificare i valori dei parametri del report direttamente nel server di report indipendentemente dalla definizione del report.  
  
-   Creare più report collegati in cui ogni report collegato è un collegamento alla definizione del report con un set di valori di parametro separato che può essere gestito indipendentemente nel server di report.  
  
 Se si intende creare snapshot, cronologie o sottoscrizioni di report in un report pubblicato, è necessario capire come i parametri del report influiscono sui requisiti di progettazione per il report.  
  
## <a name="see-also"></a>Vedere anche  
 [Concetti relativi a Reporting Services (SSRS)](../reporting-services-concepts-ssrs.md) [Set di dati condivisi e incorporati del report &#40;Generatore report e SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)   
 [Esercitazione: Aggiungere un parametro al report &#40;Generatore report&#41;](../../reporting-services/tutorial-add-a-parameter-to-your-report-report-builder.md)  
  
  
