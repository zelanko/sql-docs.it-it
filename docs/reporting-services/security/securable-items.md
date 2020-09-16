---
description: Elementi a sicurezza diretta
title: Elementi a sicurezza diretta | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- securable items [Reporting Services]
- roles [Reporting Services], securable items
- security [Reporting Services], securable items listed
- role-based security [Reporting Services], securable items
ms.assetid: 27f58d4c-5c7b-4947-af5b-0f1fa60faf5f
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 9fd4b92dcacf94e2a0196f210050954a84c1ac3d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88498014"
---
# <a name="securable-items"></a>Elementi a sicurezza diretta
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] usa la sicurezza basata sui ruoli per controllare l'accesso agli elementi archiviati in un server di report. Quando si concede a un utente l'accesso a un server di report, in genere si creano due assegnazioni di ruolo:  
  
-   Al livello di sito  
  
-   Nella cartella Home, ovvero il nodo radice della gerarchia di cartelle del server di report  
  
 La sicurezza viene ereditata all'interno della gerarchia di cartelle del server di report. Con la creazione di assegnazioni di ruolo al livello di sito e nella cartella Home, viene impostata un'ereditarietà delle autorizzazioni che si estende a tutti gli elementi e le operazioni di un server di report.  
  
 Per i singoli elementi, è possibile definire impostazioni di sicurezza specifiche che avranno la priorità sull'ereditarietà delle autorizzazioni. Gli elementi che è possibile proteggere singolarmente includono:  
  
-   Cartelle  
  
-   Report  
  
-   Modelli di report  
  
-   Risorse  
  
-   Origini dati condivise  
  
-   Set di dati condivisi  
  
 Altri costrutti, ad esempio pianificazioni e sottoscrizioni, non sono protetti in modo esplicito. Le pianificazioni e le sottoscrizioni operano nel contesto di sicurezza di un report.  
  
## <a name="item-descriptions"></a>Descrizioni degli elementi  
 Nella tabella seguente vengono indicati gli elementi a sicurezza diretta e le relative caratteristiche.  
  
|Elemento|Caratteristiche|  
|----------|---------------------|  
|Cartelle|La sicurezza della cartella si applica alla cartella stessa e agli elementi che contiene. La cartella Home è il nodo radice della gerarchia di cartelle. Le impostazioni di sicurezza che vengono definite per questa cartella determinano le impostazioni di sicurezza iniziali per tutti i report, le cartelle, le risorse e le origini dei dati condivise che sono subordinati a questa cartella nella gerarchia di cartelle. Per altre informazioni, vedere [Proteggere le cartelle](../../reporting-services/security/secure-folders.md).<br /><br /> La cartella Report personali è una cartella per scopi specifici che viene protetta tramite un'assegnazione di ruolo implicita basata su un ruolo dedicato. Per altre informazioni, vedere [Proteggere i report personali](../../reporting-services/security/secure-my-reports.md).|  
|Report|È possibile proteggere i report e i report collegati per controllare il tipo di azioni eseguibili da un utente, ad esempio la modifica delle proprietà di un determinato report.<br /><br /> La cronologia del report viene protetta tramite il report corrispondente. Non è possibile definire impostazioni di sicurezza specifiche per singoli snapshot all'interno della cronologia del report.<br /><br /> Per altre informazioni sulla sicurezza dei report, vedere [Garantire la sicurezza di report e risorse](../../reporting-services/security/secure-reports-and-resources.md).|  
|Modelli di report|È possibile specificare l'assegnazione di ruolo per un intero modello di report o per una parte di esso. Poiché i modelli di report possono essere molto estesi, è consigliabile proteggere gli elementi del modello con mapping a dati riservati.|  
|Risorse|È possibile proteggere una risorsa per controllare l'accesso alla risorsa stessa e alle sue proprietà.<br /><br /> Solo le risorse autonome possono essere protette separatamente. Le risorse incorporate in un report non possono essere protette indipendentemente dal report.<br /><br /> Per altre informazioni sulla sicurezza delle risorse, vedere [Garantire la sicurezza di report e risorse](../../reporting-services/security/secure-reports-and-resources.md).|  
|Origini dati condivise|È possibile proteggere le origini dati condivise per limitare l'accesso all'elemento e alle relative pagine delle proprietà. Per altre informazioni, vedere [Proteggere le origini dei dati condivise](../../reporting-services/security/secure-shared-data-source-items.md).|  
|Set di dati condivisi|È possibile proteggere i set di dati condivisi per controllare il tipo di azioni eseguibili da un utente, ad esempio la visualizzazione o la modifica della definizione o la modifica delle proprietà di un set di dati condiviso specifico.<br /><br /> Per ulteriori informazioni, vedere [Proteggere gli elementi del set di dati condiviso](../../reporting-services/security/secure-shared-dataset-items.md).|  
  
## <a name="see-also"></a>Vedere anche  
 [Concessione di autorizzazioni in un server di report in modalità nativa](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)   
 [Creare, eliminare o modificare un ruolo &#40;Management Studio&#41;](../../reporting-services/security/role-definitions-create-delete-or-modify.md)   
 [Concedere l'accesso utente a un server di report &#40;Gestione report&#41;](../../reporting-services/security/grant-user-access-to-a-report-server-report-manager.md)   
 [Modificare o eliminare un'assegnazione di ruolo &#40;Gestione report&#41;](../../reporting-services/security/role-assignments-modify-or-delete.md)  
  
  
