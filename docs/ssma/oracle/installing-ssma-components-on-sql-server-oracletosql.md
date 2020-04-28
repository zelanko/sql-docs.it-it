---
title: Installazione dei componenti di SSMA in SQL Server (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 10/01/2019
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Installign the Extension Pack
- SQL Server Database Objects
ms.assetid: 33070e5f-4e39-4b70-ae81-b8af6e4983c5
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: 1f0cea859e9465eebefebc061ee51107dc7844aa
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "71713316"
---
# <a name="installing-ssma-components-on-sql-server-oracletosql"></a>Installazione dei componenti di SSMA in SQL Server (OracleToSQL)

Oltre a installare SSMA, è necessario installare anche i componenti nel computer in cui è in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]esecuzione. Questi componenti includono il pacchetto di estensioni SSMA, che supporta la migrazione dei dati e i provider Oracle per abilitare la connettività tra server.  
  
## <a name="ssma-for-oracle-extension-pack"></a>SSMA per Oracle Extension Pack

Il pacchetto di estensione SSMA aggiunge i database **sysdb** e **ssmatesterdb** all'istanza specificata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Il **sysdb** del database contiene le tabelle e le stored procedure necessarie per eseguire la migrazione dei dati e le funzioni definite dall'utente che emulano le funzioni di sistema Oracle. Il database **ssmatesterdb** contiene le tabelle e le procedure richieste dal componente tester.  
  
Inoltre, quando si esegue la migrazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]dei dati a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , SSMA crea processi di Agent quando viene utilizzato il motore di migrazione dei dati sul lato server per la migrazione dei dati.  
  
### <a name="prerequisites"></a>Prerequisiti

Prima di installare i componenti di SSMA per Oracle server [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]in, verificare che il sistema soddisfi i requisiti seguenti:  
  
- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]è installata l'istanza di. SSMA non supporta SQL Server 2008 Express Edition.
  
- [!INCLUDE[msCoName](../../includes/msconame_md.md)]Windows Installer 3,1 o versione successiva.  
  
- Il provider client Oracle o il provider di OLE DB per Oracle e la connettività al database Oracle di cui si desidera eseguire la migrazione. È possibile installare i provider dal supporto del prodotto Oracle o dal sito Web Oracle.  
  
- Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] servizio browser deve essere in esecuzione durante l'installazione. Viene utilizzato per popolare un elenco delle istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nell'installazione guidata di. È possibile disabilitare il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] servizio browser dopo l'installazione.  
  
    > [!NOTE]  
    > Se il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] servizio browser è in esecuzione, ma non viene ancora visualizzato un elenco di istanze nel programma di installazione, è necessario sbloccare la porta UDP 1434. È possibile utilizzare Windows Firewall per sbloccare temporaneamente la porta oppure è possibile disabilitare temporaneamente Windows Firewall. Potrebbe anche essere necessario disabilitare temporaneamente il software antivirus. Assicurarsi di abilitare i firewall e il software antivirus dopo l'installazione.  
  
### <a name="installing-the-extension-pack"></a>Installazione del pacchetto di estensione

È possibile installare il pacchetto di estensione in qualsiasi momento prima di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]eseguire la migrazione dei dati a.  
  
> [!IMPORTANT]  
> Per installare il pacchetto di estensione, è necessario essere un membro del ruolo del server **sysadmin** nell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
**Per installare il pacchetto di estensione**
  
1. Se non è già stato fatto, estrarre tutti i file dal file zip SSMA.  
  
    A seconda della versione di WinZip disponibile, è possibile fare doppio clic sul file oppure fare clic con il pulsante destro del mouse sul file, quindi scegliere **Estrai tutto** o **Apri in WinZip**. Per estrarre i file, seguire le istruzioni disponibili nell'interfaccia utente di WinZip.  
  
2. Copiare **SSMA per Oracle Extension Pack.* n*. Installare. exe** (dove *n* è il numero di Build) per il computer in cui [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]è in esecuzione.  
  
3. Fare doppio clic su **SSMA per Oracle Extension Pack.* n*. Installare. exe**.  
  
4. Nella pagina di **benvenuto** selezionare **Avanti**.  
  
5. Nella pagina **contratto di licenza con l'utente finale** leggere il contratto di licenza. Se si accetta, selezionare la casella di controllo Accetto **i termini del contratto di licenza** e quindi fare clic su **Avanti**.  
  
6. Nella pagina Selezione **tipo di installazione** selezionare **tipico**.  
  
7. Nella pagina **Inizio installazione** fare clic su **Installa**.  
  
8. Nella pagina **completamento del primo passaggio dell'installazione** fare clic su **Avanti**.  
  
    Verrà visualizzata una nuova finestra di dialogo in cui è possibile selezionare l'istanza [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di per l'installazione del pacchetto di estensione.  
  
9. Selezionare l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a cui si eseguirà la migrazione degli schemi Oracle e quindi fare clic su **Avanti**.  
  
    L'istanza predefinita ha lo stesso nome del computer. Le istanze denominate saranno seguite da una barra rovesciata e dal nome dell'istanza.  
  
10. Nella pagina connessione selezionare il metodo di autenticazione e quindi fare clic su **Avanti**.  
  
    L'autenticazione di Windows utilizzerà le credenziali di Windows per tentare di accedere all'istanza [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]di. Se si seleziona [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] l'autenticazione di, è necessario [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] immettere un nome di account di accesso e una password.  
  
11. Nella pagina successiva selezionare **Install Utilities database** *n*, dove *n* è il numero di versione e quindi fare clic su **Next (avanti**).  
  
    Viene creato il database **sysdb** e vengono create le stored procedure e le funzioni definite dall'utente in tale database.  
  
    Se l'opzione **Installa database tester** è selezionata, verrà creato il database **ssmatesterdb** del tester.  
  
12. Per installare le utilità in un'altra istanza [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]di, selezionare **Sì**, quindi selezionare **Avanti**oppure fare clic su **No**per uscire dalla procedura guidata.  
  
13. In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o tramite l'utilità sqlcmd eseguire lo script seguente per abilitare CLR:  
  
    ```
    sp_configure 'clr enabled', 1  
    GO  
    RECONFIGURE  
    GO  
    ```

    Se CLR non è abilitato, si riceverà l'errore seguente quando SSMA si [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]connette a:  
  
    SSMA non è riuscito a recuperare le informazioni sulla versione dell'assembly del pacchetto di estensione. Reinstallare il pacchetto di estensione nel server di database.  
  
### <a name="sql-server-database-objects"></a>Oggetti di database SQL Server  

Dopo aver installato il pacchetto di estensione, viene visualizzata una tabella **ssma_oracle. bcp_migration_packages** nel database **sysdb** .

Ogni volta che si esegue la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]migrazione dei dati in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , SSMA crea un processo di Agent. Questi processi sono denominati **ssma_oracle pacchetto di migrazione dei dati {GUID}** e sono [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] visibili nel nodo [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] Agent di nella cartella Jobs.  
  
## <a name="see-also"></a>Vedere anche

[Installazione di SSMA per il client Oracle &#40;OracleToSQL&#41;](../../ssma/oracle/installing-ssma-for-oracle-client-oracletosql.md)  
[Migrazione di database Oracle a SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
