---
title: Proteggere le cartelle | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- high-security folders [Reporting Services]
- low-security folders
- folders [Reporting Services], security
- security [Reporting Services], folders
ms.assetid: 0fd91f77-0143-476b-9af0-87293be78e44
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 00bf03cedffd985726eb10e1c048132c415b241e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65570552"
---
# <a name="secure-folders"></a>Proteggere le cartelle
  La sicurezza di tutto il contenuto di un server di report si basa sulle impostazioni di sicurezza delle cartelle. Poiché che la sicurezza viene ereditata tramite la struttura di cartelle, è possibile consentire determinati tipi di accesso a sezioni diverse, grandi o piccole, della gerarchia di cartelle.  
  
 Le cartelle a elevata sicurezza possono essere utilizzate per l'archiviazione di report riservati o come aree di gestione temporanea. Si potrebbe ad esempio utilizzare una cartella per testare i report prima di inserirli nella loro posizione definitiva. Per controllare l'accesso a questa area, è possibile definire un'assegnazione di ruolo che consenta solo agli autori dei report di aggiungere ed eliminare elementi e una seconda assegnazione di ruolo che consenta a chi esegue il test di elaborare i report ma non di aggiungere o rimuovere elementi. Poiché le assegnazioni di ruolo vengono definite in modo esplicito per gli utenti che si occupano della progettazione e del test dei report, nessun altro utente, ad eccezione degli amministratori del sistema locale, potrà accedere alla cartella.  
  
 Le cartelle a bassa sicurezza possono essere utilizzate per l'archiviazione di report che si desidera siano facilmente accessibili.  
  
 La sicurezza delle cartelle rappresenta la base per la sicurezza a livello di elemento, a partire dal nodo radice della gerarchia di cartelle del server di report, ovvero la cartella Home. Poiché la sicurezza viene ereditata, per la cartella Home è consigliabile impostare criteri di sicurezza più restrittivo possibile. A tale scopo, assegnare il ruolo **Visualizzazione** nella cartella Home, che consente l'accesso di sola lettura.  
  
## <a name="tasks-and-folder-access"></a>Attività e accesso alle cartelle  
 Quando si creano assegnazioni di ruolo per le cartelle, è consigliabile valutare l'opportunità di selezionare le attività elencate nella tabella seguente.  
  
|Selezionare questa attività|Per concedere l'autorizzazione per|  
|----------------------|---------------------------|  
|Visualizzazione di cartelle|Visualizzare la gerarchia di cartelle e le proprietà di sola lettura che indicano quando la cartella è stata creata e modificata.<br /><br /> Gli elementi inclusi nella cartella possono essere visualizzati solo dagli utenti nelle cui assegnazioni di ruolo sono incluse anche le attività "Visualizzazione di report", "Visualizzazione di modelli", "Visualizzazione di risorse" e "Visualizzazione di origini dei dati".|  
|Gestione di cartelle|Visualizzare le proprietà di una cartella, modificare il nome o la descrizione o spostare la cartella in un'altra posizione. Questa attività consente agli utenti di creare cartelle.|  
|Gestione di report|Aggiungere report dal file system a una cartella e pubblicare i report da Progettazione report nel server di report.|  
|Gestione di origini dei dati|Aggiungere nuove origini dei dati condivise a una cartella e modificare quelle esistenti.|  
|Impostazione della sicurezza per singoli elementi|Creare e modificare assegnazioni di ruolo che controllano l'accesso alla cartella. Questa attività deve essere utilizzata con l'attività "Visualizzazione di cartelle" o "Gestione di cartelle". In caso contrario, non si avrà alcun effetto in quanto l'utente non sarà in grado di selezionare l'elemento.|  
  
## <a name="see-also"></a>Vedere anche  
 [Garantire la sicurezza di report e risorse](../../reporting-services/security/secure-reports-and-resources.md)   
 [Proteggere le origini dei dati condivise](../../reporting-services/security/secure-shared-data-source-items.md)   
 [Concessione di autorizzazioni in un server di report in modalità nativa](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)  
  
  
