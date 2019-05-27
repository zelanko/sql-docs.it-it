---
title: Configurare Gestione Report per il passaggio di cookie di autenticazione personalizzati | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- authentication [Reporting Services]
- extensions [Reporting Services], custom security
ms.assetid: 91aeb053-149e-4562-ae4c-a688d0e1b2ba
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 34f637ee2d0a8235f21167df78178c4de9292c8c
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66102050"
---
# <a name="configure-report-manager-to-pass-custom-authentication-cookies"></a>Configurare Gestione report per il passaggio di cookie di autenticazione personalizzati
  Se si sta utilizzando un'estensione di autenticazione personalizzata, è necessario configurare Gestione report per la trasmissione di cookie di autenticazione personalizzati. In caso contrario, i cookie verranno trasmessi solo mediante richieste HTTP specifiche del server di report. Se si desidera trasmettere ulteriori cookie, è necessario modificare il file RSReportServer.Config.  
  
## <a name="modifying-the-rsreportserverconfig-file"></a>Modifica del file RSReportServer.config  
 È possibile abilitare gestione Report di trasmettere ulteriori cookie al server di report mediante l'aggiunta di un <`PassThroughCookies`> elemento per le impostazioni di configurazione di gestione Report nel file RSReportServer. config. La trasmissione di cookie aggiuntivi è utile in una soluzione di autenticazione Single Sign-On che, insieme ai cookie di autenticazione del server di report, richiede anche cookie di un sistema di autenticazione di terze parti.  
  
 Per consentire la trasmissione di ulteriori cookie tramite richieste HTTP quando si utilizza Gestione report, impostare gli elementi seguenti nel file RSReportServer.config:  
  
```  
<UI>  
   <CustomAuthenticationUI>  
      ...  
      <PassThroughCookies>  
         <PassThroughCookie>cookiename1</PassThroughCookie>  
         <PassThroughCookie>cookiename2</PassThroughCookie>  
      </PassThroughCookies>  
   </CustomAuthenticationUI>  
      ...  
</UI>  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Autenticazione con il server di report](authentication-with-the-report-server.md)   
 [File di configurazione RSReportServer](../report-server/rsreportserver-config-configuration-file.md)   
 [Panoramica sulle estensioni di sicurezza](../extensions/security-extension/security-extensions-overview.md)   
 [Configurare e amministrare un server di report &#40;modalità nativa SSRS&#41;](../report-server/configure-and-administer-a-report-server-ssrs-native-mode.md)  
  
  
