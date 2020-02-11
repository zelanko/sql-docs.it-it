---
title: Abilitare le connessioni crittografate al motore di database (Gestione configurazione SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- connections [SQL Server], encrypted
- SSL [SQL Server]
- Secure Sockets Layer (SSL)
- encryption [SQL Server], connections
- cryptography [SQL Server], connections
- certificates [SQL Server], installing
- requesting encrypted connections
- installing certificates
- security [SQL Server], encryption
ms.assetid: e1e55519-97ec-4404-81ef-881da3b42006
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: a872057f354b289d65a6a3a730e3a63afd7af0d4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62782315"
---
# <a name="enable-encrypted-connections-to-the-database-engine-sql-server-configuration-manager"></a>Abilitazione di connessioni crittografate al Motore di database (Gestione configurazione SQL Server)
  In questo argomento viene descritto come abilitare connessioni crittografate per un'istanza del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] specificando un certificato per il [!INCLUDE[ssDE](../../includes/ssde-md.md)] tramite Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . È necessario che sia disponibile un certificato per il computer server e che il computer client sia impostato per considerare attendibile l'autorità radice del certificato. Il processo di provisioning consiste nell'installazione di un certificato tramite l'importazione in Windows.  
  
 Il certificato deve essere emesso per **l'autenticazione server**. Il nome del certificato deve essere il nome di dominio completo (FQDN) del computer.  
  
 I certificati per gli utenti vengono archiviati nel computer locale. Per installare un certificato utilizzato da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è necessario eseguire Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con lo stesso account utente del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , a meno che il servizio sia in esecuzione con l'account LocalSystem, NetworkService o LocalService e sia pertanto consentito utilizzare un account amministrativo.  
  
 Il client deve essere in grado di verificare la proprietà del certificato utilizzato dal server. Se il client dispone del certificato chiave pubblica dell'autorità di certificazione che ha firmato il certificato del server, non sono necessarie ulteriori operazioni di configurazione. 
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows sono inclusi i certificati chiave pubblica di numerose autorità di certificazione. Se il certificato del server è stato firmato da un'autorità di certificazione pubblica o privata per la quale il client non dispone del certificato chiave pubblica, è necessario installare il certificato chiave pubblica dell'autorità di certificazione che ha firmato il certificato del server.  
  
> [!NOTE]  
>  Per utilizzare la crittografia in un cluster di failover, è necessario installare il certificato server con il nome DNS completo del server virtuale in tutti i nodi del cluster di failover. Ad esempio, se si dispone di un cluster a due nodi, con nodi denominati test1. la società>. com e test2. * \< * l'azienda>. com e si dispone di un server virtuale denominato Virtsql, è necessario installare un certificato per virtsql. * \< * l'azienda>. com in entrambi i nodi. * \< * È possibile impostare il valore dell'opzione **ForceEncryption**su **Sì**.  
  
 **Contenuto dell'articolo**  
  
-   **Per abilitare connessioni crittografate:**  
  
     [Eseguire il provisioning di (installare) un certificato nel server](#Provision)  
  
     [Esportare il certificato del server](#Export)  
  
     [Configurare il server in modo che accetti connessioni crittografate](#ConfigureServerConnections)  
  
     [Configurare il client in modo che richieda connessioni crittografate](#ConfigureClientConnections)  
  
     [Crittografare una connessione da SQL Server Management Studio](#EncryptConnection)  
  
##  <a name="SSMSProcedure"></a>  
  
###  <a name="Provision"></a>Per eseguire il provisioning (installare) un certificato nel server  
  
1.  Dal menu **Start** fare clic su **Esegui**, quindi nella casella **Apri** digitare `MMC` e fare clic su **OK**.  
  
2.  Nella console MMC scegliere **Aggiungi/Rimuovi snap-in** dal menu **File**.  
  
3.  Nella finestra di dialogo **Aggiungi/Rimuovi snap-in** fare clic su **Aggiungi**.  
  
4.  Nella finestra di dialogo **Aggiungi snap-in autonomo** fare clic su **Certificati**e quindi su **Aggiungi**.  
  
5.  Nella finestra **di dialogo snap-in certificati** fare clic su **account computer**, quindi fare clic su **fine**.  
  
6.  Nella finestra **di dialogo Aggiungi snap-in autonomo** fare clic su **Chiudi.**  
  
7.  Nella finestra di dialogo **Aggiungi/Rimuovi snap-in** fare clic su **OK**.  
  
8.  Nello snap-in **Certificati** espandere **Certificati**e **Personale**, fare clic con il pulsante destro del mouse su **Certificati**, scegliere **Tutte le attività**e quindi fare clic su **Importa**.  
  
9. Completare l' **Importazione guidata certificati**per aggiungere un certificato al computer e chiudere la console MMC. Per ulteriori informazioni sull'aggiunta di un certificato a un computer, vedere la documentazione di Windows.  
  
###  <a name="Export"></a>Per esportare il certificato del server  
  
1.  Nello snap-in **Certificati** individuare il certificato nella cartella **Certificati** / **Personale** , fare clic con il pulsante destro del mouse su **Certificato**, scegliere **Tutte le attività**e quindi fare clic su **Esporta**.  
  
2.  Completare l' **Esportazione guidata certificati**e archiviare il file di certificato in una posizione appropriata.  
  
###  <a name="ConfigureServerConnections"></a>Per configurare il server in modo che accetti connessioni crittografate  
  
1.  In **Gestione configurazione SQL Server** espandere **Configurazione di rete SQL Server**, fare clic con il pulsante destro del mouse su **Protocolli per** _\<istanza server>_ e quindi scegliere **Proprietà**.  
  
2.  Nella finestra di dialogo **protocolli per**_\<nome istanza>_ **Proprietà** , nella scheda **certificato** , selezionare il certificato desiderato dall'elenco a discesa per la casella **certificato** , quindi fare clic su **OK**.  
  
3.  Nella casella **ForceEncryption** della scheda **Flag** selezionare **Sì**e quindi fare clic su **OK** per chiudere la finestra di dialogo.  
  
4.  Riavviare il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
###  <a name="ConfigureClientConnections"></a>Per configurare il client in modo che richieda connessioni crittografate  
  
1.  Copiare il certificato originale o il file di certificato esportato nel computer client.  
  
2.  Nel computer client usare lo snap-in **Certificati** per installare il certificato radice o il file di certificato esportato.  
  
3.  Nel riquadro della console fare clic con il pulsante destro del mouse su **Configurazione SQL Server Native Client**e quindi scegliere **Proprietà**.  
  
4.  Nella casella **Imponi crittografia protocolli** della pagina **Flag** fare clic su **Sì**.  
  
###  <a name="EncryptConnection"></a>Per crittografare una connessione da SQL Server Management Studio  
  
1.  Nella barra degli strumenti di Esplora oggetti fare clic su **Connetti**e quindi su **Motore di database**.  
  
2.  Nella finestra di dialogo **Connetti al server** completare le informazioni di connessione e quindi fare clic su **Opzioni**.  
  
3.  Nella scheda **Proprietà connessione** fare clic su **Crittografa connessione**.  
  
  
