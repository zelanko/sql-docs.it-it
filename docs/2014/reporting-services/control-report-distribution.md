---
title: Controllare la distribuzione dei Report | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- subscriptions [Reporting Services], report distribution
- subscriptions [Reporting Services], e-mail
- subscriptions [Reporting Services], file share delivery
- file share delivery [Reporting Services]
- e-mail [Reporting Services]
- subscriptions [Reporting Services], security
- mail [Reporting Services]
ms.assetid: 8f15e2c6-a647-4b05-a519-1743b5d8654c
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: de8a27801ef89f10bf303cee17d1c2d0e1081c5a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66109694"
---
# <a name="control-report-distribution"></a>Controllare la distribuzione dei report
  È possibile configurare un server di report in modo da ridurre i rischi di sicurezza associati alla distribuzione tramite posta elettronica e condivisione file.  
  
## <a name="securing-reports"></a>sicurezza di report  
 Per controllare la distribuzione dei report, è innanzitutto necessario proteggerli dall'accesso non autorizzato. Per poter essere utilizzato in una sottoscrizione, un report deve utilizzare un set di credenziali archiviate che rimangano invariate per i singoli recapiti. Gli utenti che possono accedere al report nel server di report possono eseguirlo ed eventualmente distribuirlo. Per evitare che ciò accada, è necessario limitare l'accesso ai report solo agli utenti per i quali è strettamente necessario. Per altre informazioni, vedere [proteggere i report e le risorse](security/secure-reports-and-resources.md) e [proteggere le cartelle](security/secure-folders.md).  
  
 I report con contenuto strettamente riservato che utilizzano la sicurezza dei database per autorizzare gli accessi non possono essere distribuiti tramite sottoscrizioni.  
  
> [!IMPORTANT]  
>  I report vengono trasportati come file. I rischi e le precauzioni per i file equivalgono a quelli per i report che vengono salvati su disco o inviati come allegati. Un utente che accede a un file può distribuirlo o utilizzarlo a propria discrezione.  
  
## <a name="controlling-e-mail-delivery"></a>Controllo del recapito tramite posta elettronica  
 È possibile configurare un server di report in modo che la distribuzione tramite posta elettronica sia circoscritta a domini host specifici. È possibile, ad esempio, fare in modo che un server di report recapiti un report solo ai domini indicati nel file di configurazione RSReportServer.  
  
 È inoltre possibile definire le impostazioni di configurazione in modo che il campo **A** di una sottoscrizione venga nascosto. In questo caso, i report verranno recapitati solo all'utente che definisce la sottoscrizione. Non è tuttavia possibile impedire a un utente che ha ricevuto un report di inoltrarlo.  
  
 Il modo più efficace per controllare la distribuzione dei report consiste nel configurare un server di report in modo che invii unicamente un URL del server di report. Il server di report utilizza l'autenticazione di Windows e un modello di autorizzazione basata sui ruoli per controllare l'accesso a un report. Se un utente riceve per errore tramite posta elettronica un report che non è autorizzato a visualizzare, il server di report non visualizzerà il report.  
  
## <a name="controlling-file-share-delivery"></a>Controllo del recapito tramite condivisione file  
 Il recapito tramite condivisione file viene utilizzato per inviare un report a un file presente su un disco rigido. Dopo essere stato salvato su disco, un file non è più soggetto al modello di sicurezza basata sui ruoli utilizzato dal server di report per controllare gli accessi degli utenti. Per proteggere un report recapitato a un disco rigido, è possibile associare elenchi di controllo di accesso (ACL) al file stesso o alla cartella che lo contiene. In base al sistema operativo, potrebbero essere disponibili ulteriori opzioni di sicurezza.  
  
## <a name="see-also"></a>Vedere anche  
 [Configurare un Server di Report per il recapito tramite posta elettronica &#40;Gestione configurazione SSRS&#41;](../../2014/sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md)   
 [Sottoscrizioni e recapito &#40;Reporting Services&#41;](subscriptions/subscriptions-and-delivery-reporting-services.md)   
 [Creare e gestire sottoscrizioni per server di report in modalità nativa](../../2014/reporting-services/create-manage-subscriptions-native-mode-report-servers.md)  
  
  
