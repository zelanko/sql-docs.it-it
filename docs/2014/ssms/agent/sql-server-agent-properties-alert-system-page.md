---
title: Proprietà SQL Server Agent (pagina Sistema avvisi) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql12.ag.agent.alert.f1
ms.assetid: 3e6d3bfd-20ee-4593-86cc-f65b1c08c69d
author: stevestein
ms.author: sstein
ms.openlocfilehash: e5e87f5a13c8f156cd7d2788bb9004ec20fcd3eb
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85058725"
---
# <a name="sql-server-agent-properties-alert-system-page"></a>Proprietà SQL Server Agent (pagina Sistema avvisi)
  Utilizzare questa pagina per visualizzare e modificare le impostazioni per i messaggi inviati dagli [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] avvisi di Agent.  
  
## <a name="options"></a>Opzioni  
 **Sessione di posta elettronica**  
 Le opzioni incluse in questa sezione consentono di configurare la posta elettronica di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
 **Abilita profilo di posta**  
 Consente di abilitare la posta elettronica di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Per impostazione predefinita, la posta elettronica di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non è abilitata.  
  
 **Sistema di posta elettronica**  
 Consente di impostare il sistema di posta elettronica utilizzato da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Posta elettronica database  
  
> [!NOTE]  
>  Dopo avere modificato il sistema di posta elettronica, è necessario riavviare il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent per rendere operative le modifiche.  
  
 **Profilo posta**  
 Consente di impostare il profilo che deve essere utilizzato in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. È anche possibile scegliere **\<new Database Mail profile...>** di creare un nuovo profilo.  
  
 **Messaggi di posta elettronica tramite cercapersone**  
 Le opzioni incluse in questa sezione consentono di configurare i messaggi di posta elettronica inviati a indirizzi di cercapersone in modo che possano funzionare con il sistema di cercapersone utilizzato.  
  
 **Formato indirizzo per messaggi di posta elettronica tramite cercapersone**  
 Questa sezione consente di specificare il formato degli indirizzi e della riga dell'oggetto dei messaggi di posta elettronica inviati tramite cercapersone.  
  
 **Riga A**  
 Consente di specificare le opzioni della riga **A** del messaggio  
  
 **Prefisso**  
 Consente di digitare un testo fisso richiesto dal sistema di cercapersone all'inizio della riga **A** dei messaggi inviati a un cercapersone.  
  
 **Cercapersone**  
 Consente di includere l'indirizzo di posta elettronica del messaggio tra il prefisso e il suffisso.  
  
 **Suffisso**  
 Consente di digitare un testo fisso richiesto dal sistema di cercapersone alla fine della riga **A** dei messaggi inviati a un cercapersone.  
  
 **Riga Cc**  
 Consente di specificare le opzioni della riga **Cc** del messaggio.  
  
 **Prefisso**  
 Consente di digitare un testo fisso richiesto dal sistema di cercapersone all'inizio della riga **Cc** dei messaggi inviati a un cercapersone.  
  
 **Cercapersone**  
 Consente di includere l'indirizzo di posta elettronica del messaggio tra il prefisso e il suffisso.  
  
 **Suffisso**  
 Consente di digitare un testo fisso richiesto dal sistema di cercapersone alla fine della riga **Cc** dei messaggi inviati a un cercapersone.  
  
 **Oggetto**  
 Consente di specificare le opzioni dell'oggetto del messaggio.  
  
 **Prefisso**  
 Consente di digitare un testo fisso richiesto dal sistema di cercapersone all'inizio della riga **Oggetto** dei messaggi inviati a un cercapersone.  
  
 **Suffisso**  
 Consente di digitare un testo fisso richiesto dal sistema di cercapersone alla fine della riga **Oggetto** dei messaggi inviati a un cercapersone.  
  
 **Includi corpo del messaggio nel messaggio di notifica**  
 Consente di includere il corpo del messaggio di posta elettronica nel messaggio inviato al cercapersone.  
  
 **Operatore alternativo**  
 Questa sezione consente di specificare le opzioni dell'operatore alternativo.  
  
 **Abilita operatore alternativo**  
 Consente di specificare un operatore alternativo.  
  
 **Operatore**  
 Consente di impostare il nome dell'operatore alternativo a cui inviare le notifiche.  
  
 **Notifica tramite**  
 Consente di impostare la modalità di invio delle notifiche all'operatore alternativo.  
  
 **Sostituzione token**  
 Questa sezione consente di abilitare i token dei passaggi del processo che possono essere utilizzati nei processi eseguiti dagli avvisi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Per altre informazioni sui token dei passaggi dei processi, vedere [Utilizzo dei token nei passaggi dei processi](use-tokens-in-job-steps.md).  
  
> [!IMPORTANT]  
>  Qualsiasi utente di Windows che disponga di autorizzazioni di scrittura per il registro eventi di Windows può accedere ai passaggi dei processi attivati dagli avvisi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Per evitare rischi per la sicurezza, i token di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent che possono essere utilizzati in processi attivati dagli avvisi sono disabilitati per impostazione predefinita. I token interessati sono: **$(A-DBN)**, **$(A-SVR)**, **$(A-ERR)**, **$(A-SEV)** e **$(A-MSG)**.  
>   
>  Se è necessario utilizzare tali token, prima di abilitarli verificare che solo i membri di gruppi di sicurezza di Windows trusted, ad esempio il gruppo Administrators, dispongano di autorizzazioni di scrittura per il registro eventi del computer in cui è installato [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 **Sostituisci token per tutte le risposte del processo ad avvisi**  
 Selezionare questa casella di controllo per abilitare la sostituzione dei token per i processi attivati dagli avvisi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="see-also"></a>Vedere anche  
 [Operatori](operators.md)   
 [Configurare SQL Server Agent Mail per l'uso di Posta elettronica database](../../relational-databases/database-mail/configure-sql-server-agent-mail-to-use-database-mail.md)   
 [Posta elettronica database](../../relational-databases/database-mail/database-mail.md)  
  
  
