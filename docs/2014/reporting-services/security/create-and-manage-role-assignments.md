---
title: Creare e gestire assegnazioni di ruolo | Microsoft Docs
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
- security [Reporting Services], role assignments
- modifying role assignments
- deleting role assignments
ms.assetid: 086d0987-b43c-4834-8372-e08fb4b432f8
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 2f22a5af8401a0cf16c508f805dbb38ee9970780
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63242681"
---
# <a name="create-and-manage-role-assignments"></a>Creare e gestire assegnazioni di ruolo
  Un' *assegnazione di ruolo* rappresenta criteri di sicurezza che determinano se un utente o un gruppo può accedere a un elemento specifico del server di report oppure eseguire una determinata operazione. Un'assegnazione di ruolo è costituita da un unico nome di un account utente o di gruppo e da una o più definizioni di ruolo.  
  
 L'ambito delle assegnazioni di ruolo è definito a *livello di elemento* oppure a *livello di sistema*.  
  
-   Un'assegnazione di ruolo a livello di elemento viene sempre creata nel contesto di un elemento o di un ramo specifico nella gerarchia di cartelle del server di report. Per creare un'assegnazione di ruolo per una cartella o un elemento specifico, è necessario accedere a tale elemento o cartella.  
  
-   Le assegnazioni di ruolo a livello di sistema consentono agli utenti selezionati di eseguire attività che influiscono complessivamente sul sito del server di report. Sono comprese in tali attività la creazione di pianificazioni condivise, la gestione di processi, l'elaborazione di report in Generatore report e l'impostazione di proprietà. La sicurezza a livello di sistema non definisce le impostazioni di accesso agli elementi della gerarchia di cartelle del server di report.  
  
## <a name="creating-an-item-level-role-assignment"></a>Creazione di un'assegnazione di ruolo a livello di elemento  
 Per creare o gestire assegnazioni di ruolo, utilizzare Gestione report e aprire le pagine delle proprietà relative alla sicurezza dell'elemento da proteggere.  
  
 È necessario creare un'assegnazione di ruolo separata per ogni account utente o di gruppo che richiede l'accesso al server di report. Se l'account fa parte di un dominio diverso da quello in cui si trova il server di report, è necessario specificare il nome di dominio. Dopo aver specificato un account, è possibile scegliere una o più definizioni di ruolo. Le definizioni di ruolo si sommano tra loro, ovvero un'assegnazione supporta la combinazione di tutte le attività delle varie definizioni per un utente o un gruppo particolare.  
  
 Per consentire l'accesso al livello più generale possibile, è consigliabile scegliere un elemento nella parte alta della gerarchia di cartelle, ad esempio il nodo radice Home. In seguito sarà possibile creare assegnazioni di ruolo per impedire l'accesso ad aree specifiche della gerarchia di cartelle.  
  
 Per creare un'assegnazione di ruolo, è necessario appartenere al gruppo locale Administrators nel server di report. È possibile delegare tale compito assegnando altri utenti al ruolo **Gestione contenuto** .  
  
 Per altre informazioni, vedere [Concedere l'accesso utente a un server di report &#40;Gestione report&#41;](grant-user-access-to-a-report-server.md)dovrebbe essere assegnato a pochissimi utenti.  
  
## <a name="creating-a-system-level-role-assignment"></a>Creazione di un'assegnazione di ruolo a livello di sistema  
 Per creare o gestire un'assegnazione di ruolo a livello di sistema, utilizzare Gestione report e aprire la pagina Impostazioni sito.  
  
 Le assegnazioni di ruolo a livello di sistema e di elemento sono associate. È necessario creare un'assegnazione di ruolo a livello di sistema per ogni utente o gruppo che dispone di un'assegnazione di ruolo a livello di elemento.  
  
 Le assegnazioni di ruolo a livello di sistema includono un'ampia gamma di autorizzazioni, ma non includono autorizzazioni appartenenti a un'assegnazione di ruolo a livello di elemento. Contrariamente alle autorizzazioni di sistema in un computer, i ruoli di sistema nei server di report non definiscono le autorizzazioni complete che includono il set completo di tutte le possibili operazioni, ma specificano solo un set di attività il cui ambito è il sito del server di report. Le autorizzazioni definite tramite assegnazioni di ruolo a livello di sistema determinano se gli utenti possono visualizzare proprietà dell'applicazione, ad esempio l'immagine o il titolo della Home page, visualizzare o gestire pianificazioni condivise o utilizzare Generatore report.  
  
 Per altre informazioni, vedere [Concedere l'accesso utente a un server di report &#40;Gestione report&#41;](grant-user-access-to-a-report-server.md) e [Ruoli predefiniti](role-definitions-predefined-roles.md).  
  
## <a name="modifying-a-role-assignment"></a>Modifica di assegnazioni di ruolo  
 Un'assegnazione di ruolo può essere modificata in qualsiasi momento. Le modifiche hanno effetto quando l'assegnazione viene salvata, ma non vengono applicate durante una sessione utente. Se infatti si modifica un'assegnazione di ruolo per negare l'accesso al report mentre è aperto da un utente, l'utente può comunque continuare a utilizzarlo fino a quando non chiude la propria sessione.  
  
 Se si aggiunge un account utente a un gruppo che fa già parte di un'assegnazione di ruolo, trascorrerà un certo periodo di tempo prima che l'account utente sia in grado di accedere agli elementi tramite i criteri dell'account di gruppo. Questo ritardo è dovuto alla memorizzazione nella cache dei token di autenticazione da parte di Internet Information Services (IIS). È possibile attendere che i token vengano aggiornati (in genere l'attesa è di quindici minuti) oppure reimpostare IIS in modo che la cache venga aggiornata immediatamente.  
  
 È possibile modificare una sola assegnazione di ruolo alla volta. Non è possibile eseguire un'operazione di ricerca e sostituzione globale per modificare i nomi delle definizioni di ruolo o le impostazioni delle assegnazioni di ruolo né per individuare tutte le assegnazioni di ruolo che includono un utente o un gruppo specifico.  
  
## <a name="deleting-a-role-assignment"></a>Eliminazione di assegnazioni di ruolo  
 È possibile eliminare un'assegnazione di ruolo selezionando la casella di controllo accanto all'assegnazione che si vuole eliminare e quindi facendo clic su **Elimina**. È inoltre possibile eliminare assegnazioni di ruolo facendo clic su **Ripristina sicurezza padre**. Quando si fa clic su questo pulsante, le assegnazioni di ruolo esistenti per l'elemento vengono eliminate e al loro posto vengono utilizzate le assegnazioni di ruolo ereditate tramite un elemento padre.  
  
## <a name="see-also"></a>Vedere anche  
 [Concedere l'accesso utente a un server di report &#40;Gestione report&#41;](grant-user-access-to-a-report-server.md)   
 [Modificare o eliminare un'assegnazione di ruolo &#40;Gestione report&#41;](role-assignments-modify-or-delete.md)   
 [Assegnazioni di ruolo](role-assignments.md)   
 [Definizioni di ruolo](role-definitions.md)   
 [Predefined Roles](role-definitions-predefined-roles.md)   
 [Concessione di autorizzazioni in un server di report in modalità nativa](granting-permissions-on-a-native-mode-report-server.md)  
  
  
