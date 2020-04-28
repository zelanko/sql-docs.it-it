---
title: Connessione a SQL Server (MySQLToSQL) | Microsoft Docs
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
ms.openlocfilehash: 0ec33e462f1b68d70a86a0fbf4f7cf0214d25770
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "68103136"
---
# <a name="connecting-to-sql-server-mysqltosql"></a>Connessione a SQL Server (MySQLToSQL)
Per eseguire la migrazione dei database MySQL in SQL Server, è necessario connettersi all'istanza di destinazione di SQL Server. Quando si esegue la connessione, SSMA ottiene i metadati relativi a tutti i database nell'istanza di SQL Server e Visualizza i metadati del database in Esplora metadati SQL Server. SSMA archivia le informazioni dell'istanza di SQL Server si è connessi a, ma non archivia le password.  
  
La connessione a SQL Server rimane attiva fino a quando non si chiude il progetto. Quando si riapre il progetto, è necessario riconnettersi a SQL Server se si desidera una connessione attiva al server. È possibile lavorare offline fino a quando non si caricano oggetti di database in SQL Server e si migrano i dati.  
  
I metadati relativi all'istanza di SQL Server non vengono sincronizzati automaticamente. Per aggiornare i metadati in SQL Server Metadata Explorer, è invece necessario aggiornare manualmente i metadati del SQL Server. Per ulteriori informazioni, vedere la sezione "sincronizzazione dei metadati di SQL Server" più avanti in questo argomento.  
  
## <a name="required-sql-server-permissions"></a>Autorizzazioni SQL Server richieste  
L'account utilizzato per connettersi a SQL Server richiede autorizzazioni diverse a seconda delle azioni eseguite dall'account:  
  
-   Per convertire gli oggetti MySQL [!INCLUDE[tsql](../../includes/tsql-md.md)] in sintassi, per aggiornare i metadati da SQL Server o per salvare la sintassi convertita in script, l'account deve disporre dell'autorizzazione per accedere all'istanza di SQL Server.  
  
-   Per caricare gli oggetti di database in SQL Server, il requisito di autorizzazione minimo è l'appartenenza al ruolo del database **db_owner** nel database di destinazione.  
  
## <a name="establishing-a-sql-server-connection"></a>Creazione di una connessione SQL Server  
Prima di convertire gli oggetti di database MySQL in SQL Server sintassi, è necessario stabilire una connessione all'istanza di SQL Server in cui si vuole eseguire la migrazione del database o dei database MySQL.  
  
Quando si definiscono le proprietà di connessione, è inoltre necessario specificare il database in cui verrà eseguita la migrazione degli oggetti e dei dati. È possibile personalizzare questo mapping a livello di schema MySQL dopo la connessione a SQL Server. Per altre informazioni, vedere [mapping di database MySQL a schemi SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-databases-to-sql-server-schemas-mysqltosql.md)  
  
> [!IMPORTANT]  
> Prima di provare a connettersi a SQL Server, assicurarsi che l'istanza di SQL Server sia in esecuzione e che sia in grado di accettare le connessioni.  
  
**Per eseguire la connessione a SQL Server**  
  
1.  Scegliere **Connetti a SQL Server** dal menu **file** . questa opzione è abilitata dopo la creazione di un progetto.  
  
    Se in precedenza si è connessi a SQL Server, il nome del comando verrà **riconnesso SQL Server**.  
  
2.  Nella finestra di dialogo connessione immettere o selezionare il nome dell'istanza di SQL Server.  
  
    -   Se ci si connette all'istanza predefinita nel computer locale, è possibile immettere **localhost** o un punto (**.**).  
  
    -   Se ci si connette all'istanza predefinita in un altro computer, immettere il nome del computer.  
  
    -   Se ci si connette a un'istanza denominata in un altro computer, immettere il nome del computer seguito da una barra rovesciata e quindi dal nome dell'istanza, ad esempio MyServer\MyInstance.  
  
3.  Se l'istanza di SQL Server è configurata in modo da accettare connessioni su una porta non predefinita, immettere il numero di porta utilizzato per SQL Server le connessioni nella casella **porta server** . Per l'istanza predefinita di SQL Server, il numero di porta predefinito è 1433. Per le istanze denominate, SSMA proverà a ottenere il numero di porta dal servizio SQL Server Browser.  
  
4.  Nella casella **autenticazione** selezionare il tipo di autenticazione da utilizzare per la connessione. Per utilizzare l'account di Windows corrente, selezionare **autenticazione di Windows**. Per usare un account di accesso SQL Server, selezionare SQL Server autenticazione e quindi specificare il nome e la password dell'account di accesso.  
  
