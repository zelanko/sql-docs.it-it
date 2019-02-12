---
title: Riferimento della libreria del provider WMI Reporting Services (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
api_name:
- Reporting Services WMI Provider Library
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- WMI provider [Reporting Services], library
ms.assetid: 17ba711d-7eff-4423-9168-63dc425a3428
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 302e7f1b58fdb2a63af9f2a1b4e9dad3127c6d57
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56034512"
---
# <a name="reporting-services-wmi-provider-library-reference-ssrs"></a>Riferimento della libreria del provider WMI Reporting Services (SSRS)
  Il provider WMI (Windows Management Instrumentation) di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] supporta operazioni WMI che consentono di scrivere script e codice per modificare le impostazioni del server di report e di Gestione report.  
  
 Ad esempio, se si vuole modificare l'impostazione relativa all'uso della sicurezza integrata quando il server di report si connette al database del server di report, creare un'istanza della classe MSReportServer_ConfigurationSetting e usare la proprietà DatabaseIntegratedSecurity dell'istanza del server di report. Le classi mostrate nella tabella seguente rappresentano i componenti di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Le classi sono definite negli spazi dei nomi [!INCLUDE[ssRSWMInmspc](../../includes/ssrswminmspc-md.md)] o [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)] . Ognuna delle classi supporta operazioni di lettura e scrittura. Le operazioni di creazione non sono supportate.  
  
## <a name="classes"></a>Classi  
 [Classe MSReportServer_Instance](msreportserver-instance-class.md)  
 Fornisce le informazioni di base necessarie affinché un client si connetta a un server di report installato.  
  
 [Classe MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-class.md)  
 Rappresenta i parametri di installazione e di runtime di un'istanza del server di report. Tali parametri sono archiviati nel file di configurazione per il server di report.  
  
 Per altre informazioni sulle operazioni WMI, vedere la documentazione di WMI SDK inclusa in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK.  
  
## <a name="see-also"></a>Vedere anche  
 [Accedere al provider WMI per Reporting Services](../tools/access-the-reporting-services-wmi-provider.md)   
 [Guida di riferimento tecnico &#40;SSRS&#41;](../technical-reference-ssrs.md)  
  
  
