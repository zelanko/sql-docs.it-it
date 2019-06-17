---
title: La connessione a SQL Server (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- authentication
- instance of SQL Server
- metadata, refreshing
- ports
- refreshing metadata
- spaces in database names
- special characters
- SQL Server
- SQL Server, connecting
- SQL Server, connecting to
- SQL Server, reconnecting
ms.assetid: f84cf007-ddf1-4396-a07c-3e0729abc769
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 0bedb8ba74d7965df34a102fb0d53a0cbdb248dc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63139023"
---
# <a name="connecting-to-sql-server-accesstosql"></a>La connessione a SQL Server (AccessToSQL)
Per migrare i database di Access [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è necessario connettersi all'istanza di destinazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Quando ci si connette, SSMA Ottiene i metadati relativi ai database nell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e visualizza i metadati di database in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Visualizzatore metadati. SSMA archivia le informazioni su quale istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che si è connessi a, ma non archivia le password.  
  
La connessione a SQL Server rimane attiva fino a quando non si chiude il progetto. Quando si riapre il progetto, è necessario riconnettersi a SQL Server se si desidera che una connessione attiva al server. È possibile lavorare offline finché non si caricare gli oggetti di database in SQL Server e la migrazione dei dati.  
  
I metadati sull'istanza di SQL Server non viene sincronizzato automaticamente. In alternativa, per aggiornare i metadati nel Visualizzatore metadati di SQL Server, è necessario aggiornare manualmente i metadati di SQL Server. Per altre informazioni, vedere la sezione "Come sincronizzare Metadata di SQL Server" più avanti in questo argomento.  
  
## <a name="required-sql-server-permissions"></a>Autorizzazioni necessarie di SQL Server  
L'account utilizzato per connettersi a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] richiede autorizzazioni diverse a seconda delle azioni eseguite da quell'account.  
  
-   Per accedere agli oggetti per convertire [!INCLUDE[tsql](../../includes/tsql-md.md)] sintassi, per aggiornare i metadati dal [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o per salvare sintassi convertita in script, l'account deve disporre dell'autorizzazione per accedere all'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Per caricare gli oggetti di database in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ed eseguire la migrazione dei dati a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], il requisito di autorizzazione minima necessaria è l'appartenenza al **db_owner** ruolo del database nel database di destinazione.  
  
## <a name="establishing-a-sql-server-connection"></a>Tentativo di stabilire una connessione a SQL Server  
Prima di convertire oggetti di database di Access da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] informazioni sulla sintassi, è necessario stabilire una connessione all'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in cui si vuole eseguire la migrazione di database di Access.  
  
Quando si definiscono le proprietà di connessione, è inoltre possibile specificare il database in cui verranno migrati dati e oggetti. È possibile personalizzare il mapping a livello di database l'accesso dopo la connessione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per altre informazioni, vedere [Mapping di database di origine e destinazione](mapping-source-and-target-databases-accesstosql.md).  
  
> [!IMPORTANT]  
> Prima di connettersi al [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], assicurarsi che l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è in esecuzione e può accettare connessioni. Per altre informazioni, vedere "ci si connette per la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] motore di Database" in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] documentazione Online di.  
  
**Per connettersi a SQL Server**  
  
1.  Nel **File** dal menu **Connetti al Server SQL**.  
  
    Se precedentemente connesso al [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], il nome del comando sarà **Riconnetti a SQL Server**.  
  
2.  Nel **nome Server** casella, immettere o selezionare il nome dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
    -   Se ci si connette all'istanza predefinita nel computer locale, è possibile immettere **localhost** o un punto ( **.** ).  
  
    -   Se ci si connette all'istanza predefinita in un altro computer, immettere il nome del computer.  
  
    -   Se ci si connette a un'istanza denominata, immettere il nome del computer, una barra rovesciata e il nome dell'istanza. Ad esempio: MyServer\MyInstance.  
  
    -   Per connettersi a un'istanza utente attiva di [!INCLUDE[ssExpress](../../includes/ssexpress_md.md)], connettersi tramite named pipe protocollo e specificando il nome della pipe, ad esempio \\ \\.\pipe\sql\query. Per altre informazioni, vedere il [!INCLUDE[ssExpress](../../includes/ssexpress_md.md)] documentazione.  
  
3.  Se l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è configurato per accettare le connessioni su una porta non predefinito, immettere il numero di porta usato per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] connessioni nel **porta Server** casella. Per l'istanza predefinita di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], il numero di porta predefinito è 1433. Per le istanze denominate, SSMA tenterà di ottenere il numero di porta dal [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] servizio Browser.  
  
