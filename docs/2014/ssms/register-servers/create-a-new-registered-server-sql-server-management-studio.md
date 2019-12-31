---
title: Creare un nuovo server registrato
ms.custom: seo-lt-2019
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql12.swb.registerserver.general.sqlce.f1
- sql12.swb.registerserver.general.sqlserver.f1
helpviewer_keywords:
- Registered Servers [SQL Server], creating new registered servers
ms.assetid: 716ea070-a3b5-4514-9de2-82ce8a96514b
author: markingmyname
ms.author: maghan
manager: jroth
ms.openlocfilehash: cce885929deff7484a4e068bf06ac3b39dbb3062
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/19/2019
ms.locfileid: "75244666"
---
# <a name="create-a-new-registered-server-sql-server-management-studio"></a>Creazione di un nuovo server registrato (SQL Server Management Studio)
  In questo argomento viene illustrato come salvare le informazioni di connessione per i server ai quali si accede di frequente, registrando il server nel componente Server registrati di [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. La registrazione di un server può essere eseguita prima della connessione o durante la connessione da Esplora oggetti. È disponibile un comando di menu speciale che consente di registrare le istanze del server nel computer locale.  
  
 Esistono due tipi di server registrati:  
  
-   Gruppi di server locali  
  
     Utilizzare i gruppi di server locale per stabilire facilmente connessioni ai server gestiti di frequente. Nel gruppo di server locali vengono registrati sia server locali che non locali. I gruppi di server locali sono univoci per ogni utente. Per informazioni su come condividere le informazioni sui server registrati, vedere [Esportare informazioni relative a server registrati &#40;SQL Server Management Studio&#41;](export-registered-server-information-sql-server-management-studio.md) e [Importare informazioni relative a server registrati &#40;SQL Server Management Studio&#41;](import-registered-server-information-sql-server-management-studio.md).  
  
    > [!NOTE]  
    >  Se possibile, si consiglia di utilizzare l'autenticazione di Windows.  
  
-   Server di gestione centrale  
  
     Le registrazioni dei server vengono archiviate in un server di gestione centrale anziché nel file system. I server di gestione centrale e i server registrati subordinati possono essere registrati solo utilizzando l'autenticazione di Windows. Dopo la registrazione di un server di gestione centrale, verranno automaticamente visualizzati i server registrati associati. Per altre informazioni sui server di gestione centrale, vedere [Amministrare più server tramite server di gestione centrale](../../relational-databases/administer-multiple-servers-using-central-management-servers.md). Le versioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] precedenti a [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] non possono essere designate come server di gestione centrale.  
  
##  <a name="SSMSProcedure"></a>Utilizzo di SQL Server Management Studio  
  
#### <a name="to-automatically-register-the-local-server-instances"></a>Per registrare automaticamente le istanze locali del server  
  
-   In Server registrati fare clic con il pulsante destro del mouse su un nodo dell'albero Server registrati e selezionare **Update Local Server Registration**(Aggiorna registrazione server locale).  
  
#### <a name="to-create-a-new-registered-server"></a>Per creare un nuovo server registrato  
  
1.  Se il componente Server registrati non è visibile in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], scegliere **Server registrati** dal menu **Visualizza**.  
  
     **Tipo di server**  
     Per la registrazione di un server da Server registrati, la casella **Tipo di server** è di sola lettura e corrisponde al tipo di server visualizzato nel riquadro Server registrati. Per registrare un tipo diverso di server, fare clic su **Motore di database**, **Analysis Server**, **Reporting Services**o **Integration Services** o sulla barra degli strumenti **Server registrati** prima di avviare la registrazione di un nuovo server.  
  
     **Nome server**  
     Selezionare l'istanza del server da registrare nel formato: * \<nomeserver>*[\\*\<NomeIstanza>*].  
  
     **Autenticazione**  
     Per la connessione a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]sono disponibili due modalità di autenticazione.  
  
     **Autenticazione di Windows**  
     La modalità di autenticazione di Windows consente all'utente di utilizzare un account utente di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows per la connessione.  
  
     **Autenticazione SQL Server**  
     Quando un utente si connette con un nome di accesso e una password da una connessione di tipo non trusted, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esegue l'autenticazione verificando che sia impostato un account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e che la password specificata corrisponda a quella registrata in precedenza. Se non è stato impostato alcun account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , l'autenticazione non viene completata e viene segnalato un errore all'utente.  
  
    > [!IMPORTANT]  
    >  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]Per altre informazioni, vedere [scegliere una modalità di autenticazione](../../relational-databases/security/choose-an-authentication-mode.md).  
  
     **Nome utente**  
     Consente di visualizzare il nome utente utilizzato dalla connessione corrente. Questa opzione di sola lettura è disponibile solo se si è scelto di utilizzare l'autenticazione di Windows per la connessione. Per modificare il **Nome utente**connettersi al computer come utente diverso.  
  
     **Accesso**  
     Immettere l'account di accesso da utilizzare per la connessione. Questa opzione è disponibile solo se si è scelto di utilizzare l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per la connessione.  
  
     **Password**  
     Immettere la password per l'account di accesso. Questa opzione può essere modificata solo se si è scelto di utilizzare l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per la connessione.  
  
     **Memorizza password**  
     Selezionare questa opzione per crittografare e archiviare in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] la password immessa. Questa opzione viene visualizzata solo se si è scelto di utilizzare l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per la connessione.  
  
    > [!NOTE]  
    >  Se la password è stata archiviata e si desidera arrestarne la memorizzazione, deselezionare questa casella di controllo e quindi fare clic su **Salva**.  
  
     **Nome server registrato**  
     Nome che si desidera venga visualizzato nel componente Server registrati. Non è necessario che questo nome corrisponda a quello indicato nella casella **Nome server** .  
  
     **Descrizione server registrato**  
     Consente di immettere una descrizione facoltativa del server.  
  
     **Test**  
     Consente di testare la connessione al server selezionato in **Nome server**.  
  
     **Salvare**  
     Fare clic su questo pulsante per salvare le impostazioni del server registrato.  
  
