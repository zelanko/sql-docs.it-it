---
title: Proteggere gli elementi del set di dati condiviso | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: security
ms.topic: conceptual
ms.assetid: 08e6d8b5-d88c-4ed2-9c05-55c757e00014
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: a51e261d06933a30bf1c59adffa6963c9826f360
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "65570677"
---
# <a name="secure-shared-dataset-items"></a>Proteggere gli elementi del set di dati condiviso
  In un server di report gli elementi del set di dati condiviso possono essere utilizzati da più report. È possibile proteggere set di dati condivisi per controllare il livello di accesso degli utenti. Per impostazione predefinita, solo i membri del gruppo **Administrators** predefinito possono visualizzare set di dati condivisi, modificare proprietà, abilitare la memorizzazione nella cache, creare piani di aggiornamento della cache ed eliminare elementi, mentre per tutti gli altri utenti è necessario creare assegnazioni di ruolo che consentano l'accesso a un set di dati condiviso.  
  
 Per impostare la sicurezza, è necessario creare un'assegnazione di ruolo che specifichi l'account utente o di gruppo autorizzato ad accedere al set di dati condiviso.  
  
## <a name="role-based-access-to-shared-datasets"></a>Accesso basato sui ruoli a set di dati condivisi  
 Per concedere l'accesso a set di dati condivisi, è possibile consentire agli utenti di ereditare le assegnazioni di ruolo esistenti da una cartella padre oppure creare una nuova assegnazione di ruolo nell'elemento stesso.  
  
 Le assegnazioni di ruolo predefinite che consentono di aggiungere, eliminare, modificare proprietà dell'elemento e visualizzare report correlati e origini dati condivise per i set di dati condivisi sono Gestione contenuto, Report personali e Server di pubblicazione. Per modificare una definizione del set di dati condiviso, utilizzare l'assegnazione di ruolo predefinita Generatore report o Gestione contenuto.  
  
 Poiché le assegnazioni di ruolo sono ereditate in genere da un nodo padre, una cartella per cui l'attività **Visualizzazione di report** è abilitata passa tale autorizzazione ai set di dati condivisi e ai report che contiene.  
  
 Per garantire un controllo maggiore sui set di dati condivisi e sui relativi risultati della query, configurare la sicurezza a livello di elemento sull'elemento del set di dati condiviso o salvare i set di dati condivisi in una cartella e configurare in quest'ultima la sicurezza a livello di elemento.  
  
## <a name="shared-dataset-parameters"></a>Parametri dei set di dati condivisi  
 I parametri dei set di dati condivisi non possono essere utilizzati per limitare i dati per utenti specifici. Lo scopo di tali parametri è infatti quello di fornire una modalità per specificare i dati da includere nel momento in cui il set di dati condiviso viene elaborato. Nel server di report non è possibile proteggere i valori per un parametro del set di dati condiviso.  
  
 Nella definizione del set di dati condiviso è possibile contrassegnare i parametri come valori di sola lettura e specificare valori predefiniti. L'override dei parametri contrassegnati come valori di sola lettura non può essere eseguito nel server. In un piano di aggiornamento della cache per un set di dati condiviso, ad esempio, non è possibile specificare valori per i parametri di sola lettura. Se nei parametri del set di dati condiviso sono incluse espressioni che si riferiscono alla raccolta globale dell'utente o sono presenti altre dipendenze dell'utente, non è possibile creare un piano di aggiornamento della cache per il set di dati stesso.  
  
## <a name="tasks-access-to-items-and-default-roles"></a>Attività, accesso agli elementi e ruoli predefiniti  
 I set di dati condivisi seguono lo stesso modello di sicurezza dei report. Per assegnare a un utente l'autorizzazione per azioni specifiche, scegliere un ruolo che includa l'attività corrispondente in cui sono presenti tali autorizzazioni. Nella tabella seguente vengono elencate le attività e le relative azioni incluse.  
  
|Selezionare questa attività|Per concedere agli utenti l'autorizzazione per|Ruoli predefiniti che includono l'attività|  
|----------------------|---------------------------------|-----------------------------------------|  
|Visualizzazione di report|Visualizzare l'elemento del set di dati condiviso nella gerarchia di cartelle. Se questa attività non è selezionata, l'elemento non è visibile agli utenti che potrebbero non essere consapevoli della disponibilità del set di dati.|Browser<br /><br /> Gestione contenuto<br /><br /> Generatore report<br /><br /> Report personali|  
|Gestione di report|Visualizzare le proprietà che specificano il nome, la descrizione e le informazioni di connessione. Questa attività viene inoltre utilizzata per visualizzare un elemento del set di dati condiviso nella gerarchia di cartelle. Se si seleziona questa attività, è possibile omettere l'attività Visualizzazione di report.|Gestione contenuto<br /><br /> Editore<br /><br /> Report personali|  
|Utilizzo di report|Visualizzare la definizione del set di dati condiviso.|Gestione contenuto<br /><br /> Generatore report|  
|Impostazione della sicurezza per singoli elementi|Creare e modificare assegnazioni di ruolo che controllano l'accesso al set di dati condiviso. Questa attività deve essere utilizzata con l'attività Visualizzazione di report o Gestione di report. In caso contrario non avrà alcun effetto, poiché l'utente non potrà selezionare l'elemento.|Gestione contenuto|  
  
 Per altre informazioni, vedere [Attività a livello di elemento](../../reporting-services/security/tasks-and-permissions-item-level-tasks.md) e [Predefined Roles](../../reporting-services/security/role-definitions-predefined-roles.md)(Ruoli predefiniti).  
  
## <a name="see-also"></a>Vedere anche  
 [Gestire set di dati condivisi](../../reporting-services/report-data/manage-shared-datasets.md)   
 [Proteggere le cartelle](../../reporting-services/security/secure-folders.md)   
 [Garantire la sicurezza di report e risorse](../../reporting-services/security/secure-reports-and-resources.md)   
 [Concessione di autorizzazioni in un server di report in modalità nativa](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)   
 [Concessione di autorizzazioni in un server di report in modalità nativa](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)  
  
  
