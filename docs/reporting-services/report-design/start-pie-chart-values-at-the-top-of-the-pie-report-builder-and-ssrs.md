---
title: Iniziare a visualizzare i valori del grafico a torta dalla parte superiore (Generatore report) | Microsoft Docs
description: Informazioni su come iniziare a visualizzare i valori del grafico a torta dalla parte superiore del grafico anziché a 90 gradi dalla cima della torta (impostazione predefinita).
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: d0e6fb59-ca4e-4d70-97cb-0ad183da21d3
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: b1158cf4a88bb491b8ed1cb492eec1c3021cb6f9
ms.sourcegitcommit: ea0bf89617e11afe85ad85309e0ec731ed265583
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/28/2020
ms.locfileid: "92907059"
---
# <a name="start-pie-chart-values-at-the-top-of-the-pie-report-builder-and-ssrs"></a>Inizio della visualizzazione dei valori del grafico a torta dalla parte superiore (Generatore report e SSRS)
Per impostazione predefinita, nei grafici a torta dei report impaginati di [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] il primo valore nel set di dati inizia a 90 gradi dalla cima della torta. 

![Screenshot di un grafico a torta di Generatore report con il set di dati a partire da 90 gradi.](../../reporting-services/media/report-builder-pie-chart-start-at-90.png)

*I valori del grafico iniziano a 90 gradi.*

È possibile far iniziare il primo valore dalla cima della torta. 

![Screenshot di un grafico a torta di Generatore report con il set di dati a partire dalla cima.](../../reporting-services/media/report-builder-pie-chart-start-at-top.png)

*I valori del grafico iniziano dalla cima della torta.*
  
## <a name="to-start-the-pie-chart-at-the-top-of-the-pie"></a>Per fare iniziare il grafico a torta dalla cima della torta  
  
1.  Fare clic sulla torta stessa.  
  
2.  Se il riquadro **Proprietà** non è visualizzato, fare clic su **Proprietà** nella scheda **Visualizza**  
  
3.  Nel riquadro **Proprietà** , sotto **Attributi personalizzati** modificare **PieStartAngle** da **0** a **270**.  
  
4.  Fare clic su **Esegui** per visualizzare l'anteprima del report.  
  
 Il primo valore inizia ora all'inizio del grafico a torta.  
  
## <a name="see-also"></a>Vedere anche  
 [Formattazione di un grafico &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/formatting-a-chart-report-builder-and-ssrs.md)   
 [Grafici a torta &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/pie-charts-report-builder-and-ssrs.md)  
  
  
