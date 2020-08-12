---
title: Risolvere i problemi relativi ai grafici (Generatore report) | Microsoft Docs
description: Per visualizzare un valore numerico, usare campi con tipi di dati numerici lungo l'asse dei valori, anziché numeri formattati.
ms.date: 01/17/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 3a327ffa-3b69-40d6-8015-cc01cfae9161
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 45894eca20fa5762eb4f2e02496e79bd327c8fb3
ms.sourcegitcommit: 5b7457c9d5302f84cc3baeaedeb515e8e69a8616
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/20/2020
ms.locfileid: "83689464"
---
# <a name="troubleshoot-charts-report-builder-and-ssrs"></a>Risoluzione dei problemi relativi ai grafici (Generatore report e SSRS)
  Queste informazioni possono essere utili in caso di utilizzo di grafici.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="why-does-my-chart-count-not-sum-the-values-on-the-value-axis"></a>Nel grafico viene eseguito il conteggio, anziché la somma, dei valori sull'asse dei valori  
 Per tracciare correttamente la maggior parte dei grafici, sono necessari valori numerici lungo l'asse dei valori, che in genere corrisponde all'asse Y. Se il tipo di dati del campo valori è **String**, non sarà possibile visualizzare un valore numerico, neanche se nei campi sono presenti numeri. Viene invece visualizzato un conteggio del numero totale di righe che contengono un valore in tale campo. Per evitare questo comportamento, assicurarsi che i campi utilizzati per le serie di valori abbiano tipi di dati numerici anziché stringhe che contengono numeri formattati.  

## <a name="need-more-help"></a>Per ulteriore assistenza  
   
  Soluzione:  
 * [SQL Server Reporting Services](https://stackoverflow.com/questions/tagged/reporting-services) su Stack Overflow  
 * Inserire un problema o un suggerimento in [Microsoft SQL Server UserVoice](https://feedback.azure.com/forums/908035-sql-server).  
  
## <a name="see-also"></a>Vedere anche  
 [Grafici &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)  
  
  
