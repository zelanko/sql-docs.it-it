---
title: Nuovo ruolo utente (Management Studio) | Microsoft Docs
description: Informazioni su come creare una definizione di ruolo a livello di elemento in cui siano enumerate le attività che un utente può eseguire nella pagina Nuovo ruolo utente di SQL Server Management Studio.
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: tools
ms.topic: conceptual
f1_keywords:
- sql13.swb.reportserver.newrole.f1
ms.assetid: 9f76a235-0b58-479c-8e5b-50588091b71c
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 853ef460d56f1561b735ccaff1acfb95b6dfc580
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/22/2020
ms.locfileid: "86913917"
---
# <a name="new-user-role-management-studio"></a>Nuovo ruolo utente (Management Studio)
  Utilizzare questa pagina per creare una definizione di ruolo a livello di elemento. Una definizione di ruolo a livello di elemento è una raccolta denominata di attività che elenca quelle eseguibili dagli utenti in relazione a cartelle, report, modelli, risorse e origini dei dati condivise. Un esempio di definizione di ruolo a livello di elemento è il ruolo predefinito Visualizzazione che identifica il tipo di azioni che un utente finale di un report potrebbe avere la necessità di eseguire per l'esplorazione delle cartelle e la visualizzazione dei report.  
  
 Le definizioni di ruolo sono progettate per essere in numero limitato. Per la maggior parte delle organizzazioni sono infatti necessarie solo poche definizioni di ruolo. Se le definizioni di ruolo predefinite fossero insufficienti, è comunque possibile modificarle o crearne di nuove.  
  
> [!NOTE]  
>  Le definizioni di ruolo vengono utilizzate solo in un server di report in esecuzione in modalità nativa. Se il server di report è configurato per l'integrazione con SharePoint, questa pagina non è disponibile.  
  
## <a name="options"></a>Opzioni  
 **Nome**  
 Consente di digitare la definizione del ruolo. I nomi di definizione di ruolo devono essere univoci nell'ambito dello spazio dei nomi del server di report. Il nome deve includere almeno un carattere alfanumerico. È inoltre possibile utilizzare spazi e alcuni simboli. Il nome non può contenere i caratteri seguenti:  
  
 ; ? : \@ & = + , $ / * < >  
  
 " /  
  
 **Descrizione**  
 Consente di digitare una descrizione per illustrare le modalità di utilizzo del ruolo ed elencare le azioni supportate.  
  
 **Attività**  
 Consente di selezionare le attività che possono essere eseguite tramite questo ruolo. Non è possibile creare nuove attività o modificare attività esistenti supportate da [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. In una definizione di ruolo a livello di elemento è possibile utilizzare solo attività a livello di elemento.  
  
 **Descrizione dell'attività**  
 Visualizza una descrizione dell'attività, che include le operazioni o autorizzazioni supportate.  
  
## <a name="see-also"></a>Vedere anche  
 [Guida sensibile al contesto del server di report in Management Studio](../../reporting-services/tools/report-server-in-management-studio-f1-help.md)   
 [Definizioni di ruolo](../../reporting-services/security/role-definitions.md)  
  
  
