---
title: Finestra di dialogo Accesso a Reporting Services (SSRS) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: tools
ms.topic: reference
f1_keywords:
- sql13.rtp.rptdesigner.reportservicelogin.f1
ms.assetid: 2037d797-0b61-44c7-931f-6c689c3fc733
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 25d2741a8449875852c733aa763322011834a6b1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65581273"
---
# <a name="reporting-services-login-dialog-box-ssrs"></a>Finestra di dialogo Accesso a Reporting Services (SSRS)
  Utilizzare la finestra di dialogo **Accesso a Reporting Services** per specificare le credenziali per la pubblicazione di report nel server di report.  
  
-   **Nota** La prima volta che si pubblica un report in un server di report dopo aver impostato la proprietà di distribuzione **TargetServerURL** per un progetto, verificare che il nome del server includa **server** e non **report**. Ad esempio, `https://localhost/reportserver`e non `https://localhost/reports`. Se si specifica la directory `reports` nel server locale anziché la directory `reportserver` , verrà visualizzata questa finestra di dialogo. Per altre informazioni sull'impostazione **TargetServerURL**, vedere [Impostare le proprietà di distribuzione &#40;Reporting Services&#41;](../../reporting-services/tools/set-deployment-properties-reporting-services.md).  
  
## <a name="options"></a>Opzioni  
 **Server**  
 Indica il nome del server di report. Ad esempio, `https://localhost/reportserver`. Per i server di report che utilizzano una porta diversa da quella predefinita, ovvero 80, includere il numero di porta. Ad esempio, `https://localhost:81/reportserver`.  
  
 **User name**  
 Consente di digitare il nome utente da utilizzare per l'accesso al servizio Web.  
  
 **Password**  
 Consente di digitare la password da utilizzare per l'accesso al servizio Web.  
  
## <a name="see-also"></a>Vedere anche  
 [Connessioni dati, origini dati e stringhe di connessione &#40;Generatore report e SSRS&#41;](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)   
 [Specificare le credenziali e le informazioni sulla connessione per le origini dati del report](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md)   
 [Guida sensibile al contesto di Progettazione report](../../reporting-services/tools/report-designer-f1-help.md)  
  
  
