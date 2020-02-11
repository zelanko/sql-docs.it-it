---
title: Connessione a SQL Server (AccessToSQL) | Microsoft Docs
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
ms.openlocfilehash: 4630ae8d92dbf0e9b1c5bf615dd82d436a5751f5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68006643"
---
# <a name="connecting-to-sql-server-accesstosql"></a>Connessione a SQL Server (AccessToSQL)
Per eseguire la migrazione dei [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]database di Access a, è necessario connettersi all' [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]istanza di destinazione di. Quando si esegue la connessione, SSMA ottiene i metadati relativi ai database nell'istanza [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di e Visualizza i metadati [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] del database in Esplora metadati. SSMA archivia informazioni sull'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a cui si è connessi, ma non archivia le password.  
  
La connessione a SQL Server rimane attiva fino a quando non si chiude il progetto. Quando si riapre il progetto, è necessario riconnettersi a SQL Server se si desidera una connessione attiva al server. È possibile lavorare offline fino a quando non si caricano oggetti di database in SQL Server e si migrano i dati.  
  
I metadati relativi all'istanza di SQL Server non vengono sincronizzati automaticamente. Per aggiornare i metadati in SQL Server Metadata Explorer, è invece necessario aggiornare manualmente i metadati del SQL Server. Per ulteriori informazioni, vedere la sezione "sincronizzazione dei metadati di SQL Server" più avanti in questo argomento.  
  
## <a name="required-sql-server-permissions"></a>Autorizzazioni SQL Server richieste  
L'account utilizzato per la connessione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] richiede autorizzazioni diverse a seconda delle azioni eseguite dall'account.  
  
-   Per convertire gli oggetti di [!INCLUDE[tsql](../../includes/tsql-md.md)] accesso in sintassi, per aggiornare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]i metadati da o per salvare la sintassi convertita in script, l'account deve disporre dell'autorizzazione per accedere [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]all'istanza di.  
  
-   Per caricare gli oggetti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database in e per eseguire [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]la migrazione dei dati a, il requisito di autorizzazione minimo è l'appartenenza al ruolo del database **db_owner** nel database di destinazione.  
  
## <a name="establishing-a-sql-server-connection"></a>Creazione di una connessione SQL Server  
Prima di convertire gli oggetti di database [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di Access nella sintassi, è necessario stabilire una connessione all' [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] istanza di in cui si desidera eseguire la migrazione dei database di Access.  
  
Quando si definiscono le proprietà di connessione, è inoltre necessario specificare il database in cui verrà eseguita la migrazione degli oggetti e dei dati. È possibile personalizzare questo mapping a livello di database di Access dopo la connessione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]a. Per ulteriori informazioni, vedere [mapping di database di origine e di destinazione](mapping-source-and-target-databases-accesstosql.md).  
  
> [!IMPORTANT]  
> Prima di connettersi a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], verificare che l'istanza di sia [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in esecuzione e che sia in grado di accettare le connessioni. Per ulteriori informazioni, vedere "connessione al [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] motore di database" nella [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] documentazione online di.  
  
**Per eseguire la connessione a SQL Server**  
  
1.  Scegliere **Connetti a SQL Server**dal menu **file** .  
  
    Se in precedenza si è [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]connessi a, il nome del comando verrà **riconnesso a SQL Server**.  
  
2.  Nella casella **nome server** immettere o selezionare il nome dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
    -   Se ci si connette all'istanza predefinita nel computer locale, è possibile immettere **localhost** o un punto (**.**).  
  
    -   Se ci si connette all'istanza predefinita in un altro computer, immettere il nome del computer.  
  
    -   Se ci si connette a un'istanza denominata, immettere il nome del computer, una barra rovesciata e il nome dell'istanza. Ad esempio: MyServer\MyInstance.  
  
    -   Per connettersi a un'istanza utente attiva di [!INCLUDE[ssExpress](../../includes/ssexpress_md.md)], connettersi utilizzando il protocollo Named Pipes e specificando il nome della pipe \\ \\, ad esempio .\pipe\sql\query. Per altre informazioni, vedere la documentazione di [!INCLUDE[ssExpress](../../includes/ssexpress_md.md)].  
  
3.  Se l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è configurata in modo da accettare connessioni su una porta non predefinita, immettere il numero di porta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizzato per le connessioni nella casella **porta server** . Per l'istanza predefinita di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], il numero di porta predefinito è 1433. Per le istanze denominate, SSMA proverà a ottenere il numero [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di porta dal servizio browser.  
  
