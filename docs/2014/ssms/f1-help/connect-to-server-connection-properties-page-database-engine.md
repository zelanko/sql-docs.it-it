---
title: Motore di database - Connetti al server (pagina Proprietà connessione) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql12.swb.connecttosqlserver.connectionproperties.f1
ms.assetid: edc1143c-6a47-4b02-92ab-441bdea8ea8a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 30382bcb0c70fb985c88866602cb997988b88569
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "70153749"
---
# <a name="connect-to-server-connection-properties-page-database-engine"></a>Motore di database - Connetti al server (pagina Proprietà connessione)
  Utilizzare questa scheda per visualizzare o specificare le opzioni per la connessione a un' [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] istanza di o [!INCLUDE[ssDE](../../includes/ssde-md.md)] alla registrazione di in **Server registrati**. **Connetti** e **Opzioni** vengono visualizzate in questa finestra di dialogo solo quando ci si connette a [!INCLUDE[ssDE](../../includes/ssde-md.md)]un'istanza del. **Test** e **Salva** vengono visualizzati solo in questa finestra di dialogo durante [!INCLUDE[ssDE](../../includes/ssde-md.md)]la registrazione.  
  
## <a name="options"></a>Opzioni  
 **Connettersi al database**  
 Selezionare dall'elenco un database al quale connettersi. Se si seleziona ** \<>predefinita **, si verrà connessi al database predefinito per il server. Se si seleziona ** \<Sfoglia server>**, è possibile esplorare il server per il database a cui connettersi.  
  
 Quando ci si connette a un'istanza [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] del motore di database [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]tramite, è necessario [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizzare l'autenticazione di e specificare un database nella scheda **Proprietà connessione** della finestra di dialogo **Connetti al server** . Assicurarsi di selezionare la casella di controllo **Crittografa connessione** .  
  
 Per impostazione predefinita, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] si connette al **master**. Se si specifica un database utente, si vedranno solo quel database e i relativi oggetti in Esplora oggetti. Se si esegue la connessione al **master**, sarà possibile vedere tutti i database. Per altre informazioni, vedere [Panoramica del database SQL di Azure](/azure/sql-database/sql-database-technical-overview).  
  
 **Protocollo di rete**  
 Consente di selezionare un protocollo dall'elenco. I protocolli client disponibili sono i protocolli configurati tramite Configurazione SQL Native Client in Gestione computer.  
  
 **Dimensioni del pacchetto di rete**  
 Immettere la dimensione dei pacchetti di rete che devono essere inviati. Il valore predefinito è 4096 byte.  
  
 **Timeout connessione**  
 Immettere il numero di secondi di attesa prima che venga stabilita una connessione prima del timeout. Il valore predefinito è 15 secondi.  
  
 **Timeout esecuzione**  
 Immettere il numero massimo di secondi di attesa del completamento dell'esecuzione di un'attività nel server. Il valore predefinito è zero secondi, che indica l'assenza di un timeout.  
  
 **Crittografia connessione**  
 Consente di forzare la crittografia della connessione.  
  
 **Usa colore personalizzato**  
 Selezionare questa opzione per specificare il colore di sfondo per la barra di stato in una finestra dell'editor di query del [!INCLUDE[ssDE](../../includes/ssde-md.md)] . Per specificare il colore, fare clic su **Seleziona**. Nella finestra di dialogo **Colore** selezionare un colore predefinito nella griglia **Colori di base** oppure fare clic su **Definisci colori personalizzati** per definire e usare un colore personalizzato.  
  
-   Quando si specifica un colore per una voce server nel riquadro **Esplora oggetti** , tale colore verrà usato quando si apre una finestra dell'editor di query. Per aprire una finestra dell'editor di query, fare clic con il pulsante destro del mouse sulla voce server e scegliere **Nuova query**. In alternativa, quando il riquadro **Esplora oggetti** è attivo e relativo a tale server, fare clic su **Nuova query** sulla barra degli strumenti.  
  
-   Quando si specifica un colore per una voce server nel riquadro **Server registrati** , tale colore verrà usato quando si apre una finestra dell'editor di query. Per aprire una finestra dell'editor di query, fare clic con il pulsante destro del mouse sulla voce server e scegliere **Nuova query**. In alternativa, quando il riquadro **Server registrati** è attivo e relativo a tale server, fare clic su **Nuova query** sulla barra degli strumenti.  
  
-   Quando si sceglie **Nuovo** dal menu **File** e si fa clic su **Query del Motore di database**, il colore specificato nella finestra di dialogo **Connetti al server** verrà applicato alla finestra dell'editor di query.  
  
 **Reimposta tutto**  
 Consente di sostituire i valori predefiniti a tutti i valori delle proprietà di connessione immessi manualmente.  
  
 **Connettere**  
 Consente di eseguire un tentativo di connessione con i valori elencati.  
  
 **Opzioni**  
 Fare clic su questo pulsante per modificare la finestra di dialogo e nascondere le opzioni aggiuntive per la connessione al server, ad esempio le opzioni per la memorizzazione della password.  
  
 **Test**  
 Durante la registrazione del [!INCLUDE[ssDE](../../includes/ssde-md.md)] in **Server registrati**, scegliere questa opzione per verificare la connessione.  
  
 **Salvare**  
 Consente di salvare le impostazioni in **Server registrati**.  
  
## <a name="see-also"></a>Vedere anche  
 [Proprietà connessione - finestra di dialogo](../../database-engine/connection-properties-dialog-box.md)  
  
  
