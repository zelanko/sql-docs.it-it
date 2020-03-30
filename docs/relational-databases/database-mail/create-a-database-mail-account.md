---
title: Creare un account di Posta elettronica database | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- Database Mail [SQL Server], accounts
- accounts [Database Mail]
ms.assetid: c07abbc6-fc6a-470b-8fa3-532f2e06b16a
author: stevestein
ms.author: sstein
ms.openlocfilehash: 640a24917c1bcb8b7b707308693f658de8dd33e6
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "70211365"
---
# <a name="create-a-database-mail-account"></a>Creare un account di Posta elettronica database.
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  Per creare un account di Posta elettronica database, utilizzare la **Configurazione guidata Posta elettronica database** o [!INCLUDE[tsql](../../includes/tsql-md.md)] .  
  
-   **Prima di iniziare:**  [Prerequisiti](#Prerequisites)  
  
-   **Per creare un account di Posta elettronica database usando:**  [Configurazione guidata Posta elettronica database](#SSMSProcedure), [Transact-SQL](#TsqlProcedure)  
  
-   **Completamento:**  [Passaggi successivi per configurare Posta elettronica database](#FollowUp)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> Prerequisiti  
  
-   Determinare il nome del server e il numero di porta per il server SMTP (Simple Mail Transfer Protocol) utilizzato per inviare e-mail. Se il server SMTP richiede l'autenticazione, determinare il nome utente e la password per il server SMTP.  
  
-   Se lo si desidera, è possibile specificare il tipo e il numero di porta del server. Il tipo di server per la posta in uscita è sempre SMTP. La maggior parte dei server SMTP utilizza la porta predefinita, ovvero la 25.  
  
##  <a name="using-database-mail-configuration-wizard"></a><a name="SSMSProcedure"></a> Utilizzo della Configurazione guidata Posta elettronica database  
 **Per creare un account di Posta elettronica database utilizzando una procedura guidata**  
  
-   In Esplora oggetti, connettersi all'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] su cui si desidera configurare Posta elettronica database ed espandere l'albero di server.  
  
-   Espandere il nodo **Gestione**  
  
-   Fare doppio clic su Posta elettronica database per aprire la Configurazione guidata Posta elettronica database.  
  
-   Nella pagina **Selezione attività di configurazione** selezionare l'opzione **Gestisci account e profili di Posta elettronica database**e fare clic su **Avanti**.  
  
-   Nella pagina **Gestione profili e account** selezionare l'opzione **Crea un nuovo account** e fare clic su **Avanti**.  
  
-   Nella pagina **Nuovo account** , specificare il nome dell'account, la descrizione, informazione sul server di posta elettronica e tipo di autenticazione. Scegliere **Avanti**  
  
-   Per completare la creazione del nuovo account, rivedere le azioni da eseguire nella pagina **Completamento procedura guidata** quindi fare clic su **Fine** .  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Uso di Transact-SQL  
 **Per creare un account di Posta elettronica database utilizzando Transact-SQL**  
  
 Eseguire la stored procedure **msdb.dbo.sysmail_add_account_sp** per creare l'account, specificando le seguenti informazioni:  
  
-   Nome dell'account da creare.  
  
-   Descrizione dell'account (facoltativa).  
  
-   Indirizzo di posta elettronica visualizzato nei messaggi in uscita.  
  
-   Nome visualizzato nei messaggi in uscita.  
  
-   Nome del server SMTP.  
  
-   Nome utente da utilizzare per l'accesso se il server SMTP richiede l'autenticazione.  
  
-   Password da utilizzare per l'accesso se il server SMTP richiede l'autenticazione.  
  
 Nell'esempio seguente viene creato un nuovo account di Posta elettronica database.  
  
```  
EXECUTE msdb.dbo.sysmail_add_account_sp  
    @account_name = 'AdventureWorks Administrator',  
    @description = 'Mail account for administrative e-mail.',  
    @email_address = 'dba@Adventure-Works.com',  
    @display_name = 'AdventureWorks Automated Mailer',  
    @mailserver_name = 'smtp.Adventure-Works.com' ;  
```  
  
##  <a name="follow-up-next-steps-to-configuring-the-database-mail"></a><a name="FollowUp"></a> Completamento: Passaggi successivi per configurare Posta elettronica database  
  
-   [Creare un profilo di Posta elettronica database](../../relational-databases/database-mail/create-a-database-mail-profile.md)  
  
  
