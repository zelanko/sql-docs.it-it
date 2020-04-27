---
title: Pagina delle proprietà sicurezza, elementi (Gestione report) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 351b8503-354f-4b1b-a7ac-f1245d978da0
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 5ad98fe533caefa937d969754fa1278354e5c6e1
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66102158"
---
# <a name="security-properties-page-items-report-manager"></a>Pagina delle proprietà sicurezza, Elementi (Gestione report)
  Utilizzare la pagina delle proprietà sicurezza per visualizzare o modificare le impostazioni di sicurezza che regolano l'accesso a cartelle, report, modelli, risorse e origini dei dati condivise. Questa pagina è disponibile per gli elementi per i quali l'utente è autorizzato a definire le impostazioni di sicurezza.  
  
 Il livello di accesso agli elementi viene impostato tramite assegnazioni di ruolo che specificano le attività consentite per un gruppo o un utente. Le assegnazioni di ruolo sono costituite da un nome di utente o gruppo e da una o più definizioni di ruolo che specificano la raccolta di attività consentite.  
  
 Le sottocartelle e gli elementi in esse inclusi ereditano le impostazioni di sicurezza dalla cartella radice. A meno che non si interrompa in modo esplicito questo meccanismo, le sottocartelle e gli elementi ereditano il contesto di sicurezza di un elemento padre. Se si ridefiniscono i criteri di sicurezza per una cartella in un livello centrale della gerarchia, le nuove impostazioni di sicurezza verranno applicate a tutti gli elementi figlio, incluse le sottocartelle.  
  
## <a name="navigation"></a>Navigazione  
 Utilizzare la procedura riportata di seguito per navigare fino a questo percorso nell'interfaccia utente.  
  
###### <a name="to-open-the-security-page-for-an-item"></a>Per aprire la pagina Sicurezza per un elemento  
  
1.  Aprire Gestione report, quindi individuare l'elemento per il quale si desidera configurare le impostazioni di sicurezza.  
  
2.  Posizionare il puntatore del mouse sull'elemento, quindi fare clic sulla freccia a discesa.  
  
3.  Nel menu a discesa, eseguire uno dei passaggi seguenti:  
  
    -   Fare clic su **Sicurezza**. Viene visualizzata la pagina delle proprietà Sicurezza per l'elemento.  
  
    -   Fare clic su **Gestisci** per aprire la pagina delle proprietà Generale per l'elemento. Quindi selezionare la scheda **Sicurezza** .  
  
 **Modifica sicurezza elemento**  
 Fare clic per modificare le impostazioni di sicurezza definite per l'elemento corrente. Se si modificano le impostazioni di sicurezza per una cartella, le modifiche verranno applicate al contenuto della cartella corrente e di tutte le relative sottocartelle.  
  
 Questo pulsante non è disponibile per la cartella Home.  
  
 Quando si modificano le impostazioni di sicurezza di un elemento sono disponibili i pulsanti seguenti.  
  
 **Elimina**  
 Selezionare la casella di controllo accanto al nome del gruppo o dell'utente che si desidera eliminare e fare clic su **Elimina**. Non è possibile eliminare l'ultima assegnazione di ruolo rimasta o un'assegnazione di ruolo predefinita, ad esempio "BUILTIN\Administrators", che rappresenta la base di riferimento per la sicurezza del server di report. L'eliminazione di un'assegnazione di ruolo non comporta l'eliminazione di account utente, account di gruppo o definizioni di ruolo.  
  
 **Nuova assegnazione ruolo**  
 Fare clic per visualizzare la pagina Nuova assegnazione ruolo nella quale è possibile creare assegnazioni di ruolo aggiuntive per l'elemento corrente. Per ulteriori informazioni, vedere la [pagina nuova assegnazione ruolo: modifica assegnazione ruolo &#40;Gestione report&#41;](../../2014/reporting-services/new-role-assignment-edit-role-assignment-page-report-manager.md).  
  
 **Ripristina sicurezza padre**  
 Fare clic per impostare le stesse impostazioni di sicurezza della cartella padre del livello immediatamente superiore. Se il meccanismo di ereditarietà non è mai interrotto in tutta la gerarchia di cartelle del server di report, verranno utilizzate le impostazioni di sicurezza della cartella principale, ovvero Home.  
  
 **Gruppo o utente**  
 Consente di visualizzare un elenco dei gruppi e degli utenti che fanno parte di un'assegnazione di ruolo esistente per l'elemento corrente. Le assegnazioni di ruolo esistenti per la cartella corrente sono definite per i gruppi e gli utenti visualizzati in questa colonna. È possibile fare clic sul nome di un gruppo o un utente per visualizzare o modificare i dettagli dell'assegnazione di ruolo.  
  
 **Ruoli**  
 Visualizza un elenco di una o più definizioni di ruolo che fanno parte di un'assegnazione di ruolo esistente. Se a un account utente o di gruppo vengono assegnati più ruoli, il gruppo o l'utente potrà eseguire tutte le attività incluse nei ruoli. Per visualizzare le attività associate a un ruolo, utilizzare SQL Server Management Studio per visualizzare le attività incluse in ogni definizione di ruolo.  
  
## <a name="see-also"></a>Vedi anche  
 [Guida sensibile al contesto Gestione report](../../2014/reporting-services/report-manager-f1-help.md)   
 [Ruoli predefiniti](security/role-definitions-predefined-roles.md)   
 [Concessione di autorizzazioni in un server di report in modalità nativa](security/granting-permissions-on-a-native-mode-report-server.md)   
 [Assegnazioni di ruolo](security/role-assignments.md)   
 [Definizioni dei ruoli](security/role-definitions.md)  
  
  
