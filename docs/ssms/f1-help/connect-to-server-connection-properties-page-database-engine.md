---
title: Motore di database - Connetti al server (pagina Proprietà connessione) | Microsoft Docs
ms.custom: ''
ms.date: 08/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.swb.connecttoce.connectionproperties.f1
- sql13.swb.connecttosqlserver.connectionproperties.f1
ms.assetid: edc1143c-6a47-4b02-92ab-441bdea8ea8a
author: markingmyname
ms.author: maghan
manager: jroth
ms.openlocfilehash: f0ba80b069cbd24923c91f9761e98dcdb8f2febd
ms.sourcegitcommit: 5d839dc63a5abb65508dc498d0a95027d530afb6
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/09/2019
ms.locfileid: "67680312"
---
# <a name="connect-to-server-connection-properties-page-database-engine"></a>Motore di database - Connetti al server (pagina Proprietà connessione)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Usare questa scheda per visualizzare o specificare le opzioni per la connessione a un'istanza del [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)] o alla registrazione del [!INCLUDE[ssDE](../../includes/ssde_md.md)] in **Server registrati**. Le opzioni**Connetti** e **Opzioni** vengono visualizzate in questa finestra di dialogo solo durante la connessione a un'istanza del [!INCLUDE[ssDE](../../includes/ssde_md.md)]. Le opzioni**Test** e **Salva** vengono visualizzate in questa finestra di dialogo solamente durante la registrazione del [!INCLUDE[ssDE](../../includes/ssde_md.md)].  
  
**Connetti al database**  
Selezionare dall'elenco un database al quale connettersi. Se si seleziona **<default>** , viene stabilita la connessione al database predefinito del server. Se si seleziona **<Browse server>** , sarà possibile cercare il database a cui connettersi tra quelli disponibili nel server.  
  
Quando si esegue una connessione a un'istanza del motore di database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tramite [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], è necessario usare l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e specificare un database nella scheda **Proprietà connessione** della finestra di dialogo **Connetti al server** . Assicurarsi di selezionare la casella di controllo **Crittografa connessione** .  
  
Per impostazione predefinita, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] si connette al **master**. Quando si esegue la connessione a [!INCLUDE[ssSDS](../../includes/sssds-md.md)], se si specifica un database utente, si vedranno solo quel database e i relativi oggetti in Esplora oggetti. Se si esegue la connessione al **master**, si è in grado di vedere tutti i database. Per altre informazioni, vedere la [panoramica di database SQL di Microsoft Azure](/azure/sql-database/sql-database-technical-overview).  
  
**Protocollo di rete**  
Consente di selezionare un protocollo dall'elenco. I protocolli client disponibili sono i protocolli configurati tramite Configurazione di rete dei client in Gestione computer.  
  
**Dimensioni pacchetto di rete**  
Immettere la dimensione dei pacchetti di rete che devono essere inviati. Il valore predefinito è 4096 byte.  
  
**Timeout connessione**  
Immettere il numero di secondi di attesa dell'attivazione di una connessione prima del timeout. Il valore predefinito è 15 secondi.  
  
**Timeout esecuzione**  
Immettere il numero massimo di secondi di attesa del completamento dell'esecuzione di un'attività nel server. Il valore predefinito è zero secondi, che indica l'assenza di un timeout.  
  
**Crittografa connessione**  
Consente di forzare la crittografia della connessione.  
  
**Utilizza colore personalizzato**  
Selezionare questa opzione per specificare il colore di sfondo per la barra di stato in una finestra dell'editor di query del [!INCLUDE[ssDE](../../includes/ssde_md.md)] . Per specificare il colore, fare clic su **Seleziona**. Nella finestra di dialogo **Colore** selezionare un colore predefinito nella griglia **Colori di base** oppure fare clic su **Definisci colori personalizzati** per definire e usare un colore personalizzato.  
  
-   Quando si specifica un colore per una voce server nel riquadro **Esplora oggetti** , tale colore verrà usato quando si apre una finestra dell'editor di query. Per aprire una finestra dell'editor di query, fare clic con il pulsante destro del mouse sulla voce server e scegliere **Nuova query**. In alternativa, quando il riquadro **Esplora oggetti** è attivo e relativo a tale server, fare clic su **Nuova query** sulla barra degli strumenti.  
  
-   Quando si specifica un colore per una voce server nel riquadro **Server registrati** , tale colore verrà usato quando si apre una finestra dell'editor di query. Per aprire una finestra dell'editor di query, fare clic con il pulsante destro del mouse sulla voce server e scegliere **Nuova query**. In alternativa, quando il riquadro **Server registrati** è attivo e relativo a tale server, fare clic su **Nuova query** sulla barra degli strumenti.  
  
-   Quando si sceglie **Nuovo** dal menu **File** e si fa clic su **Query del Motore di database**, il colore specificato nella finestra di dialogo **Connetti al server** verrà applicato alla finestra dell'editor di query.  
  
**ID tenant o nome di dominio AD**  
Quando si esegue la connessione con l'autenticazione **Active Directory - Universale con MFA**, specificare il dominio che esegue l'autenticazione. Questa opzione è disponibile solo quando si usa SSMS 17.2 o versione successiva. 

**Reimposta tutto**  
Consente di sostituire i valori predefiniti a tutti i valori delle proprietà di connessione immessi manualmente.  
  
**Connect**  
Consente di eseguire un tentativo di connessione con i valori elencati.  
  
**Opzioni**  
Fare clic su questo pulsante per modificare la finestra di dialogo e nascondere le opzioni aggiuntive per la connessione al server, ad esempio le opzioni per la memorizzazione della password.  
  
**Test**  
Durante la registrazione del [!INCLUDE[ssDE](../../includes/ssde_md.md)] in **Server registrati**, scegliere questa opzione per verificare la connessione.  
  
**Salva**  
Salva le impostazioni in **Server registrati**.  
  
## <a name="see-also"></a>Vedere anche  
[Finestra di dialogo Proprietà connessione](../../ssms/f1-help/connection-properties-dialog-box.md)  
  