4.  Nella casella **database** immettere il nome del database di destinazione per la migrazione di oggetti e dati.  
  
    Questa opzione non è disponibile quando si esegue la riconnessione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
    Il nome del database di destinazione non può contenere spazi o caratteri speciali. È ad esempio possibile eseguire la migrazione dei database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Access a un database denominato "ABC". Non è tuttavia possibile eseguire la migrazione dei [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database di Access a un database denominato "a b-c".  
  
    È possibile personalizzare questo mapping per ogni database dopo la connessione. Per ulteriori informazioni, vedere [mapping di database di origine e di destinazione](mapping-source-and-target-databases-accesstosql.md)  
  
5.  Nel menu a discesa **autenticazione** selezionare il tipo di autenticazione da utilizzare per la connessione. Per utilizzare l'account di Windows corrente, selezionare **autenticazione di Windows**. Per usare un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] account di accesso, selezionare **SQL Server autenticazione**e quindi specificare un nome utente e una password.  
  
6.  Per la connessione sicura vengono aggiunti due controlli, la casella di controllo **Crittografa connessione** e la casella di controllo **TrustServerCertificate** . È visibile solo quando è selezionata la casella di controllo **Crittografa connessione** **TrustServerCertificate** . Quando la **connessione Encrypt** è selezionata (true) e **TrustServerCertificate** è deselezionata (false), convaliderà il certificato SSL SQL Server. La convalida del certificato del server fa parte dell'handshake SSL e assicura che il server a cui si esegue la connessione sia quello corretto. Per garantire questo problema, è necessario installare un certificato sul lato client e sul lato server.  
  
7.  Fare clic su **Connetti**.  
  
**Compatibilità tra versioni superiore**  
  
È consentita la connessione/riconnessione a versioni successive di SQL Server.  
  
1.  Sarà possibile connettersi a SQL Server 2008 o SQL Server 2012 quando il progetto creato è SQL Server 2005.  
  
2.  Sarà possibile connettersi a SQL Server 2012 quando il progetto creato è SQL Server 2008, ma non è consentito connettersi a versioni inferiori, ad esempio SQL Server 2005.  
  
3.  Sarà possibile connettersi solo a SQL Server 2012 quando il progetto creato è SQL Server 2012.  
  
4.  La compatibilità con le versioni successive non è valida per SQL Azure.  
  
||||||||
|-|-|-|-|-|-|-|
|**TIPO di progetto rispetto alla versione del SERVER di destinazione**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2005 (versione: 9. x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2008 (versione: 10. x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2012 (versione: 11. x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2014 (versione: 12. x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2016 (versione: 13. x)|SQL Azure|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2005|Sì|Sì|Sì|Sì|Sì||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2008||Sì|Sì|Sì|Sì||
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2012|||Sì|Sì|Sì||
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2014||||Sì|Sì||
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016|||||Sì||
|SQL Azure||||||Sì|
  
> [!IMPORTANT]  
> La conversione degli oggetti di database viene eseguita in base al tipo di progetto, ma non in base alla versione della SQL Server connessa a. Nel caso di SQL Server progetto 2005, la conversione viene eseguita in base a SQL Server 2005 anche se si è connessi a una versione successiva di SQL Server (SQL Server 2008/SQL Server 2012/SQL Server 2014/SQL Server 2016).  
  
## <a name="synchronizing-sql-server-metadata"></a>Sincronizzazione di metadati di SQL Server  
Se [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gli schemi cambiano dopo la connessione, è possibile sincronizzare i metadati con il server.  
  
**Per sincronizzare i metadati di SQL Server**  
  
-   In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Esplora metadati fare clic con il pulsante destro del mouse su **database**, quindi scegliere **Sincronizza con database**.  
  
## <a name="reconnecting-to-sql-server"></a>Riconnessione a SQL Server  
La connessione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] rimane attiva fino a quando non si chiude il progetto. Quando si riapre il progetto, è necessario riconnettersi a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se si desidera una connessione attiva al server. È possibile lavorare offline fino a quando non si caricano oggetti di database in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e si migrano i dati.  
  
La procedura per la riconnessione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è identica alla procedura per stabilire una connessione.  
  
## <a name="next-steps"></a>Passaggi successivi  
Se si desidera personalizzare il mapping tra i database di origine e di destinazione, vedere [mapping di database di origine e di destinazione](mapping-source-and-target-databases-accesstosql.md) in caso contrario, il passaggio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] successivo consiste nel convertire gli oggetti di database nella sintassi utilizzando [Converti oggetti di database](converting-access-database-objects-accesstosql.md) .  
  
## <a name="see-also"></a>Vedere anche  
[Migrazione dei database di Access a SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
