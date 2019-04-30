---
title: La connessione a SQL Server (DB2eToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: b59803cb-3cc6-41cc-8553-faf90851410e
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 26410a933c7432189f664c2b04d2b41e3e31c9c2
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63298988"
---
# <a name="connecting-to-sql-server-db2etosql"></a>La connessione a SQL Server (DB2eToSQL)
Per eseguire la migrazione di database DB2 a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2014 o Azure SQL DB è necessario connettersi a uno qualsiasi di queste istanze di destinazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Quando ci si connette, SSMA Ottiene i metadati relativi a tutti i database nell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e visualizza i metadati di database nel [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Visualizzatore metadati. SSMA archivia le informazioni su quale istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] si è connessi a, ma non archivia le password.  
  
La connessione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] rimane attiva fino a quando non si chiude il progetto. Quando si riapre il progetto, è necessario riconnettersi alla [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se si desidera che una connessione attiva al server. È possibile lavorare offline fino a quando non si caricano gli oggetti di database in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ed eseguire la migrazione dei dati.  
  
I metadati sull'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non viene sincronizzato automaticamente. In alternativa, per aggiornare i metadati nel [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Visualizzatore metadati, è necessario aggiornare manualmente il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] metadati. Per altre informazioni, vedere la "sincronizzazione in corso [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] metadati" più avanti in questo argomento.  
  
## <a name="required-sql-server-permissions"></a>Autorizzazioni necessarie di SQL Server  
L'account utilizzato per connettersi a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] richiede autorizzazioni diverse a seconda di operazioni eseguite con l'account:  
  
-   Per convertire oggetti DB2 [!INCLUDE[tsql](../../includes/tsql-md.md)] sintassi, per aggiornare i metadati dal [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o per salvare sintassi convertita in script, l'account deve disporre dell'autorizzazione per accedere all'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Per caricare gli oggetti di database in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], l'account deve essere un membro del **sysadmin** ruolo del server. Ciò è necessario installare gli assembly CLR.  
  
-   Per eseguire la migrazione dei dati per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], l'account deve essere un membro del **sysadmin** ruolo del server. Questa operazione è necessaria per eseguire il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pacchetti la migrazione dei dati dell'agente.  
  
-   Per eseguire il codice generato da SSMA, l'account deve disporre **Execute** le autorizzazioni per tutte le funzioni definite dall'utente nel **ssma_DB2** dello schema del database di destinazione. Queste funzioni forniscono funzionalità equivalenti di funzioni di sistema DB2 e utilizzate dagli oggetti convertiti.  
  
Se l'account utilizzato per connettersi al [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è per eseguire la migrazione di tutte le attività, l'account deve essere un membro del **sysadmin** ruolo del server.  
  
## <a name="establishing-a-sql-server-connection"></a>Tentativo di stabilire una connessione a SQL Server  
Prima di convertire oggetti di database DB2 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] informazioni sulla sintassi, è necessario stabilire una connessione all'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in cui si desidera migrare i database di DB2.  
  
Quando si definiscono le proprietà di connessione, è inoltre possibile specificare il database in cui verranno migrati dati e oggetti. È possibile personalizzare il mapping a livello di schema DB2 dopo la connessione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per altre informazioni, vedere [Mapping di schemi DB2 a schemi SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/mapping-db2-schemas-to-sql-server-schemas-db2tosql.md).  
  
> [!IMPORTANT]  
> Prima di provare a connettersi al [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], assicurarsi che l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è in esecuzione e può accettare connessioni.  
  
**Per connettersi a SQL Server**  
  
1.  Nel **File** dal menu **Connetti al Server SQL**.  
  
    Se precedentemente connesso al [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], il nome del comando sarà **Riconnetti a SQL Server**.  
  
2.  Nella finestra di dialogo di connessione, immettere o selezionare il nome dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
    -   Se ci si connette all'istanza predefinita nel computer locale, è possibile immettere **localhost** o un punto (**.**).  
  
    -   Se ci si connette all'istanza predefinita in un altro computer, immettere il nome del computer.  
  
    -   Se ci si connette a un'istanza denominata in un altro computer, immettere il nome del computer seguito da una barra rovesciata e quindi il nome dell'istanza, ad esempio MyServer\MyInstance.  
  
3.  Se l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è configurato per accettare le connessioni su una porta non predefinito, immettere il numero di porta usato per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] connessioni nel **porta Server** casella. Per l'istanza predefinita di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], il numero di porta predefinito è 1433. Per le istanze denominate, SSMA tenterà di ottenere il numero di porta dal [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] servizio Browser.  
  
