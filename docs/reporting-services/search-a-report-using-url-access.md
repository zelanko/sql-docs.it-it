---
title: Cercare un report tramite l'accesso con URL | Microsoft Docs
description: Informazioni su come cercare un report tramite l'accesso con URL. Impostare ad esempio il valore del parametro rc:FindString nell'URL affinché corrisponda al testo da cercare.
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
helpviewer_keywords:
- searching reports
- text searches [Reporting Services]
- URL access [Reporting Services], report searches
ms.assetid: 6f3410c4-7944-448f-bae8-bab3e8152d46
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: c7d5ba7b312bb89942fd899f4c769179a0c97bab
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/28/2020
ms.locfileid: "87238433"
---
# <a name="search-a-report-using-url-access"></a>Cercare un report tramite l'accesso con URL
  È possibile cercare in un report del testo specifico utilizzando l'accesso tramite URL. Per eseguire una ricerca in un report, impostare il valore del parametro *rc:FindString* nell'URL affinché corrisponda al testo da cercare. Inoltre, usare i parametri *rc:StartFind* e *rc:EndFind* per restringere la ricerca alle pagine specifiche all'interno del report.  
  
## <a name="example"></a>Esempio  
 Nell'esempio di accesso tramite URL seguente viene cercata la prima occorrenza del testo "Mountain-400" nel report di esempio Product Catalog a partire da pagina uno fino a pagina cinque:  
  
```  
https://server/Reportserver?/SampleReports/Product Catalog&rs:Command=Render&rc:StartFind=1&rc:EndFind=5&rc:FindString=Mountain-400  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Accesso con URL &#40;SSRS&#41;](../reporting-services/url-access-ssrs.md)   
 [Riferimento ai parametri di accesso con URL](../reporting-services/url-access-parameter-reference.md)  
  
  
