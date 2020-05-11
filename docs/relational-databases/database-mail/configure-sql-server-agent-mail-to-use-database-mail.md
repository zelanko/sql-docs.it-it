---
title: Configurare Posta elettronica di SQL Server Agent per l'utilizzo di Posta elettronica database
ms.date: 08/05/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- Database Mail [SQL Server], SQL Server Agent Mail
- SQL Server Agent Mail
ms.assetid: 4b8b61bd-4bd1-43cd-b6e5-c6ed2e101dce
author: stevestein
ms.author: sstein
ms.custom: seo-dt-2019
ms.openlocfilehash: 1e449c95c6dd087eaa70de48b1fb79ac8d7b6f6c
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/04/2020
ms.locfileid: "82763202"
---
# <a name="configure-sql-server-agent-mail-to-use-database-mail"></a>Configurare Posta elettronica di SQL Server Agent per l'utilizzo di Posta elettronica database
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  In questo argomento viene illustrato come configurare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent per utilizzare Posta elettronica database per inviare notifiche e avvisi in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  Per informazioni su come abilitare e configurare la funzionalità Posta elettronica database, vedere [Configurare Posta elettronica database](../../relational-databases/database-mail/configure-database-mail.md).  Per un esempio sull'uso di [!INCLUDE[tsql](../../includes/tsql-md.md)], vedere [Creare un profilo di Posta elettronica database](../../relational-databases/database-mail/create-a-database-mail-profile.md).
  
-   **Prima di iniziare:**  
  
-   [Prerequisiti](#Prerequisites)  
  
-   [Sicurezza](#Security)  
  
-   [Per configurare SQL Server Agent Mail per l'utilizzo di Posta elettronica database tramite SQL Server Management Studio](#SSMSProcedure)  
  
-   [Attività di completamento](#Follow_Up)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Prima di iniziare  
  
  > [!NOTE]
  > SQL Agent su Istanza gestita è sempre configurato per l'uso di Posta elettronica database, quindi questo contenuto non è applicabile in Istanza gestita. In Istanza gestita è necessario disporre di un profilo che deve essere chiamato **[AzureManagedInstance_dbmail_profile](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)** per associare SQL Agent a Posta elettronica database. 
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> Prerequisiti  
  
-   [Abilitare Posta elettronica database](../../relational-databases/database-mail/configure-database-mail.md).  
  
-    [Creare un account di Posta elettronica database](../../relational-databases/database-mail/create-a-database-mail-account.md) per l'account del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent da usare.  
  
-   [Creare un profilo di Posta elettronica database](../../relational-databases/database-mail/create-a-database-mail-profile.md) per l'account del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent da usare e aggiungere l'utente a **DatabaseMailUserRole** nel database **msdb** .
  
-   Impostare il profilo come predefinito per il database **msdb** .  
  
###  <a name="security"></a><a name="Security"></a> Sicurezza  
  
####  <a name="permissions"></a><a name="Permissions"></a> Autorizzazioni  
 Per creare gli account dei profili ed eseguire le stored procedure è necessario che l'utente sia un membro del ruolo predefinito del server sysadmin.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Con SQL Server Management Studio  
 **Per configurare SQL Server Agent Mail per l'utilizzo di Posta elettronica database**  
  
-   In Esplora oggetti espandere un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Fare clic con il pulsante destro del mouse su **SQL Server Agent**, quindi scegliere **Proprietà**.  
  
-   Fare clic su **Sistema avvisi**.  
  
-   Selezionare **Attiva profilo di posta**.  
  
-   Nell'elenco **Sistema di posta elettronica** selezionare **Posta elettronica database**.  
  
-   Selezionare un profilo di posta elettronica per Posta elettronica database nell'elenco **Profilo posta**. 
  
-   Riavviare SQL Server Agent.  
  
##  <a name="follow-up-tasks"></a><a name="Follow_Up"></a> Attività di completamento  
 Le attività seguenti sono necessarie per completare la configurazione dell'agent per inviare avvisi e notifiche.  
  
-   [Avvisi](../../ssms/agent/alerts.md)  
  
     Gli avvisi possono essere configurati per segnalare a un operatore un evento di database o una condizione del sistema operativo.  
  
-   [Operatori](../../ssms/agent/operators.md)  
  
     Gli operatori solo alias di persone o gruppi che possono ricevere notifiche elettroniche  
  
  
