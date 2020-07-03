---
title: Sicurezza relativa a DQS
ms.date: 10/01/2012
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 921927f5-1b1e-452a-a79e-c691829fd826
author: swinarko
ms.author: sawinark
ms.openlocfilehash: 55eb89febb9d4db79946a13b7d876d3391ab2516
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/02/2020
ms.locfileid: "85895359"
---
# <a name="dqs-security"></a>Sicurezza relativa a DQS

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sqlserver.md)]

  L'infrastruttura di sicurezza di [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) si basa sull'infrastruttura di sicurezza di SQL Server. Un amministratore del database concede a un utente un set di autorizzazioni associando l'utente a un ruolo DQS. Così facendo, si determinano le risorse DQS a cui l'utente ha accesso e le attività funzionali che è in grado di svolgere.  
  
## <a name="dqs-roles"></a>Ruoli DQS  
 Esistono quattro ruoli per DQS. Uno è il ruolo di amministratore del database (DBA) che gestisce principalmente l'installazione di prodotti, la manutenzione del database e la gestione degli utenti. Questo ruolo opera principalmente in SQL Server Management Studio, piuttosto che all'interno dell'applicazione [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] . Il relativo ruolo del server è sysadmin.  
  
 Gli altri ruoli sono Information Worker, amministratori dei dati che utilizzano direttamente il prodotto dall'applicazione [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] . Con questi ruoli è possibile effettuare le operazioni seguenti:  
  
-   L'utente **DQS Administrator** (ruolo dqs_administrator) può effettuare tutte le operazioni nell'ambito del prodotto. Può modificare ed eseguire un progetto, creare e modificare una Knowledge Base, interrompere un'attività, arrestare un processo all'interno di un'attività e modificare la configurazione e le impostazioni relative ai servizi dati di riferimento. Tuttavia, l'Amministratore DQS non può installare il server o aggiungere nuovi utenti. Tale attività deve essere svolta dall'amministratore del database.  
  
-   Il **DQS KB Editor** (ruolo dqs_kb_editor) può eseguire tutte le attività di DQS, ad eccezione di quelle amministrative. Il DQS DB Editor può modificare ed eseguire un progetto nonché creare e modificare una Knowledge Base. Può visualizzare i dati del monitoraggio delle attività, ma non interrompere o arrestare un'attività o eseguire attività amministrative.  
  
-   Il **DQS KB Operator** (ruolo dqs_kb_operator) può modificare ed eseguire un progetto. Non può eseguire qualsiasi altro tipo di gestione delle informazioni né creare o modificare una Knowledge Base. Può visualizzare i dati di monitoraggio delle attività, ma non interrompere o arrestare un'attività o eseguire attività amministrative.  
  
## <a name="user-management"></a>User Management  
 L'amministratore di database (DBA) crea gli utenti di DQS e li associa ai ruoli DQS in SQL Server Management Studio. Il DBA gestisce le autorizzazioni aggiungendo account di accesso SQL come utenti del database DQS_MAIN e associando ogni utente a uno dei ruoli DQS. A ogni ruolo vengono concesse autorizzazioni per un set di stored procedure nel database DQS_MAIN. I tre ruoli DQS non sono disponibili per i database DQS_PROJECTS e DQS_STAGING_DATA.  
  
## <a name="related-tasks"></a>Attività correlate  
  
|Descrizione dell'attività|Argomento|  
|----------------------|-----------|  
|Viene descritto come creare un utente e assegnare ruoli DQS utilizzando SQL Server Management Studio.|[Gestione di utenti DQS in SSMS](https://msdn.microsoft.com/library/955af01d-00da-4c51-9311-f3848749df54)|  
  
  
