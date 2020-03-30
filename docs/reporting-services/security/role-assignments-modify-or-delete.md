---
title: Modificare o eliminare un'assegnazione di ruolo (portale Web SSRS) | Microsoft Docs
ms.date: 05/07/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: security
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
ms.openlocfilehash: 28695a4849b29c6e593f42489fc149efd9a8db53
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "65570651"
---
# <a name="role-assignments---modify-or-delete"></a>Assegnazioni di ruolo - Modificare o eliminare

Un'assegnazione di ruolo associa un account utente o di gruppo a un ruolo predefinito che definisce le attività che possono essere eseguite. Determina i tipi di attività eseguiti da un utente su una cartella, un report, un modello o un altro tipo di contenuto. Per creare, modificare o eliminare le assegnazioni di ruolo, usare il portale Web SSRS. Dopo avere creato un'assegnazione di ruolo per un particolare utente o gruppo, è possibile modificarla in un secondo momento selezionando un ruolo diverso. Se si desidera revocare autorizzazioni a un server di report, è possibile eliminare un'assegnazione di ruolo dal server di report stesso.  

A seconda degli scopi, alcuni approcci potrebbero essere più appropriati rispetto ad altri. Gli esempi includono la personalizzazione o la creazione di una nuova definizione di ruolo o la modifica dell'appartenenza di un account di gruppo in Active Directory.  

Se un gruppo di utenti deve gestire il proprio contenuto ma non è opportuno che abbia il set completo di autorizzazioni associato a Gestione contenuto, ad esempio, è possibile creare una nuova definizione di ruolo denominata Gestione contenuto reparto che includa tutte le attività di Gestione contenuto tranne **l'impostazione dei criteri di sicurezza per gli elementi**.

Analogamente, per un amministratore di sistema o di rete è probabilmente più semplice gestire account di gruppo di Active Directory piuttosto che assegnazioni di ruolo nel portale Web. È possibile ridurre il sovraccarico di gestione delle assegnazioni di ruolo creando una singola assegnazione di ruolo per un account di gruppo, quindi modificare l'appartenenza al gruppo quando gli utenti non devono più accedere ai report.
  
 Se si stabilisce che la modifica o l'eliminazione di un'assegnazione di ruolo è l'approccio migliore, ricordarsi di controllare sia le assegnazioni di ruolo a livello di sistema sia quelle a livello di elemento. Ogni tipo di assegnazione di ruolo viene configurato tramite pagine diverse del portale Web.
  
## <a name="to-modify-or-delete-a-system-role-assignment"></a>Per eliminare o modificare un'assegnazione di ruolo a livello di sistema
  
1. Accedere al [portale Web di un server di report &#40;modalità nativa SSRS&#41;](../../reporting-services/web-portal-ssrs-native-mode.md).

2. Selezionare **Impostazioni sito** > **Sicurezza**. Tutte le assegnazioni di ruolo a livello di sistema definite attualmente per il server o la distribuzione con scalabilità orizzontale vengono elencate in base al nome dell'account.

3. Individuare l'assegnazione di ruolo da modificare o eliminare.

4. Per aggiungere o rimuovere il ruolo per un determinato utente o gruppo, selezionare **Modifica**.

5. Per eliminare un'assegnazione di ruolo, selezionare la casella di controllo accanto al nome dell'utente o del gruppo e quindi **Elimina**.

### <a name="to-modify-or-delete-an-item-role-assignment"></a>Per modificare o eliminare un'assegnazione di ruolo a livello di elemento

1. Accedere al portale Web e individuare l'elemento per cui si vuole modificare o eliminare un'assegnazione di ruolo.

2. Passare il puntatore del mouse sull'elemento e selezionare la freccia a discesa.

3. Nel menu a discesa selezionare **Sicurezza**.

4. Individuare l'assegnazione di ruolo da modificare o eliminare.

5. Per aggiungere o rimuovere il ruolo per un determinato utente o gruppo, selezionare **Modifica**.

6. Per eliminare un'assegnazione di ruolo, selezionare la casella di controllo accanto al nome dell'utente o del gruppo e quindi **Elimina**.

## <a name="see-also"></a>Vedere anche

[Creare e gestire assegnazioni di ruolo](../../reporting-services/security/create-and-manage-role-assignments.md)  
[Assegnazioni di ruolo](../../reporting-services/security/role-assignments.md)  
