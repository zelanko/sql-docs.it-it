---
title: Connessione a Sybase ASE (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Connecting to Sybase ASE
ms.assetid: a45a2330-9175-4c9e-af38-ef920e350614
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: d9c76a33a650284fde21b28af3a61b197829ef98
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63298535"
---
# <a name="connecting-to-sybase-ase-sybasetosql"></a>Connessione a Sybase ASE (SybaseToSQL)
La migrazione dei database di Sybase Adaptive Server Enterprise (ASE) a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure, è necessario connettersi al Server adattivo che contiene i database che si desidera eseguire la migrazione. Quando ci si connette, SSMA Ottiene i metadati relativi a tutti i database nel Server adattivo e visualizza i metadati del database nel riquadro di esplorazione di metadati di Sybase. SSMA archivia le informazioni sui server di database, ma non archivia le password.  
  
La connessione ad ambiente del servizio App rimane attiva fino a quando non si chiude il progetto. Quando si riapre il progetto, è necessario riconnettersi all'ambiente del servizio App se si desidera che una connessione attiva al server.  
  
Metadati relativi al Server adattivo non viene aggiornato automaticamente. In alternativa, se si desidera aggiornare i metadati nel Visualizzatore metadati Sybase, è necessario aggiornare manualmente i metadati, come descritto nella sezione "Aggiornamento dei metadati di ASE Sybase" più avanti in questo argomento.  
  
## <a name="required-ase-permissions"></a>Autorizzazioni di ambiente del servizio App necessaria  
L'account utilizzato per connettersi all'ambiente del servizio app deve avere almeno **pubbliche** accesso al database master e a qualsiasi database di origine per eseguire la migrazione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure. Inoltre, per selezionare le autorizzazioni sulle tabelle cui vengono eseguita la migrazione, l'utente deve disporre delle autorizzazioni SELECT su tabelle di sistema seguenti:  
  
-   [source_db].dbo.sysobjects  
  
-   [source_db].dbo.syscolumns  
  
-   [source_db].dbo.sysusers  
  
-   [source_db].dbo.systypes  
  
-   [source_db].dbo.sysconstraints  
  
-   [source_db].dbo.syscomments  
  
-   [source_db].dbo.sysindexes  
  
-   [source_db].dbo.sysreferences  
  
-   master.dbo.sysdatabases  
  
## <a name="establishing-a-connection-to-ase"></a>Tentativo di stabilire una connessione all'ambiente del servizio App  
Quando ci si connette a un Server adattivo, SSMA legge i metadati del database nel server di database e quindi aggiunge i metadati del file di progetto. Questi metadati vengono utilizzati da SSMA durante la conversione di oggetti [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o la sintassi SQL Azure, e quando esegue la migrazione di dati a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure. È possibile esplorare i metadati nel riquadro di esplorazione di metadati Sybase e le proprietà di singoli oggetti di database.  
  
> [!IMPORTANT]  
> Prima di provare a connettersi al server di database, assicurarsi che il server di database è in esecuzione e può accettare connessioni.  
  
**Per connettersi a Sybase ASE**  
  
1.  Nel **File** dal menu **Connetti a Sybase**.  
  
    Se connesso in precedenza a Sybase, il nome del comando saranno **Riconnetti a Sybase**.  
  
2.  Nel **Provider** , selezionare uno qualsiasi dei provider installati nel computer per connettersi al server Sybase.  
  
3.  Nel **modalità** seleziona **modalità Standard** oppure **modalità avanzata**.  
  
    Usare la modalità standard per specificare il nome del server, porta, nome utente e password. Utilizzare modalità avanzata per fornire una stringa di connessione. Questa modalità viene in genere usata solo per la risoluzione dei problemi o l'utilizzo con il supporto tecnico.  
  
4.  Se si seleziona **modalità Standard**, specificare i valori seguenti:  
  
    1.  Nel **nome Server** casella, immettere o selezionare il nome o l'indirizzo IP del server di database.  
  
    2.  Se il server di database non è configurato per accettare le connessioni sull'impostazione predefinita la porta (5000), immettere il numero di porta che viene usato per le connessioni di Sybase nel **porta Server** casella.  
  
    3.  Nel **nome utente** immettere un account di Sybase che dispone delle autorizzazioni necessarie.  
  
    4.  Nel **Password** casella, immettere la password per il nome utente specificato.  
  
5.  Se si seleziona **modalità avanzata**, specificare una stringa di connessione nel **stringa di connessione** casella.  
  
    Esempi di stringhe di connessione diverse sono come segue:  
  
    1.  **Stringhe di connessione per il Provider OLE DB Sybase:**  
  
        Per Sybase ASE OLE DB 12,5, una stringa di connessione di esempio è il seguente:  
  
        `Server Name=sybserver;User ID=MyUserID;Password=MyP@$$word;Provider=Sybase.ASEOLEDBProvider;`  
  
        Per Sybase ASE OLE DB 15, una stringa di connessione di esempio è il seguente:  
  
        `Server=sybserver;User ID=MyUserID;Password=MyP@$$word;Provider= ASEOLEDB;Port=5000;`  
  
    2.  **Stringa di connessione del Provider ODBC Sybase:**  
  
        `Driver=Adaptive Server Enterprise;Server=sybserver;uid=MyUserID;pwd=MyP@$$word;Port=5000;`  
  
    3.  **Stringa di connessione per il Provider ADO.NET Sybase:**  
  
        `Server=sybserver;Port=5000;uid=MyUserID;pwd=MyP@$$word;`  
  
    Per altre informazioni, vedere [connettersi a Sybase &#40;SybaseToSQL&#41;](../../ssma/sybase/connect-to-sybase-sybasetosql.md).  
  
## <a name="reconnecting-to-sybase-ase"></a>La riconnessione a Sybase ASE  
La connessione al server di database rimane attiva fino a quando non si chiude il progetto. Quando si riapre il progetto, è necessario riconnettere se si desidera che una connessione attiva al Server adattivo. È possibile lavorare offline fino a quando non si desidera aggiornare i metadati, caricare gli oggetti di database in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure, ed eseguire la migrazione dei dati.  
  
## <a name="refreshing-sybase-ase-metadata"></a>Aggiornamento dei metadati di ASE Sybase  
I metadati sui database ambiente del servizio App non vengono aggiornati automaticamente. I metadati nel Visualizzatore metadati Sybase sono uno snapshot dei metadati quando si è connessi prima di tutto per il Server adattivo o l'ultima volta aggiornate manualmente i metadati. È possibile aggiornare manualmente i metadati per un singolo database, un unico schema di database o tutti i database.  
  
**Per aggiornare i metadati**  
  
1.  Assicurarsi di essere connessi al Server adattivo.  
  
2.  Nel Visualizzatore metadati Sybase, selezionare la casella di controllo accanto al database o schema di database che si desidera aggiornare.  
  
3.  I database o i singoli database o lo schema del database e quindi scegliere **aggiornare dal Database**.  
  
4.  Se viene chiesto di selezionare l'oggetto corrente, fare clic su **Sì**.  
  
## <a name="next-step"></a>Passaggio successivo  
  
-   Il passaggio successivo del processo di migrazione consiste [connettersi a un'istanza di SQL Server](connecting-to-sql-server-sybasetosql.md) / [ci si connette a un'istanza di SQL Azure](connecting-to-azure-sql-db-sybasetosql.md)  
  
## <a name="see-also"></a>Vedere anche  
[Migrazione dei database di Sybase ASE a SQL Server - Azure SQL database &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
