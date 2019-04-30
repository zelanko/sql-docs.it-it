---
title: La connessione a SQL Server (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- connecting to SQL Server 2008, SQL Server permission
- connecting to SQL Server 2008, synchronization
ms.assetid: 08233267-693e-46e6-9ca3-3a3dfd3d2be7
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 64dd3fae9776c09f81571a721aa53753e34fbb17
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63273505"
---
# <a name="connecting-to-sql-server-mysqltosql"></a>Connessione a SQL Server (MySQLToSQL)
Per eseguire la migrazione di database MySQL a SQL Server, è necessario connettersi all'istanza di destinazione di SQL Server. Quando ci si connette, SSMA Ottiene i metadati relativi a tutti i database nell'istanza di SQL Server e visualizza i metadati del database in Esplora i metadati di SQL Server. SSMA archivia le informazioni dell'istanza di SQL Server si è connessi a, ma non archiviano le password.  
  
La connessione a SQL Server rimane attiva fino a quando non si chiude il progetto. Quando si riapre il progetto, è necessario riconnettersi a SQL Server se si desidera che una connessione attiva al server. È possibile lavorare offline finché non si caricare gli oggetti di database in SQL Server e la migrazione dei dati.  
  
I metadati sull'istanza di SQL Server non viene sincronizzato automaticamente. In alternativa, per aggiornare i metadati nel Visualizzatore metadati di SQL Server, è necessario aggiornare manualmente i metadati di SQL Server. Per altre informazioni, vedere la sezione "Come sincronizzare Metadata di SQL Server" più avanti in questo argomento.  
  
## <a name="required-sql-server-permissions"></a>Autorizzazioni necessarie di SQL Server  
L'account utilizzato per connettersi a SQL Server richiede autorizzazioni diverse a seconda di operazioni eseguite con l'account:  
  
-   Per convertire gli oggetti di MySQL per [!INCLUDE[tsql](../../includes/tsql-md.md)] sintassi, per aggiornare i metadati da SQL Server o per convertire la sintassi per salvare gli script, l'account deve disporre dell'autorizzazione per accedere all'istanza di SQL Server.  
  
-   Per caricare gli oggetti di database in SQL Server, il requisito di autorizzazione minima necessaria è l'appartenenza di **db_owner** ruolo del database nel database di destinazione.  
  
## <a name="establishing-a-sql-server-connection"></a>Tentativo di stabilire una connessione a SQL Server  
Prima di convertire gli oggetti di database MySQL in sintassi SQL Server, è necessario stabilire una connessione all'istanza di SQL Server in cui si desidera migrare i database MySQL.  
  
Quando si definiscono le proprietà di connessione, è inoltre possibile specificare il database in cui verranno migrati dati e oggetti. È possibile personalizzare il mapping a livello di schema MySQL dopo la connessione a SQL Server. Per altre informazioni, vedere [Mapping di database MySQL a schemi SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-databases-to-sql-server-schemas-mysqltosql.md)  
  
> [!IMPORTANT]  
> Prima di provare a connettersi a SQL Server, assicurarsi che l'istanza di SQL Server è in esecuzione e può accettare connessioni.  
  
**Per connettersi a SQL Server**  
  
1.  Nel **File** dal menu **Connetti al Server SQL** (dopo la creazione di un progetto, questa opzione è abilitata).  
  
    Se in precedenza, si è connessi a SQL Server, il nome del comando saranno **Riconnetti a SQL Server**.  
  
2.  Nella finestra di dialogo di connessione, immettere o selezionare il nome dell'istanza di SQL Server.  
  
    -   Se ci si connette all'istanza predefinita nel computer locale, è possibile immettere **localhost** o un punto (**.**).  
  
    -   Se ci si connette all'istanza predefinita in un altro computer, immettere il nome del computer.  
  
    -   Se ci si connette a un'istanza denominata in un altro computer, immettere il nome del computer seguito da una barra rovesciata e quindi il nome dell'istanza, ad esempio MyServer\MyInstance.  
  
3.  Se l'istanza di SQL Server è configurato per accettare le connessioni su una porta non predefinito, immettere il numero di porta che viene usato per le connessioni di SQL Server nel **porta Server** casella. Per l'istanza predefinita di SQL Server, il numero di porta predefinito è 1433. Per le istanze denominate, SSMA tenterà di ottenere il numero di porta del servizio SQL Server Browser.  
  
4.  Nel **autenticazione** , selezionare il tipo di autenticazione da usare per la connessione. Per usare l'account di Windows corrente, selezionare **Windows autenticazione**. Per usare un account di accesso di SQL Server, selezionare autenticazione di SQL Server e quindi specificare il nome di accesso e password.  
  
5.  Per la connessione sicura, vengono aggiunti due controlli, il **Encrypt Connection** e **TrustServerCertificate** caselle di controllo. Solo quando **Encrypt Connection** è selezionata, il **TrustServerCertificate** casella di controllo è visibile. Quando **Encrypt Connection** è selezionata (true) e **TrustServerCertificate** è deselezionato (false), convaliderà il certificato SSL di SQL Server. La convalida del certificato del server fa parte dell'handshake SSL e assicura che il server a cui si esegue la connessione sia quello corretto. A tale scopo, è necessario installare un certificato sul lato client, nonché sul lato server.  
  
6.  Fare clic su Connetti.  
  
**Compatibilità di versione superiore**  
  
È consentito connettersi o riconnettersi alle versioni successive di SQL Server.  
  
1.  Sarà in grado di connettersi al [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008 oppure [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012 oppure [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014 o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 quando viene creato il progetto [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005.  
  
2.  Sarà in grado di connettersi al [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012 o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014 o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 quando viene creato il progetto [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008 ma non è consentito per la connessione a versioni precedenti, ovvero [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005.  
  
3.  Sarà in grado di connettersi al [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012 o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014 o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 quando viene creato il progetto [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012.  
  
4.  Sarà in grado di connettersi solo a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014 oppure [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 quando viene creato il progetto [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014.  
  
5.  Compatibilità di versione superiore non è valida per "SQL Azure".  
  
||||||||  
|-|-|-|-|-|-|-|  
|**VERSIONE SERVER di destinazione e tipo di progetto**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005<br /> (Versione: 9.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008<br /> (Versione: 10.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012<br />(Version:11.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014<br />(Version:12.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016<br />(Version:13.x)|SQL Azure|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005|Yes|Yes|Yes|Yes|Yes||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008||Yes|Yes|Yes|Yes||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012|||Yes|Yes|Yes||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2014||||Yes|Yes||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2016|||||Yes||  
|SQL Azure||||||Yes|  
  
> [!IMPORTANT]  
> Conversione degli oggetti di database viene eseguita in base al tipo di progetto, ma non in base alla versione del [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] connesso a. In caso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] progetto 2005, la conversione viene eseguita come descritto [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anche se si è connessi a una versione successiva del 2005 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SQL Server 2008 o SQL Server 2012 o SQL Server 2014/SQL Server 2016).  
  
## <a name="synchronizing-sql-server-metadata"></a>La sincronizzazione dei metadati del Server SQL  
I metadati relativi a database di SQL Server non viene aggiornato automaticamente. I metadati nel Visualizzatore metadati di SQL Server sono uno snapshot dei metadati quando si è connessa a SQL Server o l'ultima volta che si manualmente i metadati aggiornati. È possibile aggiornare manualmente i metadati per tutti i database o per qualsiasi database singolo o un oggetto di database.  
  
**Per sincronizzare i metadati**  
  
1.  Assicurarsi di essere connessi a SQL Server.  
  
2.  In Esplora i metadati di SQL Server, selezionare la casella di controllo accanto al database o schema di database che si desidera aggiornare.  
  
    Ad esempio, per aggiornare i metadati per tutti i database, selezionare la casella accanto al database.  
  
3.  I database, o i singoli database o lo schema del database e quindi scegliere **Sincronizza con Database**.  
  
## <a name="next-step"></a>Passaggio successivo  
Il passaggio successivo nel processo di migrazione dipende dalle esigenze del progetto:  
  
-   Per personalizzare il mapping tra gli schemi di MySQL e database di SQL Server e gli schemi, vedere [i database MySQL di Mapping a schemi SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-databases-to-sql-server-schemas-mysqltosql.md)  
  
-   Per personalizzare le opzioni di configurazione per i progetti, vedere [impostazione delle opzioni progetto &#40;MySQLToSQL&#41;](../../ssma/mysql/setting-project-options-mysqltosql.md)  
  
-   Per personalizzare il mapping dei tipi di dati di origine e di destinazione, vedere [Mapping di MySQL e SQL Server Data Types &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-and-sql-server-data-types-mysqltosql.md)  
  
-   Se non è necessario eseguire nessuna di queste attività, è possibile convertire le definizioni degli oggetti di database MySQL in definizioni di oggetti di SQL Server. Per altre informazioni, vedere [conversione di database MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/converting-mysql-databases-mysqltosql.md)  
  
## <a name="see-also"></a>Vedere anche  
[Database di migrazione da MySQL a SQL Server - Azure SQL database &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
