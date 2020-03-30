---
title: Abilitare e disabilitare la funzionalità Report personali | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
helpviewer_keywords:
- deactivated My Reports folder
- folders [Reporting Services], My Reports
- activated My Reports folder
- My Reports folder [Reporting Services]
- disabling My Reports folder
ms.assetid: 16c76e82-9fd4-417c-9ed3-a7d5bcd1dba2
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 6670d1da918ac1bdc6cb1947b265f9d543259814
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "65577772"
---
# <a name="enable-and-disable-my-reports"></a>Abilitare e disabilitare la funzionalità Report personali
  La caratteristica Report personali consente di assegnare spazio di archiviazione personale nel database del server di report. Gli utenti possono servirsi di tale spazio di archiviazione per salvare i propri report in una cartella privata. L'amministratore del server di report può attivare o disabilitare questa caratteristica oppure modificarne il funzionamento cambiando le impostazioni di sicurezza che determinano i vari tipi di operazioni che gli utenti possono eseguire in questa area di lavoro.  
  
 La caratteristica Report personali è disabilitata per impostazione predefinita. È possibile abilitarla o disabilitarla per tutti gli utenti, ma non solo per alcuni. Questa caratteristica può rivelarsi utile per la maggior parte degli utenti e delle organizzazioni. Tuttavia, per verificare se è adatta alla propria organizzazione, è consigliabile analizzarne i vantaggi e gli svantaggi illustrati più avanti in questo argomento.  
  
## <a name="how-to-enable-and-disable-my-reports"></a>Come abilitare e disabilitare la funzionalità Report personali  
 Per abilitare Report personali tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], connettersi all'istanza del server di report e aprire la pagina **Proprietà server** . Quindi, nella scheda **Generale** selezionare l'opzione **Abilita una cartella Report personali per ogni utente** .  
  
 La definizione di ruolo utilizzata per la funzionalità Report personali determina le azioni supportate nell'area di lavoro Report personali. Ad esempio, se per il ruolo Report personali non viene selezionata l'attività "Creazione di report collegati", gli utenti appartenenti a questo ruolo non potranno creare report collegati nelle cartelle Report personali. Per altre informazioni, vedere [Proteggere i report personali](../../reporting-services/security/secure-my-reports.md).  
  
 Per disattivare Report personali, deselezionare **Abilita una cartella Report personali per ogni utente**. Se si disattiva la funzionalità Report personali, per gli utenti non verrà più visualizzato alcun riferimento alla cartella Report personali. Le cartelle in cui sono effettivamente archiviati i dati, ovvero le sottocartelle di Cartelle utenti, devono essere eliminate manualmente dopo la disabilitazione della caratteristica.  
  
### <a name="when-my-reports-is-activated"></a>Quando la funzionalità Report personali è attivata  
 Quando questa caratteristica è attivata, per gli utenti viene visualizzata la cartella Report personali al di sotto della cartella radice Home. Oltre alla cartella Report personali, per gli amministratori del server di report verrà visualizzata la cartella Cartelle utenti contenente una sottocartella per ogni utente.  
  
 Quando questa caratteristica è attivata, non è possibile eliminare Cartelle utenti e le relative sottocartelle. Inoltre, "Report personali" diventa un nome riservato per le cartelle create sotto il nodo radice (Home).  
  
 Se si attiva la funzionalità Report personali dopo averla disattivata, verrà creata automaticamente una nuova cartella Cartelle utenti se tale cartella non esiste già. Se tale cartella esiste, verrà creata automaticamente una nuova sottocartella per ogni utente che accederà alla cartella Report personali.  
  
### <a name="when-my-reports-is-deactivated"></a>Quando la funzionalità Report personali è disattivata  
 Quando questa caratteristica è disattivata, il nome "Report personali" non è più riservato, pertanto gli utenti possono creare una cartella personale denominata Report personali nella cartella Home. Inoltre, non viene più eseguito il reindirizzamento da Report personali alle sottocartelle Report personali specifiche dell'utente. Infine, non funzioneranno più tutti i collegamenti che includono una cartella Report personali specifica dell'utente nell'indirizzo URL.  
  
## <a name="choosing-to-use-my-reports"></a>Vantaggi e svantaggi della funzionalità Report personali  
 Prima di decidere se utilizzare o meno la funzionalità Report personali, è necessario stabilire se dedicare risorse del server all'area di lavoro degli utenti. Report personali è una potente caratteristica che consente agli utenti di disporre di informazioni che permettono loro di eseguire le attività lavorative in modo più semplice. Consente inoltre di gestire report che non sono stati creati per un utilizzo generico. Uno dei motivi più importanti per utilizzare la funzionalità Report personali è rappresentato dal fatto che offre caratteristiche di sicurezza e semplicità di gestione agli utenti che progettano e modificano i report. Senza questa caratteristica, potrebbe essere necessario creare cartelle e criteri di sicurezza per diversi utenti in base alle necessità specifiche. Se cambiano gli utenti e le loro esigenze, la quantità di cartelle e di criteri di sicurezza aumenta di conseguenza e ciò può determinare difficoltà di gestione.  
  
 Si noti che, se si attiva la funzionalità Report personali, viene creata automaticamente una cartella Report personali per ogni utente con account di dominio che fa clic sul collegamento Report personali, anche se tale utente non desidera o non necessita di una cartella Report personali. Non esiste una soluzione per determinare quali cartelle sono in uso. È necessario controllare le cartelle manualmente per verificare se contengono dati.  
  
## <a name="see-also"></a>Vedere anche  
 [Protezione dei report](../../reporting-services/security/secure-my-reports.md)   
 [Gestione contenuto del server di report &#40;modalità nativa SSRS&#41;](../../reporting-services/report-server/report-server-content-management-ssrs-native-mode.md)  
  
  
