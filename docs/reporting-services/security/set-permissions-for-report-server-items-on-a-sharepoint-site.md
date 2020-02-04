---
title: Impostare autorizzazioni per gli elementi del server di report in un sito di SharePoint | Microsoft Docs
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- permissions [Reporting Services], SharePoint integrated mode
- SharePoint integration [Reporting Services], permissions
ms.assetid: 2467c657-a3bf-4ec3-a88c-8877df19823d
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 8bdd50291a009189bf894300cdea4633fdd952f0
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "65570607"
---
# <a name="set-permissions-for-report-server-items-on-a-sharepoint-site"></a>Impostare autorizzazioni per gli elementi del server di report in un sito di SharePoint
  Se le impostazioni di sicurezza predefinite non garantiscono il livello di accesso desiderato, sarà possibile creare nuovi livelli di autorizzazione per fornire l'accesso a operazioni o elementi specifici del server di report. Le impostazioni di sicurezza personalizzate possono risultare utili se si desidera limitare l'accesso a un particolare report.  
  
 Per creare gruppi e livelli di autorizzazione, è necessario essere proprietari del sito. I livelli di autorizzazione vengono utilizzati a livello globale nell'intero sito. Se si crea un nuovo livello di autorizzazione, questo sarà disponibile ad altri proprietari del sito.  
  
 La maggior parte delle autorizzazioni viene ereditata da un sito padre. Se si assegnano autorizzazioni per una raccolta o un elemento specifico, si disattiva l'ereditarietà delle autorizzazioni e sarà necessario eseguire operazioni aggiuntive per la gestione delle autorizzazioni relative al ramo specifico della gerarchia di siti.  
  
 Le autorizzazioni possono essere impostate per i file di definizione dei report (con estensione rdl), dei modelli (con estensione smdl) e delle origini dati condivise (con estensione rsds). Non è possibile utilizzare una combinazione di autorizzazioni ereditate e gestite per lo stesso elemento. Se si sceglie di gestire le autorizzazioni direttamente, le autorizzazioni ereditate non avranno effetto sull'elemento corrente. Se in seguito si desidera riattivare l'ereditarietà delle autorizzazioni, è possibile selezionare **Eredita autorizzazioni** dal menu **Azioni** .  
  
 Per impostare autorizzazioni per entità e prospettive in un modello, è necessario disporre del livello di autorizzazione Controllo completo per il modello. Controllo completo include "Gestione autorizzazioni", ovvero l'autorizzazione a livello di sito concessa ai proprietari e ai gruppi di SharePoint che dispongono dell'autorizzazione Controllo completo. Se si desidera offrire a utenti specifici la possibilità di impostare la sicurezza per gli elementi del modello, sarà necessario disattivare l'ereditarietà delle autorizzazioni e concedere autorizzazioni elevate (ad esempio Controllo completo) all'utente o al gruppo per il file del modello. Quando si concede il livello di autorizzazione Controllo completo per un elemento, ad esempio un file nella raccolta, l'ambito delle autorizzazioni sarà limitato a tale elemento e non si estenderà all'elemento padre o ad altri elementi nella stessa raccolta. Gli utenti che dispongono dell'autorizzazione Gestione autorizzazioni per il modello possono impostare la sicurezza degli elementi del modello tramite il sito di SharePoint o Progettazione modelli.  
  
### <a name="to-set-permissions-on-an-individual-report-model-or-data-source"></a>Per impostare le autorizzazioni per un singolo report, modello o origine dei dati  
  
1.  Se la raccolta non è aperta, fare clic sul nome della raccolta sulla barra di avvio veloce. Se il nome della raccolta non è visualizzato, fare clic su **Visualizza tutto il contenuto del sito**e quindi sul nome della raccolta desiderata.  
  
2.  Selezionare il file del report, del modello di report o dell'origine dati condivisa.  
  
3.  Fare clic sulla freccia verso il basso e scegliere **Gestisci autorizzazioni**dal menu.  
  
4.  Scegliere **Modifica autorizzazioni** dal menu **Azioni**, quindi fare clic su **OK** per confermare l'operazione.  
  
5.  Per assegnare autorizzazioni a un utente o a un gruppo che non dispone ancora di autorizzazioni per l'utilizzo del file, fare clic su **Nuovo**e quindi su **Aggiungi utenti**.  
  
6.  Per rimuovere o modificare le autorizzazioni per un utente o un gruppo esistente, selezionare la casella di controllo accanto al nome dell'utente o del gruppo, quindi scegliere **Rimuovi autorizzazioni utente**o **Modifica autorizzazioni utente** dal menu **Azioni**.  
  
### <a name="to-set-permissions-that-enable-model-item-security"></a>Per impostare le autorizzazioni che consentono la sicurezza degli elementi del modello  
  
1.  Accedere al sito di SharePoint utilizzando un account dotato di autorizzazione Gestione autorizzazioni per il sito.  
  
2.  Aprire la raccolta che contiene il modello.  
  
3.  Selezionare il modello.  
  
4.  Fare clic sulla freccia verso il basso accanto al modello, quindi selezionare **Gestisci autorizzazioni**.  
  
5.  Fare clic su **Azioni**.  
  
6.  Fare clic su **Modifica autorizzazioni**. Fare clic su **OK**.  
  
7.  Fare clic su **Nuovo**.  
  
8.  Fare clic su **Aggiungi utenti**.  
  
9. In Utenti/Gruppi immettere l'account utente.  
  
10. Selezionare **Assegna direttamente le autorizzazioni agli utenti**.  
  
11. Fare clic su **Controllo completo**.  
  
12. Fare clic su **OK**. Quando a un utente viene consentito di gestire le autorizzazioni per un modello specifico, questi può aprire il modello per modificarne le autorizzazioni.  
  
## <a name="see-also"></a>Vedere anche  
 [Utilizzare la sicurezza predefinita di Windows SharePoint Services per gli elementi del server di report](../../reporting-services/security/use-built-in-security-in-windows-sharepoint-services-for-report-server-items.md)   
 [Impostare le autorizzazioni per le operazioni del server di report in un'applicazione Web di SharePoint](../../reporting-services/security/set-permissions-for-report-server-operations-in-a-sharepoint-web-application.md)   
 [Confrontare ruoli e attività di Reporting Services con autorizzazioni e gruppi di SharePoint](../../reporting-services/security/reporting-services-roles-tasks-vs-sharepoint-groups-permissions.md)   
 [Informazioni di riferimento sulle autorizzazioni relative a elenchi e siti di SharePoint per gli elementi del server di report](../../reporting-services/security/sharepoint-site-and-list-permission-reference-for-report-server-items.md)   
 [Concessione di autorizzazioni per elementi del server di report in un sito di SharePoint](../../reporting-services/security/granting-permissions-on-report-server-items-on-a-sharepoint-site.md)  
  
  
