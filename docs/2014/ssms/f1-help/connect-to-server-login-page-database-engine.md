---
title: Motore di database - Connetti al server (pagina Account di accesso) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql12.swb.connecttosqlserver.login.f1
ms.assetid: e08cfbc3-bed5-4401-a13b-1c66d902fe32
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2fe246a1f8baf1ab9f60ab1fa73e21e81c052aa1
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "70153697"
---
# <a name="connect-to-server-login-page-database-engine"></a>Motore di database - Connetti al server (pagina Account di accesso)
  Usare questa scheda per visualizzare o specificare le opzioni per la connessione al [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
> [!NOTE]  
>  Per connettersi con l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , è necessario che [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sia configurato in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e nella modalità di autenticazione di Windows. Per ulteriori informazioni su come determinare la modalità di autenticazione e per modificare la modalità di autenticazione, vedere Modifica della modalità di [autenticazione del server](../../database-engine/configure-windows/change-server-authentication-mode.md).  
  
## <a name="options"></a>Opzioni  
 **Tipo di server**  
 Per la registrazione di un server da Esplora oggetti, selezionare il tipo di server a cui connettersi, ovvero [!INCLUDE[ssDE](../../includes/ssde-md.md)], Analysis Services, Reporting Services o Integration Services. Nelle altre parti della finestra di dialogo vengono visualizzate solo le opzioni applicabili al tipo di server selezionato. Durante la registrazione di un server da Server registrati, la casella **Tipo server** è di sola lettura e corrisponde al tipo di server visualizzato nel componente Server registrati. Per registrare un tipo diverso di server, selezionare [!INCLUDE[ssDE](../../includes/ssde-md.md)], Analysis Services, Reporting Services o Integration Services nella barra degli strumenti Server registrati prima di avviare la registrazione di un nuovo server.  
  
 Quando si esegue una connessione a un'istanza del motore di database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tramite [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], è necessario usare l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e specificare un database nella scheda **Proprietà connessione** della finestra di dialogo **Connetti al server** . Assicurarsi di selezionare la casella di controllo **Crittografa connessione** .  
  
 Per impostazione predefinita, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] si connette al **master**. Se si specifica un database utente, si vedranno solo quel database e i relativi oggetti in Esplora oggetti. Se si esegue la connessione al **master**, sarà possibile vedere tutti i database. Per altre informazioni, vedere [Panoramica del database SQL di Azure](/azure/sql-database/sql-database-technical-overview).  
  
 **Nome server**  
 Consente di selezionare l'istanza del server a cui connettersi. Per impostazione predefinita verrà visualizzata l'ultima istanza del server a cui è stata effettuata la connessione.  
  
 **autenticazione**  
 Per la connessione a un'istanza di [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]sono disponibili due modalità di autenticazione.  
  
 Quando si esegue una connessione a un'istanza del motore di database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tramite [!INCLUDE[ssSDS](../../includes/sssds-md.md)], è necessario usare l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e specificare un database nella scheda **Proprietà connessione** della finestra di dialogo **Connetti al server** . Assicurarsi di selezionare la casella di controllo **Crittografa connessione** .  
  
 Per impostazione predefinita, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] si connette al **master**. Se si specifica un database utente, si vedranno solo quel database e i relativi oggetti in Esplora oggetti. Se si esegue la connessione al **master**, sarà possibile vedere tutti i database. Per altre informazioni, vedere [Panoramica del database SQL di Azure](/azure/sql-database/sql-database-technical-overview).  
  
 **Modalità di autenticazione di Windows (Autenticazione di Windows)**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Tale modalità consente di connettersi tramite un account utente di Windows.  
  
 **Autenticazione di SQL Server**  
 Quando un utente si connette con un nome account di accesso e una password specifici da una connessione non affidabile, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esegue l'autenticazione verificando che sia impostato un account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e che la password specificata corrisponda a quella registrata in precedenza. Se non è stato impostato alcun account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , l'autenticazione non viene completata e viene segnalato un errore all'utente.  
  
> [!IMPORTANT]  
>  Se possibile, usare l'autenticazione di Windows.  
  
 **Nome utente**  
 Immettere il nome utente da utilizzare per la connessione. Questa opzione è disponibile solo si è scelto di utilizzare l'autenticazione di Windows per la connessione.  
  
 **Accesso**  
 Immettere l'account di accesso da utilizzare per la connessione. Questa opzione è disponibile solo se si è scelto di utilizzare l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per la connessione.  
  
 **Password**  
 Immettere la password per l'account di accesso. Questa opzione è modificabile solo se si è scelto di utilizzare l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per la connessione.  
  
 **Memorizza password**  
 Selezionare questa opzione affinché [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] archivi la password immessa. Questa opzione viene visualizzata solo se si è scelto di utilizzare l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per la connessione.  
  
 **Connettere**  
 Fare clic su questo pulsante per connettersi al server selezionato.  
  
 **Opzioni**  
 Fare clic su questo pulsante per modificare la finestra di dialogo e nascondere le opzioni aggiuntive per la connessione al server, ad esempio le opzioni per la memorizzazione della password.  
  
  
