---
title: Proprietà SQL Server Agent (pagina Sistema avvisi) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.ag.agent.alert.f1
ms.assetid: 3e6d3bfd-20ee-4593-86cc-f65b1c08c69d
author: markingmyname
ms.author: maghan
manager: jroth
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 038434c125ba980e726e5efad0b51161ef75ec99
ms.sourcegitcommit: 5d839dc63a5abb65508dc498d0a95027d530afb6
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/09/2019
ms.locfileid: "67681829"
---
# <a name="sql-server-agent-properties-alert-system-page"></a>Proprietà SQL Server Agent (pagina Sistema avvisi)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> In [Istanza gestita di database SQL di Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) sono attualmente supportate la maggior parte delle funzionalità di SQL Server Agent, ma non tutte. Per informazioni dettagliate, vedere [Differenze T-SQL tra Istanza gestita del database SQL di Azure e SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

Usare questa pagina per visualizzare e modificare le impostazioni per i messaggi inviati dagli avvisi di [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
## <a name="options"></a>Opzioni  
**Sessione di posta elettronica**  
Le opzioni incluse in questa sezione consentono di configurare la posta elettronica di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
**Abilita profilo di posta**  
Consente di abilitare la posta elettronica di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Per impostazione predefinita, la posta elettronica di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non è abilitata.  
  
**Sistema di posta elettronica**  
Consente di impostare il sistema di posta elettronica utilizzato da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Posta elettronica database  
  
> [!NOTE]  
> Dopo avere modificato il sistema di posta elettronica, è necessario riavviare il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent per rendere operative le modifiche.  
  
**Profilo posta**  
Consente di impostare il profilo che deve essere utilizzato in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. È inoltre possibile selezionare **\<nuovo profilo di Posta elettronica database>** per creare un nuovo profilo.  
  
**Messaggi di posta elettronica tramite cercapersone**  
Le opzioni incluse in questa sezione consentono di configurare i messaggi di posta elettronica inviati a indirizzi di cercapersone in modo che possano funzionare con il sistema di cercapersone utilizzato.  
  
**Formato indirizzo per messaggi di posta elettronica tramite cercapersone**  
Questa sezione consente di specificare il formato degli indirizzi e della riga dell'oggetto dei messaggi di posta elettronica inviati tramite cercapersone.  
  
**Riga A**  
Consente di specificare le opzioni della riga **A** del messaggio  
  
**Prefix**  
Consente di digitare un testo fisso richiesto dal sistema di cercapersone all'inizio della riga **A** dei messaggi inviati a un cercapersone.  
  
**Cercapersone**  
Consente di includere l'indirizzo di posta elettronica del messaggio tra il prefisso e il suffisso.  
  
**Suffisso**  
Consente di digitare un testo fisso richiesto dal sistema di cercapersone alla fine della riga **A** dei messaggi inviati a un cercapersone.  
  
**Riga Cc**  
Consente di specificare le opzioni della riga **Cc** del messaggio.  
  
**Prefix**  
Consente di digitare un testo fisso richiesto dal sistema di cercapersone all'inizio della riga **Cc** dei messaggi inviati a un cercapersone.  
  
**Cercapersone**  
Consente di includere l'indirizzo di posta elettronica del messaggio tra il prefisso e il suffisso.  
  
**Suffisso**  
Consente di digitare un testo fisso richiesto dal sistema di cercapersone alla fine della riga **Cc** dei messaggi inviati a un cercapersone.  
  
**Oggetto**  
Consente di specificare le opzioni dell'oggetto del messaggio.  
  
**Prefix**  
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
Questa sezione consente di abilitare i token dei passaggi del processo che possono essere utilizzati nei processi eseguiti dagli avvisi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Per altre informazioni sui token dei passaggi dei processi, vedere [Utilizzo dei token nei passaggi dei processi](../../ssms/agent/use-tokens-in-job-steps.md).  
  
> [!IMPORTANT]  
> Qualsiasi utente di Windows che disponga di autorizzazioni di scrittura per il registro eventi di Windows può accedere ai passaggi dei processi attivati dagli avvisi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Per evitare rischi per la sicurezza, i token di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent che possono essere utilizzati in processi attivati dagli avvisi sono disabilitati per impostazione predefinita. I token interessati sono: **$(A-DBN)** , **$(A-SVR)** , **$(A-ERR)** , **$(A-SEV)** e **$(A-MSG)** .  
>   
> Se è necessario utilizzare tali token, prima di abilitarli verificare che solo i membri di gruppi di sicurezza di Windows trusted, ad esempio il gruppo Administrators, dispongano di autorizzazioni di scrittura per il registro eventi del computer in cui è installato [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
**Sostituisci token per tutte le risposte del processo ad avvisi**  
Selezionare questa casella di controllo per abilitare la sostituzione dei token per i processi attivati dagli avvisi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="see-also"></a>Vedere anche  
[Operatori](../../ssms/agent/operators.md)  
[Configurare Posta elettronica di SQL Server Agent per l'utilizzo di Posta elettronica database](../../relational-databases/database-mail/configure-sql-server-agent-mail-to-use-database-mail.md)  
[Posta elettronica database](../../relational-databases/database-mail/database-mail.md)  
  
