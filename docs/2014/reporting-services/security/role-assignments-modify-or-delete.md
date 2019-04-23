---
title: Modificare o eliminare un'assegnazione di ruolo (Gestione report) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- removing role assignments
- roles [Reporting Services], assignments
- system roles [Reporting Services]
- modifying role assignments
- deleting role assignments
ms.assetid: 523bdd32-92cb-4b48-a3a9-d58b2385bde7
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: f8810a4df8c04703667e1b817931ada65fda0e5f
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2019
ms.locfileid: "59945427"
---
# <a name="modify-or-delete-a-role-assignment-report-manager"></a>Modificare o eliminare un'assegnazione di ruolo (Gestione report)
  Un'assegnazione di ruolo esegue il mapping di un account utente o di gruppo a una definizione di ruolo predefinita che include le attività che possono essere eseguite e determina i tipi di operazioni che un utente può eseguire in relazione a una cartella, un report, un modello o ad altro tipo di contenuto. Per creare, modificare o eliminare assegnazioni di ruolo, utilizzare Gestione report. Dopo avere creato un'assegnazione di ruolo per un particolare utente o gruppo, è possibile modificarla in un secondo momento selezionando un ruolo diverso. Se si desidera revocare autorizzazioni a un server di report, è possibile eliminare un'assegnazione di ruolo dal server di report stesso.  
  
 A seconda degli scopi, alcuni approcci potrebbero essere più appropriati rispetto ad altri. Gli esempi includono la personalizzazione o la creazione di una nuova definizione di ruolo o la modifica dell'appartenenza di un account di gruppo in Active Directory.  
  
 Se ad esempio un gruppo di utenti deve gestire completamente il contenuto, ma non deve disporre del set completo di autorizzazioni associato a Gestione contenuto, è possibile creare una nuova definizione di ruolo denominata Gestione contenuto reparto, in cui sono incluse tutte le attività di Gestione contenuto ad eccezione di **Set security policies for items**(Impostazione dei criteri di sicurezza per gli elementi).  
  
 Analogamente, se per un amministratore di sistema o di rete è più semplice gestire account di gruppo di Active Directory rispetto alle assegnazioni di ruolo in Gestione report, è possibile ridurre l'overhead della gestione delle assegnazioni di ruolo creando una sola assegnazione per un account di gruppo e successivamente adattare l'appartenenza a un gruppo quando gli utenti non richiedono più l'accesso ai report.  
  
 Se si stabilisce che la modifica o l'eliminazione di un'assegnazione di ruolo costituisce l'approccio migliore, tenere presente di controllare che le assegnazioni di ruolo vengano eseguite sia a livello di sistema che di elemento. Ogni tipo di assegnazione di ruolo viene configurato tramite pagine diverse in Gestione report.  
  
### <a name="to-modify-or-delete-a-system-role-assignment"></a>Per eliminare o modificare un'assegnazione di ruolo a livello di sistema  
  
1.  Avviare [Gestione report &#40;modalità nativa SSRS&#41;](../report-manager-ssrs-native-mode.md).  
  
2.  Fare clic su **Impostazioni sito**.  
  
3.  Fare clic su **Sicurezza**. Tutte le assegnazioni di ruolo a livello di sistema definite attualmente per il server o la distribuzione con scalabilità orizzontale vengono elencate in base al nome dell'account.  
  
4.  Individuare l'assegnazione di ruolo da modificare o eliminare.  
  
5.  Per aggiungere o rimuovere il ruolo per un particolare utente o gruppo, fare clic su **Modifica**.  
  
6.  Per eliminare un'assegnazione di ruolo, fare clic sulla casella di controllo accanto al nome dell'utente o del gruppo, quindi fare clic su **Elimina**.  
  
### <a name="to-modify-or-delete-an-item-role-assignment"></a>Per modificare o eliminare un'assegnazione di ruolo a livello di elemento  
  
1.  Avviare **Gestione report** e individuare l'elemento per il quale si desidera modificare o eliminare un'assegnazione di ruolo.  
  
2.  Posizionare il puntatore del mouse sull'elemento, quindi fare clic sulla freccia a discesa.  
  
3.  Scegliere **Sicurezza**dal menu a discesa.  
  
4.  Individuare l'assegnazione di ruolo da modificare o eliminare.  
  
5.  Per aggiungere o rimuovere il ruolo per un particolare utente o gruppo, fare clic su **Modifica**.  
  
6.  Per eliminare un'assegnazione di ruolo, fare clic sulla casella di controllo accanto al nome dell'utente o del gruppo, quindi fare clic su **Elimina**.  
  
## <a name="see-also"></a>Vedere anche  
 (create-and-manage-role-assignments.md)   
 [Assegnazioni di ruolo](role-assignments.md)   
 [Pagina Impostazioni sito &#40;Gestione report&#41;](../site-settings-page-report-manager.md)   
 [Nuova assegnazione di ruolo di sistema: Modificare la pagina Assegnazioni ruolo del sistema &#40;gestione Report&#41;](../new-system-role-assignments-edit-system-role-assignments-page-report-manager.md)  
  
  
