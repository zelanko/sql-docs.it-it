---
title: Cercare un report tramite l'accesso con URL | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- searching reports
- text searches [Reporting Services]
- URL access [Reporting Services], report searches
ms.assetid: 6f3410c4-7944-448f-bae8-bab3e8152d46
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: e0296acddd21319949ff2f76757c5297eb1bceb4
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56023790"
---
# <a name="search-a-report-using-url-access"></a>Cercare un report tramite l'accesso con URL
  È possibile cercare in un report del testo specifico utilizzando l'accesso tramite URL. Per eseguire una ricerca in un report, impostare il valore del parametro *rc:FindString* nell'URL affinché corrisponda al testo da cercare. Inoltre, usare i parametri *rc:StartFind* e *rc:EndFind* per restringere la ricerca alle pagine specifiche all'interno del report.  
  
## <a name="example"></a>Esempio  
 Nell'esempio di accesso tramite URL seguente viene cercata la prima occorrenza del testo "Mountain-400" nel report di esempio Product Catalog a partire da pagina uno fino a pagina cinque:  
  
```  
http://server/Reportserver?/SampleReports/Product Catalog&rs:Command=Render&rc:StartFind=1&rc:EndFind=5&rc:FindString=Mountain-400  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Accesso con URL &#40;SSRS&#41;](url-access-ssrs.md)   
 [Riferimento ai parametri di accesso con URL](url-access-parameter-reference.md)  
  
  
