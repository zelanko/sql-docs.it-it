---
description: Proteggere le origini dei dati condivise
title: Proteggere le origini dei dati condivise | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- shared data sources [Reporting Services]
- data sources [Reporting Services], shared
- security [Reporting Services], data sources
ms.assetid: 7299e498-0a1a-4821-a22a-5199bb773ce0
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: cf25b5dd7eac661f5ee77e2328a322601b0d3c8d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88472643"
---
# <a name="secure-shared-data-source-items"></a>Proteggere le origini dei dati condivise
  È possibile impostare la sicurezza per un'origine dei dati condivisa in modo da abilitarne o disabilitarne l'accesso.  
  
 Un utente con autorizzazioni di accesso minime a un'origine dei dati condivisa, ad esempio quelle concesse tramite il ruolo **Visualizzazione** , è in grado di visualizzare l'elenco dei report che usano tale elemento, a condizione che sia anche autorizzato a visualizzare tali report.  
  
 Un utente con autorizzazioni di accesso più estese, ad esempio quelle concesse tramite il ruolo **Gestione contenuto** , è in grado di visualizzare e impostare proprietà per l'origine dei dati condivisa.  
  
 Per impostare la sicurezza, è necessario creare un'assegnazione di ruolo che specifichi quale account utente o di gruppo è autorizzato ad accedere all'origine dei dati condivisa. Gli utenti autorizzati ad accedere a un'origine dei dati condivisa possono modificarne il nome, la descrizione, la stringa di connessione o le informazioni sulle credenziali.  
  
## <a name="tasks-and-access-to-items"></a>Attività e accesso agli elementi  
 Quando si creano assegnazioni di ruolo, per assegnare autorizzazioni appropriate a utenti e gruppi utilizzare un ruolo che contenga le attività seguenti.  
  
|Selezionare questa attività|Per concedere agli utenti l'autorizzazione per|  
|----------------------|---------------------------------|  
|Visualizzazione di origini dei dati|Visualizzare l'origine dei dati condivisa nella gerarchia di cartelle. Se questa attività non è selezionata, l'elemento non è visibile agli utenti che potrebbero non essere consapevoli che l'origine dei dati è disponibile.|  
|Gestire le origini dati|Visualizzare le proprietà che specificano il nome, la descrizione e le informazioni di connessione. Questa attività viene inoltre utilizzata per visualizzare un'origine dei dati condivisa nella gerarchia di cartelle. Se si seleziona questa attività, è possibile evitare di selezionare l'attività Visualizzazione di origini dei dati.|  
|Impostazione della sicurezza per singoli elementi|Creare e modificare assegnazioni di ruolo che controllano l'accesso all'origine dei dati condivisa. Questa attività deve essere utilizzata con l'attività Visualizzazione di origini dei dati o Gestione di origini dei dati. In caso contrario non avrà alcun effetto, poiché l'utente non potrà selezionare l'elemento.|  
  
## <a name="see-also"></a>Vedere anche  
 [Gestire origini dati dei report](../../reporting-services/report-data/manage-report-data-sources.md)   
 [Proteggere le cartelle](../../reporting-services/security/secure-folders.md)   
 [Garantire la sicurezza di report e risorse](../../reporting-services/security/secure-reports-and-resources.md)   
 [Concessione di autorizzazioni in un server di report in modalità nativa](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)   
 [Archiviare le credenziali in un'origine dati di Reporting Services](../../reporting-services/report-data/store-credentials-in-a-reporting-services-data-source.md)  
  
  
