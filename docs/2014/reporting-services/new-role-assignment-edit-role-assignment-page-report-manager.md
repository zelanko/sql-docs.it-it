---
title: 'Pagina Nuova assegnazione di ruolo: Modifica assegnazione ruolo (gestione Report) | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 3319ced0-4b86-42af-b18d-da41a625113c
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: fc4dd805faffb9fcf172f372f48d497a037fd16c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63188402"
---
# <a name="new-role-assignment-edit-role-assignment-page-report-manager"></a>Pagina Nuova assegnazione di ruolo: Modifica assegnazione ruolo (gestione Report)
  La pagina Nuova assegnazione ruolo o Modifica assegnazione ruolo consente di concedere le autorizzazioni per operazioni ed elementi del server di report. Per ogni utente che deve accedere a un server di report è necessario definire almeno un'assegnazione di ruolo per definire il livello di accesso. È possibile creare assegnazioni di ruolo nel nodo radice o in uno specifico report, modello, cartella, risorsa o origine dati condivisa. Il sistema di sicurezza di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] si basa su assegnazioni di ruolo che vengono applicate agli elementi. Tramite un'assegnazione di ruolo, un gruppo o un utente viene assegnato a una definizione di ruolo e ogni definizione di ruolo identifica le attività che i gruppi o gli utenti sono autorizzati a eseguire in relazione a un elemento specifico.  
  
 Le assegnazioni di ruolo a livello di elemento possono avere effetti estesi. Sebbene possano essere associate a un singolo report o a una singola cartella, è inoltre possibile definire le assegnazioni a un livello alto della gerarchia di cartelle in modo che vengano ereditate dalle cartelle e dagli elementi ai livelli inferiori dell'albero. Per altre informazioni, vedere [Concedere l'accesso utente a un server di report &#40;Gestione report&#41;](security/grant-user-access-to-a-report-server.md).  
  
## <a name="navigation"></a>Navigazione  
 Utilizzare la procedura riportata di seguito per navigare fino a questo percorso nell'interfaccia utente.  
  
###### <a name="to-open-the-new-role-assignment-or-edit-role-assignment-page"></a>Per aprire la pagina Nuova assegnazione ruolo o Modifica assegnazione ruolo  
  
1.  Aprire Gestione report e individuare un elemento per il quale si desidera aggiungere una nuova assegnazione di ruolo o modificare un'assegnazione di ruolo.  
  
2.  Posizionare il puntatore del mouse sull'elemento, quindi fare clic sulla freccia a discesa.  
  
3.  Scegliere **Sicurezza**dal menu a discesa. Viene visualizzata la pagina delle proprietà Sicurezza per l'elemento.  
  
4.  Se si desidera aggiungere una nuova assegnazione di ruolo, sulla barra degli strumenti fare clic su **Nuova assegnazione ruolo**. Se si desidera modificare un'assegnazione di ruolo, fare clic su **Modifica** accanto al nome del gruppo o dell'utente che si desidera modificare.  
  
    > [!NOTE]  
    >  Se un elemento eredita le impostazioni di sicurezza da un elemento padre, fare clic su **Modifica sicurezza elemento** sulla barra degli strumenti, per modificare le impostazioni di sicurezza.  
  
## <a name="options"></a>Opzioni  
 **Nome gruppo o utente**  
 Digitare il nome di un account utente o di gruppo per il quale si desidera creare l'assegnazione di ruolo. Il nome utente o il nome di gruppo deve corrispondere a un account di dominio di Windows valido. Immettere l'account nel formato seguente: \<dominio >\\< account\>.  
  
> [!NOTE]  
>  Questa casella è disponibile solo nella pagina Nuova assegnazione ruolo.  
  
 **Ruolo**  
 Mostra tutti i ruoli definiti nel server di report che possono essere utilizzati per impostare la sicurezza per gli elementi. Per la creazione o la modifica di un'assegnazione di ruolo per un report o una cartella, selezionare uno o più ruoli fino a ottenere il set di attività corrispondente alle azioni che gli utenti devono essere autorizzati a eseguire. Per visualizzare il set di attività supportate da ogni ruolo, utilizzare [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]. Non è possibile visualizzare, creare, modificare o eliminare ruoli in Gestione report. Per istruzioni, vedere [creare, eliminare o modificare un ruolo &#40;Management Studio&#41;](security/role-definitions-create-delete-or-modify.md).  
  
 **Descrizione**  
 Visualizza informazioni aggiuntive sul ruolo. Per i ruoli predefiniti, ad esempio **Visualizzazione** o **Gestione contenuto**, la descrizione riepiloga le attività supportate da ogni ruolo.  
  
 **Elimina assegnazione ruolo**  
 Fare clic per eliminare l'assegnazione ruolo esistente per un utente o un gruppo. Non è possibile eliminare l'ultima assegnazione di ruolo rimasta (a ogni elemento deve essere associata almeno una assegnazione di ruolo).  
  
> [!NOTE]  
>  Questo pulsante è disponibile solo nella pagina Modifica assegnazione ruolo.  
  
## <a name="see-also"></a>Vedere anche  
 [Creare, eliminare o modificare un ruolo &#40;Management Studio&#41;](security/role-definitions-create-delete-or-modify.md)   
 [Concessione di autorizzazioni in un server di report in modalità nativa](security/granting-permissions-on-a-native-mode-report-server.md)   
 [Gestione report &#40;modalità nativa SSRS&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [Guida F1 di gestione report](../../2014/reporting-services/report-manager-f1-help.md)   
 [Assegnazioni di ruolo](security/role-assignments.md)   
 [Concedere l'accesso utente a un server di report &#40;Gestione report&#41;](security/grant-user-access-to-a-report-server.md)  
  
  