## <a name="multiserver-queries"></a>Query multiserver  
 La finestra Editor di query in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] consente di connettersi ed eseguire query su più istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contemporaneamente. I risultati restituiti dalla query possono essere uniti in un singolo riquadro dei risultati oppure possono essere inclusi in riquadri dei risultati distinti. L'editor di query può eventualmente includere colonne indicanti il nome del server che ha prodotto ciascuna riga e l'account di accesso utilizzato per la connessione a tale server. Per altre informazioni su come eseguire query multiserver, vedere [Eseguire simultanea di istruzioni su più server &#40;SQL Server Management Studio&#41;](execute-statements-against-multiple-servers-simultaneously.md).  
  
 Per eseguire query su tutti i server in un gruppo di server locali, fare clic con il pulsante destro del mouse sul gruppo di server, scegliere **Connetti** e fare clic su **Nuova query**. Quando le query vengono eseguite nella nuova finestra dell'editor di query, verranno eseguite su tutti i server del gruppo, utilizzando le informazioni di connessione archiviate, incluso il contesto di autenticazione dell'utente. I server registrati tramite l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ma che non salvano la password non riusciranno a connettersi.  
  
 Per eseguire query su tutti i server registrati con un server di gestione centrale, espandere il server di gestione centrale, fare clic con il pulsante destro del mouse sul gruppo di server, scegliere **Connetti**e fare clic su **Nuova query**. Quando le query vengono eseguite nella nuova finestra Editor query, verranno eseguite su tutti i server del gruppo, utilizzando le informazioni di connessione archiviate e il contesto di autenticazione di Windows dell'utente.  
  
## <a name="see-also"></a>Vedere anche  
 [Nascondi oggetti di sistema in Esplora oggetti](../object/hide-system-objects-in-object-explorer.md)   
 [Esporta informazioni server registrate &#40;SQL Server Management Studio&#41;](export-registered-server-information-sql-server-management-studio.md)   
 [Importa informazioni server registrate &#40;SQL Server Management Studio&#41;](import-registered-server-information-sql-server-management-studio.md)  
  
  