4.  Nel **Database** immettere il nome del database di destinazione.  
  
    Questa opzione non è disponibile quando si riconnette a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
5.  Nel **autenticazione** , selezionare il tipo di autenticazione da usare per la connessione. Per usare l'account di Windows corrente, selezionare **Windows autenticazione**. Usare un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] account di accesso, selezionare **autenticazione di SQL Server**e quindi specificare il nome di accesso e la password.  
  
6.  Per la connessione sicura, vengono aggiunti due controlli, il **Encrypt Connection** e **TrustServerCertificate** caselle di controllo. Solo quando **Encrypt Connection** è selezionata, il **TrustServerCertificate** casella di controllo è visibile. Quando **Encrypt Connection** è selezionata (true) e **TrustServerCertificate** è deselezionato (false), convaliderà il certificato SSL di SQL Server. La convalida del certificato del server fa parte dell'handshake SSL e assicura che il server a cui si esegue la connessione sia quello corretto. A tale scopo, è necessario installare un certificato sul lato client, nonché sul lato server.  
  
7.  Fare clic su **Connetti**.  
  
**Compatibilità di versione superiore**  
  
-   Sarà in grado di connettersi al [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 quando viene creato il progetto di migrazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005.  
  
-   Sarà in grado di connettersi al [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 quando viene creato il progetto di migrazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008 ma non sarà in grado di connettersi a versioni precedenti, ovvero [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005.  
  
-   Sarà in grado di connettersi al [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 quando il progetto creato è SQL Server 2012.  
  
||||||  
|-|-|-|-|-|  
|**VERSIONE SERVER di destinazione e tipo di progetto**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012 <br />(Version:11.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014 <br />(Version:12.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 <br />(Version:13.x)|Database SQL di Azure|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012|Yes|Yes|Yes||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014||Yes|Yes||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014|||Yes||  
|Database SQL di Azure||||Yes|  
  
> [!IMPORTANT]  
> Conversione degli oggetti di database viene eseguita in base al tipo di progetto, ma non in base alla versione del [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] si è connessi. In caso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 o Azure SQL DB.  
  
## <a name="synchronizing-sql-server-metadata"></a>La sincronizzazione dei metadati del Server SQL  
I metadati relativi a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database non viene aggiornato automaticamente. I metadati nel [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] metadati Explorer è uno snapshot dei metadati quando si è connessi prima di tutto a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o l'ultima volta che si dei metadati aggiornato manualmente. È possibile aggiornare manualmente i metadati per tutti i database o per qualsiasi database singolo o un oggetto di database.  
  
**Per sincronizzare i metadati**  
  
1.  Assicurarsi di essere connessi a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
2.  In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Visualizzatore metadati, selezionare la casella di controllo accanto al database o database dello schema che si desidera aggiornare.  
  
    Ad esempio, per aggiornare i metadati per tutti i database, selezionare la casella accanto a **database**.  
  
3.  Fare doppio clic su **database**, o di singoli database o lo schema del database e quindi selezionare **Sincronizza con Database**.  
  
## <a name="next-step"></a>Passaggio successivo  
Il passaggio successivo nel processo di migrazione dipende dalle esigenze del progetto:  
  
-   Per personalizzare il mapping tra schemi DB2 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database e schemi, vedere [Mapping di schemi DB2 a schemi SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/mapping-db2-schemas-to-sql-server-schemas-db2tosql.md).  
  
-   Per personalizzare le opzioni di configurazione per i progetti, vedere [impostazioni del progetto &#40;conversione&#41; &#40;DB2ToSQL&#41; ](../../ssma/db2/project-settings-conversion-db2tosql.md) e relative sezioni.  
  
-   Per personalizzare il mapping dei tipi di dati di origine e di destinazione, vedere [Mapping DB2 e tipi di dati di SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/mapping-db2-and-sql-server-data-types-db2tosql.md).  
  
-   Se non è necessario eseguire nessuna di queste attività, è possibile convertire le definizioni degli oggetti di database DB2 in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] definizioni di oggetto. Per altre informazioni, vedere [conversione di schemi DB2 &#40;DB2ToSQL&#41;](../../ssma/db2/converting-db2-schemas-db2tosql.md).  
  
## <a name="see-also"></a>Vedere anche  
[Database DB2 la migrazione a SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)  
  
