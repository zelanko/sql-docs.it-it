---
title: Finestra di dialogo Accesso a Reporting Services | Microsoft Docs
description: Informazioni su come usare la finestra di dialogo Accesso a Reporting Services per specificare le credenziali per la pubblicazione di report nel server di report.
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
ms.openlocfilehash: 4d3e34d7ff9f92506f1225aea173521ee7d30e79
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/22/2020
ms.locfileid: "86919617"
---
# <a name="reporting-services-login-dialog-box-ssrs"></a>Finestra di dialogo Accesso a Reporting Services (SSRS)
  Utilizzare la finestra di dialogo **Accesso a Reporting Services** per specificare le credenziali per la pubblicazione di report nel server di report.  
  
-   **Nota** La prima volta che si pubblica un report in un server di report dopo aver impostato la proprietà di distribuzione **TargetServerURL** per un progetto, verificare che il nome del server includa **server** e non **report**. Ad esempio, `https://localhost/reportserver`e non `https://localhost/reports`. Se si specifica la directory `reports` nel server locale anziché la directory `reportserver` , verrà visualizzata questa finestra di dialogo. Per altre informazioni sull'impostazione **TargetServerURL**, vedere [Impostare le proprietà di distribuzione &#40;Reporting Services&#41;](../../reporting-services/tools/set-deployment-properties-reporting-services.md).  
  
## <a name="options"></a>Opzioni  
 **Server**  
 Indica il nome del server di report. Ad esempio: `https://localhost/reportserver`. Per i server di report che utilizzano una porta diversa da quella predefinita, ovvero 80, includere il numero di porta. Ad esempio: `https://localhost:81/reportserver`.  
  
 **Nome utente**  
 Consente di digitare il nome utente da utilizzare per l'accesso al servizio Web.  
  
 **Password**  
 Consente di digitare la password da utilizzare per l'accesso al servizio Web.  
  
## <a name="see-also"></a>Vedere anche  
 [Creare stringhe di connessione dati - Generatore report e SSRS](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)   
 [Specificare le credenziali e le informazioni sulla connessione per le origini dati del report](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md)   
 [Guida sensibile al contesto di Progettazione report](../../reporting-services/tools/report-designer-f1-help.md)  
  
  
