---
title: Finestra di dialogo Accesso a Reporting Services (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.reportservicelogin.f1
ms.assetid: 2037d797-0b61-44c7-931f-6c689c3fc733
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 7f4753ba89da99753463a852ae38456e56cec3b3
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2019
ms.locfileid: "59960747"
---
# <a name="reporting-services-login-dialog-box-ssrs"></a>Finestra di dialogo Accesso a Reporting Services (SSRS)
  Utilizzare la finestra di dialogo **Accesso a Reporting Services** per specificare le credenziali per la pubblicazione di report nel server di report.  
  
-   **Nota** se questa è la prima volta che si pubblica un report in un server di report dopo è impostare la proprietà di distribuzione **TargetServerURL** per un progetto, verificare che il nome del server specificato sia simile a `http://localhost/reportserver`e non `http://localhost/reports`. Se si specifica la directory `reports` nel server locale anziché la directory `reportserver` , verrà visualizzata questa finestra di dialogo. Per altre informazioni sull'impostazione **TargetServerURL**, vedere [Impostare le proprietà di distribuzione &#40;Reporting Services&#41;](set-deployment-properties-reporting-services.md).  
  
## <a name="options"></a>Opzioni  
 **Server**  
 Indica il nome del server di report. Ad esempio, `http://localhost/reportserver`. Per i server di report che utilizzano una porta diversa da quella predefinita, ovvero 80, includere il numero di porta. Ad esempio `http://localhost:81/reportserver`.  
  
 **Nome utente**  
 Consente di digitare il nome utente da utilizzare per l'accesso al servizio Web.  
  
 **Password**  
 Consente di digitare la password da utilizzare per l'accesso al servizio Web.  
  
## <a name="see-also"></a>Vedere anche  
 [Connessioni dati, origini dati e stringhe di connessione in Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)   
 [Specificare le credenziali e informazioni di connessione per origini dati del Report](../report-data/specify-credential-and-connection-information-for-report-data-sources.md) [Guida F1 della finestra di progettazione Report](report-designer-f1-help.md)  
  
  
