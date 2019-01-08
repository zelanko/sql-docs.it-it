---
title: La connessione a SQL Server (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Connecting to SQL Server
ms.assetid: dd368a1a-45b0-40e9-b4d3-5cdb48c26606
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 2d7370b9b219c43bab4bfdc45377795edf148fc9
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/11/2018
ms.locfileid: "53204710"
---
# <a name="connecting-to-sql-server-sybasetosql"></a>Connessione a SQL Server (SybaseToSQL)
La migrazione dei database di Sybase Adaptive Server Enterprise (ASE) a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è necessario connettersi a una delle istanze di destinazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Quando ci si connette, SSMA Ottiene i metadati relativi a tutti i database nell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e visualizza i metadati di database nel [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Visualizzatore metadati. SSMA archivia le informazioni su quale istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] si è connessi a, ma non archivia le password.  
  
La connessione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] rimane attiva fino a quando non si chiude il progetto. Quando si riapre il progetto, è necessario riconnettersi alla [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se si desidera che una connessione attiva al server. È possibile lavorare offline fino a quando non si caricano gli oggetti di database in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ed eseguire la migrazione dei dati.  
  
I metadati sull'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non viene sincronizzato automaticamente. Al contrario, se si desidera aggiornare i metadati in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Visualizzatore metadati, è necessario aggiornare manualmente il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] metadati, come descritto nel "Synchronizing [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] metadati" più avanti in questo argomento.  
  
## <a name="required-sql-server-permissions"></a>Autorizzazioni necessarie di SQL Server  
L'account utilizzato per connettersi a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] richiede autorizzazioni diverse a seconda delle azioni eseguite da quell'account.  
  
-   Per convertire gli oggetti ambiente del servizio app [!INCLUDE[tsql](../../includes/tsql-md.md)] sintassi, per aggiornare i metadati dal [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o per salvare sintassi convertita in script, l'account deve disporre dell'autorizzazione per accedere all'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Per caricare gli oggetti di database in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], il requisito di autorizzazione minima necessaria è l'appartenenza al **db_owner** ruolo del database nel database di destinazione.  
  
-   Per eseguire la migrazione dei dati per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], l'account deve essere un membro del **sysadmin** ruolo del server. Questa operazione è necessaria per eseguire il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pacchetti la migrazione dei dati dell'agente.  
  
-   Per eseguire il codice generato da SSMA, l'account deve disporre **Execute** le autorizzazioni per tutte le funzioni definite dall'utente nel **ssma_syb** dello schema del **sysdb** database. Queste funzioni forniscono funzionalità equivalenti ambiente del servizio app di funzioni di sistema e vengono utilizzate per gli oggetti convertiti.  
  
Se l'account utilizzato per connettersi al [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è per eseguire la migrazione di tutte le attività, l'account deve essere un membro del **sysadmin** ruolo del server.  
  
## <a name="establishing-a-sql-server-connection"></a>Tentativo di stabilire una connessione a SQL Server  
Prima di convertire oggetti di database di ASE [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] informazioni sulla sintassi, è necessario stabilire una connessione all'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in cui si desidera migrare i database di ambiente del servizio app.  
  
Quando si definiscono le proprietà di connessione, è inoltre possibile specificare il database in cui verranno migrati dati e oggetti. È possibile personalizzare il mapping a livello di schema ambiente del servizio App dopo la connessione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per altre informazioni, vedere [Mapping di schemi di ASE Sybase a schemi SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-schemas-to-sql-server-schemas-sybasetosql.md).  
  
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
  
    Questa opzione non è disponibile durante la riconnessione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
5.  Nel **autenticazione** , selezionare il tipo di autenticazione da usare per la connessione. Per usare l'account di Windows corrente, selezionare **Windows autenticazione**. Usare un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] account di accesso, selezionare **autenticazione di SQL Server** e quindi specificare il nome di accesso e la password.  
  
6.  Per la connessione sicura, vengono aggiunti due controlli, il **Encrypt Connection** e **TrustServerCertificate** caselle di controllo. Solo quando **Encrypt Connection** è selezionata, il **TrustServerCertificate** casella di controllo è visibile. Quando **Encrypt Connection** è selezionata (true) e **TrustServerCertificate** è deselezionato (false), convaliderà il certificato SSL di SQL Server. La convalida del certificato del server fa parte dell'handshake SSL e assicura che il server a cui si esegue la connessione sia quello corretto. A tale scopo, è necessario installare un certificato sul lato client, nonché sul lato server.  
  
7.  Fare clic su **Connetti**.  
  
**Compatibilità di versione superiore**  
  
-   Sarà in grado di connettersi al [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 quando viene creato il progetto di migrazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005.  
  
-   Sarà in grado di connettersi al [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 quando viene creato il progetto di migrazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008 ma non sarà in grado di connettersi a versioni precedenti, ovvero [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005.  
  
-   Sarà in grado di connettersi solo a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 quando il progetto creato è SQL Server 2012.  
  
-   Compatibilità di versione superiore non è valida per SQL Azure.  
  
||||||||
|-|-|-|-|-|-|-|
|**VERSIONE SERVER di destinazione e tipo di progetto**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005<br /> (Versione: 9.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008<br /> (Versione: 10.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012 <br />(Version:11.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014 <br />(Version:12.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 <br />(Version:13.x)|SQL Azure|
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005|Yes|Yes|Yes|Yes|Yes||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008||Yes|Yes|Yes|Yes||
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012|||Yes|Yes|Yes||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014||||Yes|Yes|| 
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016|||||Yes||  
|SQL Azure||||||Yes|  
  
> [!IMPORTANT]
> Conversione degli oggetti di database viene eseguita in base al tipo di progetto, ma non in base alla versione del [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] si è connessi. In caso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] progetto 2005, la conversione viene eseguita come descritto [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anche se si è connessi a una versione successiva del 2005 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008 o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012 oppure [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014 o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016)  
  
## <a name="reconnecting-to-sql-server"></a>Connettersi a SQL Server  
La connessione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] rimane attiva fino a quando non si chiude il progetto. Quando si riapre il progetto, è necessario riconnettersi alla [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se si desidera che una connessione attiva al server. È possibile lavorare offline finché non si aggiorna i metadati, oggetti di database di carico in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ed eseguire la migrazione dei dati.  
  
La procedura per la riconnessione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è quello utilizzato per la procedura per stabilire una connessione.  
  
## <a name="synchronizing-sql-server-metadata"></a>La sincronizzazione dei metadati del Server SQL  
I metadati relativi al [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database non viene aggiornato automaticamente. I metadati nel [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] metadati Explorer è uno snapshot dei metadati quando si è connessi prima di tutto a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o l'ultima volta che si dei metadati aggiornato manualmente. È possibile aggiornare manualmente i metadati per tutti i database o per qualsiasi database singolo o un oggetto di database.  
  
**Per sincronizzare i metadati**  
  
1.  Assicurarsi di essere connessi a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
2.  In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Visualizzatore metadati, selezionare la casella di controllo accanto al database o database dello schema che si desidera aggiornare.  
  
    Ad esempio, per aggiornare i metadati per tutti i database, selezionare la casella accanto a **database**.  
  
3.  I database o i singoli database o lo schema del database e quindi scegliere **Sincronizza con Database**.  
  
## <a name="next-step"></a>Passaggio successivo  
Il passaggio successivo nel processo di migrazione dipende dalle esigenze del progetto:  
  
-   Se si desidera personalizzare il mapping tra i database di ambiente del servizio App e gli schemi e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database e schemi, vedere [gli schemi di Mapping Sybase ASE a schemi SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-schemas-to-sql-server-schemas-sybasetosql.md).  
  
-   Se si desidera personalizzare le opzioni di configurazione per i progetti, vedere [impostazione delle opzioni progetto &#40;SybaseToSQL&#41;](../../ssma/sybase/setting-project-options-sybasetosql.md).  
  
-   Se si vuole su personalizzato il mapping dei tipi di dati di origine e di destinazione, vedere [Mapping di Sybase ASE e SQL Server Data Types &#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-and-sql-server-data-types-sybasetosql.md).  
  
-   Se non è necessario effettuare una delle seguenti, è possibile convertire le definizioni degli oggetti di database di Sybase ASE in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] definizioni di oggetto. Per altre informazioni, vedere [convertire gli oggetti di Database di Sybase ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/converting-sybase-ase-database-objects-sybasetosql.md).  
  
## <a name="see-also"></a>Vedere anche  
[Migrazione dei database di Sybase ASE a SQL Server - Azure SQL database &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