5.  Per una connessione protetta vengono aggiunti due controlli, ovvero le caselle di controllo **Encrypt connection** e **TrustServerCertificate** . La casella di controllo **TrustServerCertificate** è visibile solo quando è selezionata l'opzione **Crittografa connessione** . Quando si seleziona la casella di controllo **Crittografa connessione** (true) e **TrustServerCertificate** è deselezionata (false), verrà convalidato il certificato SSL SQL Server. La convalida del certificato del server fa parte dell'handshake SSL e assicura che il server a cui si esegue la connessione sia quello corretto. Per garantire questo problema, è necessario installare un certificato sul lato client e sul lato server.  
  
6.  Fare clic su Connetti.  
  
**Compatibilità tra versioni superiore**  
  
È consentita la connessione/riconnessione a versioni successive di SQL Server.  
  
1.  Quando il progetto creato [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005, sarà possibile connettersi a 2008 o 2012 o 2014 o 2016.  
  
2.  Sarà [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] possibile connettersi a 2012 o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014 o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 quando il progetto creato è [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008, ma non è consentito connettersi a versioni inferiori, ad esempio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005.  
  
3.  Sarà possibile [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] connettersi a 2012 o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014 o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 quando il progetto creato è [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012.  
  
4.  Sarà possibile connettersi solo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a 2014 o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 quando il progetto creato è [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014.  
  
5.  La compatibilità con le versioni successive non è valida per "SQL Azure".  
  
||||||||  
|-|-|-|-|-|-|-|  
|**TIPO di progetto rispetto alla versione del SERVER di destinazione**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005<br /> (Versione: 9. x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008<br /> (Versione: 10. x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012<br />(Versione: 11. x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2014<br />(Versione: 12. x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016<br />(Versione: 13. x)|SQL Azure|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005|Sì|Sì|Sì|Sì|Sì||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008||Sì|Sì|Sì|Sì||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012|||Sì|Sì|Sì||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2014||||Sì|Sì||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2016|||||Sì||  
|SQL Azure||||||Sì|  
  
> [!IMPORTANT]  
> La conversione degli oggetti di database viene eseguita in base al tipo di progetto, ma non in base alla versione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di connessa a. Nel caso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] un progetto 2005, la conversione viene eseguita in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] base a 2005 anche se si è connessi a una versione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] successiva di (SQL Server 2008/SQL Server 2012/SQL Server 2014/SQL Server 2016).  
  
## <a name="synchronizing-sql-server-metadata"></a>Sincronizzazione di metadati di SQL Server  
I metadati relativi ai database SQL Server non vengono aggiornati automaticamente. I metadati in SQL Server Esplora metadati sono uno snapshot dei metadati quando si è connessi per la prima volta a SQL Server o all'ultima volta che sono stati aggiornati manualmente i metadati. È possibile aggiornare manualmente i metadati per tutti i database o per qualsiasi singolo database o oggetto di database.  
  
**Per sincronizzare i metadati**  
  
1.  Assicurarsi di essere connessi a SQL Server.  
  
2.  In SQL Server Esplora metadati, selezionare la casella di controllo accanto allo schema del database o del database che si desidera aggiornare.  
  
    Ad esempio, per aggiornare i metadati per tutti i database, selezionare la casella accanto a database.  
  
3.  Fare clic con il pulsante destro del mouse su database o sul database singolo o sullo schema del database, quindi scegliere **Sincronizza con database**.  
  
## <a name="next-step"></a>passaggio successivo  
Il passaggio successivo della migrazione dipende dalle esigenze del progetto:  
  
-   Per personalizzare il mapping tra gli schemi di MySQL e SQL Server database e schemi, vedere [mapping di database MySQL a SQL Server schemi &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-databases-to-sql-server-schemas-mysqltosql.md)  
  
-   Per personalizzare le opzioni di configurazione per i progetti, vedere [impostazione delle opzioni del progetto &#40;MySQLToSQL&#41;](../../ssma/mysql/setting-project-options-mysqltosql.md)  
  
-   Per personalizzare il mapping dei tipi di dati di origine e di destinazione, vedere [mapping di tipi di dati MySQL e SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-and-sql-server-data-types-mysqltosql.md)  
  
-   Se non è necessario eseguire alcuna di queste attività, è possibile convertire le definizioni degli oggetti di database MySQL in SQL Server definizioni degli oggetti. Per altre informazioni, vedere [conversione di database MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/converting-mysql-databases-mysqltosql.md)  
  
## <a name="see-also"></a>Vedere anche  
[Migrazione di database MySQL a SQL Server-database SQL di Azure &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