4.  Nel **Database** casella, immettere il nome del database di destinazione per la migrazione di oggetti e dati.  
  
    Questa opzione non è disponibile durante la riconnessione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
    Il nome di database di destinazione non può contenere spazi o caratteri speciali. Ad esempio, è possibile migrare i database di Access un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database denominato "abc". Ma non è possibile migrare i database di Access un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database denominato "a b a c".  
  
    È possibile personalizzare questo mapping per ogni database dopo la connessione. Per altre informazioni, vedere [Mapping di origine e i database di destinazione](mapping-source-and-target-databases-accesstosql.md)  
  
5.  Nel **autenticazione** -menu a discesa, seleziona il tipo di autenticazione da usare per la connessione. Per usare l'account di Windows corrente, selezionare **Windows autenticazione**. Usare un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] account di accesso, selezionare **autenticazione di SQL Server**e quindi specificare un nome utente e password.  
  
6.  Per la connessione sicura, vengono aggiunti due controlli, **Encrypt Connection** casella di controllo e **TrustServerCertificate** casella di controllo. Solo quando **Encrypt Connection** sia selezionata la casella di controllo **TrustServerCertificate** casella di controllo è visibile. Quando **Encrypt Connection** è checked(true) e **TrustServerCertificate** è unchecked(false), convaliderà il certificato SSL di SQL Server. La convalida del certificato del server fa parte dell'handshake SSL e assicura che il server a cui si esegue la connessione sia quello corretto. A tale scopo, è necessario installare un certificato sul lato client, nonché sul lato server.  
  
7.  Fare clic su **Connetti**.  
  
**Compatibilità di versione superiore**  
  
È consentito connettersi o riconnettersi alle versioni successive di SQL Server.  
  
1.  Sarà in grado di connettersi a SQL Server 2008 o SQL Server 2012, quando il progetto creato è SQL Server 2005.  
  
2.  Sarà in grado di connettersi a SQL Server 2012, quando il progetto creato è SQL Server 2008, ma non è consentito per la connessione a versioni precedenti, ad esempio SQL Server 2005.  
  
3.  Sarà in grado di connettersi a SQL Server 2012 solo quando il progetto creato è SQL Server 2012.  
  
4.  Compatibilità di versione superiore non è valida per SQL Azure.  
  
||||||||
|-|-|-|-|-|-|-|
|**VERSIONE SERVER di destinazione e tipo di progetto**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 (versione: 9.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008 (versione: 10.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012 (Version:11.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014 (Version:12.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 (Version:13.x)|SQL Azure|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005|Yes|Yes|Yes|Yes|Yes||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008||Yes|Yes|Yes|Yes||
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012|||Yes|Yes|Yes||
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014||||Yes|Yes||
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016|||||Yes||
|SQL Azure||||||Yes|
  
> [!IMPORTANT]  
> Conversione degli oggetti di database viene eseguita in base al tipo di progetto, ma non in base alla versione di SQL Server connesso a. In caso di progetto di SQL Server 2005, la conversione viene eseguita in base a SQL Server 2005 anche se si è connessi a una versione successiva di SQL Server (SQL Server 2008 o SQL Server 2012 o SQL Server 2014/SQL Server 2016).  
  
## <a name="synchronizing-sql-server-metadata"></a>La sincronizzazione dei metadati del Server SQL  
Se [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] schemi modificare dopo essersi connessi, è possibile sincronizzare i metadati con il server.  
  
**Per sincronizzare i metadati di SQL Server**  
  
-   In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Visualizzatore metadati, fare clic a destra **database**, quindi selezionare **Sincronizza con Database**.  
  
## <a name="reconnecting-to-sql-server"></a>Connettersi a SQL Server  
La connessione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] rimane attiva fino a quando non si chiude il progetto. Quando si riapre il progetto, è necessario riconnettersi alla [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se si desidera che una connessione attiva al server. È possibile lavorare offline fino a quando non si caricano gli oggetti di database in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ed eseguire la migrazione dei dati.  
  
La procedura per la riconnessione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è quello utilizzato per la procedura per stabilire una connessione.  
  
## <a name="next-steps"></a>Passaggi successivi  
Se si desidera personalizzare il mapping tra i database di origine e di destinazione, vedere [Mapping di origine e i database di destinazione](mapping-source-and-target-databases-accesstosql.md) in caso contrario, il passaggio successivo consiste nel convertire gli oggetti di database a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando la sintassi [convertire oggetti di database](converting-access-database-objects-accesstosql.md)  
  
## <a name="see-also"></a>Vedere anche  
[Migrazione dei database di Access a SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
