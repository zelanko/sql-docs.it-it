---
title: Programma esterno di Posta elettronica database | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- external programs [Database Mail]
- DatabaseMail90.exe
- Database Mail [SQL Server], external programs
ms.assetid: bc124164-eb6e-4b7f-bf66-98a3113d02f7
author: stevestein
ms.author: sstein
ms.openlocfilehash: 220080e231c63f0224af9054039298fddd83ad96
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "68134446"
---
# <a name="database-mail-external-program"></a>Programma esterno di Posta elettronica database
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  L'eseguibile esterno di Posta elettronica database è **DatabaseMail.exe**, situato nella **directory MSSQL\Binn** dell'installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Posta elettronica database utilizza l'attivazione di Service Broker per avviare il programma esterno in presenza di messaggi di posta elettronica da elaborare. Posta elettronica database avvia un'istanza del programma esterno. Il programma esterno viene eseguito nel contesto di sicurezza dell'account di servizio per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **Contenuto dell'argomento**  
  
-   [Concetti relativi al Programma esterno di Posta elettronica database](#ComponentsAndConcepts)  
  
-   [Attività correlate alla configurazione del Programma esterno di Posta elettronica database](#RelatedTasks)  
  
##  <a name="database-mail-external-program-concepts"></a><a name="ComponentsAndConcepts"></a> Concetti relativi al Programma esterno di Posta elettronica database  
 All'avvio del programma esterno, il programma viene connesso a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizzando l'autenticazione di Windows e viene avviata l'elaborazione dei messaggi di posta elettronica. In assenza di messaggi da inviare per il periodo di timeout specificato, il programma viene chiuso. È possibile configurare il tempo di attesa da parte del programma prima della chiusura utilizzando Configurazione guidata posta elettronica database oppure le stored procedure di Posta elettronica database. Per altre informazioni, vedere [sysmail_configure_sp &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-configure-sp-transact-sql.md).  
  
 Il programma esterno archivia le informazioni in tabelle di sistema nel database **msdb** . Se il programma esterno non è in grado di comunicare con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], registra gli errori nel registro eventi applicazioni di Microsoft Windows. La registrazione aggiuntiva dei messaggi è disponibile quando il livello di registrazione è impostato su **Dettagliati** nella finestra di dialogo **Configurazione parametri di sistema** della **Configurazione guidata posta elettronica database**.  
  
 Si noti che, per motivi di efficienza, il programma esterno memorizza nella cache le informazioni relative a profili e account. Pertanto, le modifiche alla configurazione di profili e account potrebbero non venire trasmesse al programma esterno per alcuni minuti.  
  
##  <a name="tasks-related-to-configuring-database-mail-external-program"></a><a name="RelatedTasks"></a> Attività correlate alla configurazione del Programma esterno di Posta elettronica database  
  
|Attività di configurazione|Collegamento all'argomento|  
|------------------------|----------------|  
|Specificare l'ora che il Programma Esterno prima di uscire.|[sysmail_configure_sp &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-configure-sp-transact-sql.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [SQL Server Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md)   
 [Controlli e registrazione di Posta elettronica database](../../relational-databases/database-mail/database-mail-log-and-audits.md)   
 [Posta elettronica database](../../relational-databases/database-mail/database-mail.md)  
  
  
