---
title: Registrare un server connesso (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 07/28/2016
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.swb.registerserver.f1
helpviewer_keywords:
- Registered Servers [SQL Server], register connected servers
- connected server registrations [SQL Server]
ms.assetid: 77deb5f5-0f80-484f-8b8b-29afa67ec18f
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 24751639dcd0484bb31f1783ca936dddd3e9240c
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/16/2019
ms.locfileid: "68256306"
---
# <a name="register-a-connected-server-sql-server-management-studio"></a>Registrazione di un server connesso (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  Questo argomento descrive come registrare un server connesso in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS). Tramite la registrazione del server è possibile salvare le informazioni di connessione per i server ai quali si accede di frequente. È possibile registrare un server prima della connessione o durate la connessione da Esplora oggetti.  Per visualizzare i server registrati in SSMS, selezionare **Visualizza**\\**Server registrati** dal menu.
  
 **Contenuto dell'articolo**  
  
-   **Per registrare un server utilizzando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-register-a-connected-server"></a>Per registrare un server connesso  
  
In Esplora oggetti fare clic con il pulsante destro del mouse su un server al quale si è già connessi e quindi scegliere **Registra**.
  
**Nome server**  
In questo campo viene inserito per impostazione predefinita il nome del server a cui si è connessi.  Facoltativamente, è possibile digitare un altro nome server o sceglierne uno dall'elenco a discesa.

**Autenticazione**  
Per la connessione a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]sono disponibili due modalità di autenticazione. 

-    **Autenticazione di Windows**  
La modalità di autenticazione di Windows consente all'utente di utilizzare un account utente di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows per la connessione. 

-    **autenticazione di SQL Server**   
Quando un utente si connette con un nome di accesso e una password da una connessione di tipo non trusted, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esegue l'autenticazione verificando che sia impostato un account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e che la password specificata corrisponda a quella registrata in precedenza. Se non è stato impostato alcun account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , l'autenticazione non viene completata e viene segnalato un errore all'utente.

     > [!IMPORTANT]  
     > [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)] Per altre informazioni, vedere [Scegliere una modalità di autenticazione](../../relational-databases/security/choose-an-authentication-mode.md).  

     -    **User name**  
Consente di visualizzare il nome utente utilizzato dalla connessione corrente. Questa opzione di sola lettura è disponibile solo se si è scelto di utilizzare l'autenticazione di Windows per la connessione. Per modificare il **Nome utente**connettersi al computer come utente diverso. 

     -    **Account di accesso**  
Immettere l'account di accesso da utilizzare per la connessione. Questa opzione è disponibile solo se si è scelto di utilizzare l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per la connessione.  

     -    **Password**  
Immettere la password per l'account di accesso. Questa opzione può essere modificata solo se si è scelto di utilizzare l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per la connessione. 

     -    **Memorizza password**  
Selezionare questa opzione per crittografare e archiviare in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] la password immessa. Questa opzione viene visualizzata solo se si è scelto di utilizzare l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per la connessione.  

          > [!NOTE]  
          > Se la password è stata memorizzata e si vuole evitarne la memorizzazione in futuro, deselezionare questa casella di controllo e fare clic su **Salva**.  

**Nome server registrato**  
Nome che si desidera venga visualizzato nel componente Server registrati. Non è necessario che questo nome corrisponda a quello indicato nella casella **Nome server** .  
  
**Descrizione server registrato**  
Consente di immettere una descrizione facoltativa del server.  
  
**Test**  
Consente di testare la connessione al server selezionato in **Nome server**.  
  
**Salva**  
Fare clic su questo pulsante per salvare le impostazioni del server registrato. 

## <a name="see-also"></a>Vedere anche  
[Creazione di un nuovo server registrato (SQL Server Management Studio)](../../tools/sql-server-management-studio/create-a-new-registered-server-sql-server-management-studio.md)
  
  
