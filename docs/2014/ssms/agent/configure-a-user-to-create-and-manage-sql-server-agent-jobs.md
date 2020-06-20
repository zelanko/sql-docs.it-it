---
title: Configurare un utente per la creazione e la gestione di processi di SQL Server Agent | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, user configuration
- jobs [SQL Server Agent], user configuration
- SQLAgentUserRole database role
- proxy accounts [SQL Server Agent]
ms.assetid: 67897e3e-b7d0-43dd-a2e2-2840ec4dd1ef
author: stevestein
ms.author: sstein
ms.openlocfilehash: 83313389b3b872004fb23b0babdad19cfb5b8e7d
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "84995485"
---
# <a name="configure-a-user-to-create-and-manage-sql-server-agent-jobs"></a>Configure a User to Create and Manage SQL Server Agent Jobs
  In questo argomento viene descritto come configurare un utente per la creazione o l'esecuzione di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] processi di Agent.  
  
-   **Prima di iniziare**  [Sicurezza](#Security)  
  
-   **Per configurare un utente per la creazione e la gestione di processi di SQL Server Agent tramite**  [SQL Server Management Studio](#SSMS)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="security"></a><a name="Security"></a> Sicurezza  
 Per configurare un utente per la creazione o l'esecuzione di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] processi di Agent, è innanzitutto necessario aggiungere un account di accesso SQL Server esistente o un ruolo msdb a uno dei ruoli predefiniti del [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database di Agent seguenti nel database msdb: SQLAgentUserRole, SQLAgentReaderRole o SQLAgentOperatorRole.  
  
 Per impostazione predefinita, i membri di questi ruoli del database possono creare passaggi di processo personalizzati ed eseguirli con il proprio account. Per eseguire processi che includono altri tipi di passaggi, ad esempio pacchetti [!INCLUDE[ssIS](../../includes/ssis-md.md)] , questi utenti non amministrativi dovranno avere accesso a un account proxy. Tutti i membri del ruolo predefinito del server sysadmin dispongono dell'autorizzazione per la creazione, la modifica e l'eliminazione degli account proxy. Per altre informazioni sulle autorizzazioni associate con questi ruoli di database predefiniti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, vedere [Ruoli di database predefiniti di SQL Server Agent](sql-server-agent-fixed-database-roles.md).  
  
####  <a name="permissions"></a><a name="Permissions"></a> Autorizzazioni  
 Per informazioni dettagliate, vedere [Implementazione della sicurezza di SQL Server Agent](implement-sql-server-agent-security.md).  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMS"></a> Utilizzo di SQL Server Management Studio  
 **Per aggiungere un account di accesso SQL o un ruolo msdb a un ruolo predefinito del database di SQL Server Agent**  
  
1.  Espandere un server in **Esplora oggetti**.  
  
2.  Espandere **Sicurezza**e quindi **Account di accesso**.  
  
3.  Fare clic con il pulsante destro del mouse sull'account di accesso che si vuole aggiungere al ruolo predefinito del database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent e scegliere **Proprietà**.  
  
4.  Nella pagina **mapping utenti** della finestra di dialogo **Proprietà account di accesso** Selezionare la riga contenente `msdb` .  
  
5.  Nell'area **Appartenenza a ruoli del database per: msdb**selezionare il ruolo predefinito del database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
 **Per configurare un account proxy per la creazione e la gestione dei passaggi di processo di SQL Server Agent**  
  
1.  Espandere un server in **Esplora oggetti**.  
  
2.  Espandere **SQL Server Agent**.  
  
3.  Fare clic con il pulsante destro del mouse su **Proxy** e scegliere **Nuovo proxy**.  
  
4.  Nella pagina **Generale** della finestra **Nuovo account proxy** specificare il nome del proxy, il nome delle credenziali e la descrizione per il nuovo proxy. Si noti che prima di creare un proxy di SQL Server Agent, è necessario innanzitutto creare le credenziali. Per ulteriori informazioni sulla creazione di una credenziale, vedere [creare una](../../relational-databases/security/authentication-access/create-a-credential.md) credenziale e [creare credenziali &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-credential-transact-sql).  
  
5.  Selezionare i sottosistemi appropriati per il proxy.  
  
6.  Nella pagina **Entità** aggiungere o rimuovere account di accesso oppure ruoli per concedere o negare l'accesso all'account proxy.  
  
## <a name="see-also"></a>Vedere anche  
 [Implementazione della sicurezza di SQL Server Agent](implement-sql-server-agent-security.md)  
  
  
