---
title: Installazione di componenti SSMA in SQL Server (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Installign the Extension Pack
- SQL Server Database Objects
ms.assetid: 33070e5f-4e39-4b70-ae81-b8af6e4983c5
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 2041901a851ca755b1079535ccbf763472ec7bc4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63055671"
---
# <a name="installing-ssma-components-on-sql-server-oracletosql"></a>Installazione di componenti SSMA in SQL Server (OracleToSQL)
Oltre a installare SSMA, è necessario installare anche i componenti nel computer che esegue [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Questi componenti includono il pacchetto di estensioni SSMA, che supporta la migrazione dei dati e i provider Oracle per abilitare la connettività server-to-server.  
  
## <a name="ssma-for-oracle-extension-pack"></a>SSMA per Oracle Extension Pack  
Il pacchetto di estensione SSMA consente di aggiungere i database **sysdb** e **ssmatesterdb**, per l'istanza specificata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Il database **sysdb** contiene le tabelle e stored procedure necessarie per la migrazione dei dati e le funzioni definite dall'utente che emulano le funzioni di sistema Oracle. Il **ssmatesterdb** database contiene tabelle e delle procedure necessarie per il componente di Tester.  
  
Inoltre, quando si esegue la migrazione dei dati per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], crea SSMA [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent i processi quando il modulo di migrazione dei dati lato server viene usato per la migrazione dei dati.  
  
### <a name="prerequisites"></a>Prerequisiti  
Prima di installare SSMA per componenti server Oracle in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], assicurarsi che il sistema soddisfi i requisiti seguenti:  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è installata l'istanza. SSMA non supporta SQL Server 2008 Express Edition.  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows Installer 3.1 o versione successiva.  
  
-   Il Provider del Client Oracle o il provider OLE DB per Oracle e la connettività al database Oracle che vuoi eseguire la migrazione. È possibile installare i provider dal supporto del prodotto Oracle o sito Web Oracle.  
  
-   Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] servizio Browser deve essere eseguito durante l'installazione. Viene utilizzato per popolare un elenco delle istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nell'installazione guidata. È possibile disabilitare il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] servizio Browser dopo l'installazione.  
  
    > [!NOTE]  
    > Se il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] servizio Browser è in esecuzione, ma ancora non è presente un elenco di istanze nel programma di installazione, è necessario sbloccare la porta UDP 1434. È possibile usare Windows Firewall per temporaneamente sbloccare la porta oppure è possibile disabilitare temporaneamente Windows Firewall. Potrebbe anche essere necessario disabilitare temporaneamente il software antivirus. Assicurarsi di abilitare i firewall e software antivirus dopo l'installazione.  
  
### <a name="installing-the-extension-pack"></a>Installare il pacchetto di estensione  
È possibile installare qualsiasi momento prima della migrazione dei dati per il pacchetto di estensione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
> Per installare il pacchetto di estensione, è necessario essere un membro del **sysadmin** ruolo del server nell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
**Per installare il pacchetto di estensione**  
  
1.  Se non è già stato fatto, estrarre tutti i file dal file Zip SSMA.  
  
    A seconda della versione di WinZip si dispone, è possibile fare doppio clic sul file, oppure fare doppio clic su file e selezionare **Estrai tutto** oppure **aperto in WinZip**. Seguire le istruzioni nell'interfaccia utente WinZip per estrarre i file.  
  
2.  Copiare SSMA per Oracle Extension Pack. *n*. Install.exe, dove *n* è il numero di build, al computer in cui è in esecuzione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
3.  Fare doppio clic su SSMA per Oracle Extension Pack. *n*. Install.exe.  
  
4.  Nella pagina di benvenuto, fare clic su **successivo**.  
  
5.  Nella pagina Contratto di licenza leggere il contratto di licenza. Se si accetta, selezionare la **accetto i termini del contratto di licenza** casella di controllo e quindi fare clic su **successivo**.  
  
6.  Nella pagina Selezione tipo di installazione, fare clic su **tipica**.  
  
7.  Nella pagina pronto per installare, fare clic su **installare**.  
  
8.  Nella pagina il primo passaggio dell'installazione di completato, fare clic su **successivo**.  
  
    Verrà visualizzata una nuova finestra di dialogo, in cui si seleziona l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per l'installazione del pacchetto di estensione.  
  
9. Selezionare l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in cui faranno la migrazione di schemi Oracle e quindi fare clic **successivo**.  
  
    L'istanza predefinita ha lo stesso nome del computer. Le istanze denominate saranno seguite da una barra rovesciata e il nome dell'istanza.  
  
10. Nella pagina connessione selezionare il metodo di autenticazione e quindi fare clic su **successivo**.  
  
    L'autenticazione di Windows userà le credenziali di Windows per tentare di accedere all'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se si seleziona [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] l'autenticazione, è necessario immettere un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nome account di accesso e la password.  
  
11. Nella pagina successiva, selezionare **installare Database Utilities** *n*, dove *n* è il numero di versione e quindi fare clic su **Avanti**.  
  
    Il **sysdb** database viene creato e le funzioni definite dall'utente e stored procedure vengono create in tale database.  
  
    Se **installare Database Tester** sia selezionata l'opzione il tester **ssmatesterdb** database verrà creato.  
  
12. Per installare le utilità in un'altra istanza del [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], selezionare **Yes**, quindi fare clic su **successivo**. Per uscire dalla procedura guidata, fare clic **No**.  
  
13. In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o tramite l'utilità sqlcmd, eseguire lo script seguente per abilitare CLR:  
  
    ```  
    sp_configure 'clr enabled', 1  
    GO  
    RECONFIGURE  
    GO  
    ```  
    Se CLR non è abilitato, si riceverà l'errore seguente quando si connette SSMA a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
    SSMA non è stato possibile recuperare le informazioni sulla versione di assembly di pacchetto di estensione. Reinstallare il pacchetto di estensione nel server di database.  
  
### <a name="sql-server-database-objects"></a>Oggetti di Database SQL Server  
Dopo aver installato il pacchetto di estensione, sarà possibile vedere un **ssma_oracle.bcp_migration_packages** tabella, un **ssma_oracle.db_storage** tabella e un **ssma_oracle.db_error_list** tabella di **sysdb** database. Si noterà anche molte stored procedure e funzioni definite dall'utente nel **ssma_oracle** dello schema.  
  
Ogni volta che si esegue la migrazione dei dati per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], SSMA consente di creare un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] processo dell'agente. Questi processi sono denominati **pacchetto di migrazione dati ssma_oracle {GUID}** e sono visibili nel [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nodo dell'agente di [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] nella cartella processi.  
  
## <a name="see-also"></a>Vedere anche  
[Installazione di SSMA per Oracle Client &#40;OracleToSQL&#41;](../../ssma/oracle/installing-ssma-for-oracle-client-oracletosql.md)  
[La migrazione da Oracle database in SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
