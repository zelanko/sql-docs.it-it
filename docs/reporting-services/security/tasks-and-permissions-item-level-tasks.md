---
title: Attività a livello di elemento | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- item-level tasks [Reporting Services]
ms.assetid: fdeb7bc3-167a-4342-84e3-32e3faa1fa39
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 7224b99b721a48f14467da7479137fb4c61d4da9
ms.sourcegitcommit: dda9a1a7682ade466b8d4f0ca56f3a9ecc1ef44e
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 05/14/2019
ms.locfileid: "65570274"
---
# <a name="tasks-and-permissions---item-level-tasks"></a>Attività e autorizzazioni - Attività a livello di elemento
  Un'attività a livello di elemento è una raccolta di autorizzazioni correlate a un report, una cartella, un modello di report, una risorsa o un'origine dati condivisa. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] include anche attività a livello di sistema applicabili all'intero sito del server di report. Per altre informazioni, vedere [Attività a livello di sistema](../../reporting-services/security/tasks-and-permissions-system-level-tasks.md). Per ulteriori informazioni sulle attività e le autorizzazioni in generale, vedere [Tasks and Permissions](../../reporting-services/security/tasks-and-permissions.md).  
  
> [!NOTE]  
>  Se si gestiscono queste attività a livello di programmazione, è necessario utilizzare metodi che supportano attività a livello di elemento. Per altre informazioni, vedere <xref:ReportService2010.ReportingService2010.ListTasks%2A> e <xref:ReportService2010.ReportingService2010.ListRoles%2A>.  
  
## <a name="permissions-in-item-level-tasks"></a>Autorizzazioni delle attività a livello di elemento  
 Nella tabella seguente vengono elencate le attività a livello di elemento e le relative autorizzazioni e gli elementi ai quali si applicano tali autorizzazioni. L'elenco delle autorizzazioni è puramente informativo e ha lo scopo di offrire una descrizione più precisa delle funzionalità disponibili tramite ogni attività.  
  
 I set di dati condivisi utilizzano lo stesso set di autorizzazioni dei report. Le parti del report utilizzano lo stesso set di autorizzazioni delle risorse.  
  
|Attività|Applicabile all'elemento|Autorizzazioni|  
|----------|---------------------|-----------------|  
|Utilizzo di report|Report|Lettura di contenuto<br /><br /> Lettura delle definizioni dei report<br /><br /> Lettura di proprietà|  
|Utilizzo di report|Set di dati condivisi|Lettura di contenuto<br /><br /> Lettura delle definizioni dei report<br /><br /> Lettura di proprietà|  
|Creazione di report collegati|Report|Creazione di collegamenti<br /><br /> Lettura di proprietà|  
|Gestione di tutte le sottoscrizioni|Report|Lettura di proprietà<br /><br /> Lettura di qualsiasi sottoscrizione<br /><br /> Creazione di qualsiasi sottoscrizione<br /><br /> Eliminazione di qualsiasi sottoscrizione<br /><br /> Aggiornamento di qualsiasi sottoscrizione|  
|Gestione di origini dei dati|Cartelle|Creazione di origini dei dati|  
|Gestione di origini dei dati|Origini dati|Aggiornamento di proprietà<br /><br /> Eliminazione del contenuto di aggiornamento<br /><br /> Lettura di proprietà|  
|Gestione di cartelle|Cartelle|Creazione di cartelle<br /><br /> Eliminazione delle proprietà di aggiornamento<br /><br /> Lettura di proprietà|  
|Gestione di sottoscrizioni individuali|Report|Lettura di proprietà<br /><br /> Creazione di sottoscrizioni<br /><br /> Eliminazione di sottoscrizioni<br /><br /> Lettura di sottoscrizioni<br /><br /> Aggiornamento di sottoscrizioni|  
|Gestione di modelli|Cartelle|Creazione di un modello|  
|Gestione di modelli|Modelli|Lettura di proprietà<br /><br /> Lettura di contenuto<br /><br /> Eliminazione del contenuto di aggiornamento<br /><br /> Lettura di origini dei dati<br /><br /> Aggiornamento di origini dei dati<br /><br /> Lettura dei criteri di autorizzazione degli elementi del modello<br /><br /> Aggiornamento dei criteri di autorizzazione degli elementi del modello<br /><br /> Eliminazione delle proprietà di aggiornamento|  
|Gestione della cronologia dei report|Report|Lettura di proprietà<br /><br /> Creazione della cronologia dei report<br /><br /> Eliminazione della cronologia dei report<br /><br /> Esecuzione dei criteri di lettura<br /><br /> Aggiornamento di criteri<br /><br /> Visualizzazione della cronologia dei report|  
|Gestione di report|Cartelle|Creazione di report<br /><br /> applicabile anche alla creazione di set di dati condivisi|  
|Gestione di report|Report|Lettura di proprietà<br /><br /> Eliminazione delle proprietà di aggiornamento<br /><br /> Aggiornamento di parametri<br /><br /> Lettura di origini dei dati<br /><br /> Aggiornamento di origini dei dati<br /><br /> Lettura delle definizioni dei report<br /><br /> Aggiornamento delle definizioni dei report<br /><br /> Esecuzione dei criteri di lettura<br /><br /> Aggiornamento di criteri|  
|Gestione di report|Set di dati condivisi|Lettura di proprietà<br /><br /> Eliminazione delle proprietà di aggiornamento<br /><br /> Aggiornamento di parametri<br /><br /> Lettura di origini dei dati<br /><br /> Aggiornamento di origini dei dati<br /><br /> Lettura delle definizioni dei report<br /><br /> Aggiornamento delle definizioni dei report<br /><br /> Esecuzione dei criteri di lettura<br /><br /> Aggiornamento di criteri|  
|Gestione di risorse|Cartelle|Creazione di risorse|  
|Gestione di risorse|Risorse|Aggiornamento di proprietà<br /><br /> Eliminazione del contenuto di aggiornamento<br /><br /> Lettura di proprietà|  
|Gestione di risorse|Parti del report|Aggiornamento di proprietà<br /><br /> Eliminazione del contenuto di aggiornamento<br /><br /> Lettura di proprietà|  
|Impostazione della sicurezza per singoli elementi|Report, risorse, origini dei dati, set di dati condivisi, cartelle|Lettura di criteri di sicurezza - Aggiornamento di criteri di sicurezza|  
|Visualizzazione di origini dei dati|Origini dei dati|Lettura di contenuto<br /><br /> Lettura di proprietà|  
|Visualizzazione di cartelle|Cartelle|Lettura di proprietà<br /><br /> Esecuzione e visualizzazione<br /><br /> Visualizzazione della cronologia dei report|  
|Visualizzazione di modelli|Modelli di report|Lettura di proprietà<br /><br /> Lettura di contenuto<br /><br /> Lettura di origini dei dati|  
|Visualizzazione di report|Report|Lettura di contenuto<br /><br /> Lettura di proprietà|  
|Visualizzazione di report|Set di dati condivisi|Lettura di contenuto<br /><br /> Lettura di proprietà|  
|Visualizzazione di risorse|Risorse|Lettura di contenuto<br /><br /> Lettura di proprietà|  
|Visualizzazione di risorse|Parti del report|Lettura di contenuto<br /><br /> Lettura di proprietà|  
  
## <a name="see-also"></a>Vedere anche  
 [Concessione di autorizzazioni in un server di report in modalità nativa](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)  
  
  
