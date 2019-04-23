---
title: Ruoli e autorizzazioni (Reporting Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- access controls [Reporting Services]
- permissions [Reporting Services], about permissions
- security [Reporting Services], identity and access control
- authentication [Reporting Services]
- permissions [Reporting Services]
- security [Reporting Services], role-based
- identity [Reporting Services]
ms.assetid: eea655fe-43ed-418d-8233-b288a8f4daa4
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 27baf79d25201f99f70760ef8673c4135f82f68e
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2019
ms.locfileid: "59959317"
---
# <a name="roles-and-permissions-reporting-services"></a>Ruoli e autorizzazioni (Reporting Services)
  In Reporting Services sono disponibili un sottosistema di autenticazione e un modello di autorizzazione basata sui ruoli. I modelli di autenticazione e autorizzazione variano a seconda che il server di report sia in esecuzione in modalità nativa o in modalità SharePoint. Se il server di report fa parte di una distribuzione di SharePoint, con le autorizzazioni di SharePoint è possibile determinare gli utenti che possono accedere al server di report.  
  
## <a name="identity-and-access-control-for-native-mode"></a>Controllo di identità e accesso per la modalità nativa  
 L'autenticazione predefinita è basata sull'autenticazione di Windows e sulla sicurezza integrata. È possibile modificare le impostazioni di autenticazione per consentire al server di report di rispondere a richieste di autenticazione diverse o anche sostituire le funzionalità di sicurezza predefinite con un'estensione di autenticazione personalizzata fornita dall'utente.  
  
 L'autorizzazione è basata su ruoli che vengono assegnati a un'entità. Ogni ruolo è costituito da un set di attività correlate, a loro volta composte da operazioni correlate. Ad esempio, l'attività **Gestione di report** concede l'accesso alle operazioni seguenti sul server di report: visualizzazione, aggiunta, aggiornamento, eliminazione e pianificazione di report, nonché aggiornamento delle relative proprietà.  
  
## <a name="identity-and-access-control-for-sharepoint-mode"></a>Controllo di identità e accesso per la modalità SharePoint  
 In modalità integrata SharePoint l'autenticazione e l'autorizzazione vengono gestite sul sito di SharePoint, prima che le richieste raggiungano il server di report. A seconda della modalità di configurazione dell'autenticazione, le richieste provenienti da un sito di SharePoint includono un token di sicurezza o un nome utente attendibile. Le autorizzazione impostate per gli utenti e i gruppi di SharePoint autorizzano l'accesso agli elementi del server di report inseriti nelle raccolte di SharePoint.  
  
## <a name="in-this-section"></a>In questa sezione  
 [Concessione di autorizzazioni in un server di report in modalità nativa](granting-permissions-on-a-native-mode-report-server.md)  
 Viene descritto il modello di autorizzazione basata sui ruoli che fornisce l'accesso al contenuto e alle operazioni.  
  
 [Concessione di autorizzazioni per elementi del server di report in un sito di SharePoint](granting-permissions-on-report-server-items-on-a-sharepoint-site.md)  
 Viene illustrato l'utilizzo di gruppi, livelli di autorizzazione e autorizzazioni di SharePoint per il controllo dell'accesso a un server di report.  
  
## <a name="see-also"></a>Vedere anche  
 [Autenticazione con il server di report](authentication-with-the-report-server.md)   
 [Concessione di autorizzazioni in un server di report in modalità nativa](granting-permissions-on-a-native-mode-report-server.md)  
  
  
