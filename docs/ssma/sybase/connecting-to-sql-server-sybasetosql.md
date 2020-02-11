---
title: Connessione a SQL Server (SybaseToSQL) | Microsoft Docs
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
ms.openlocfilehash: 4f40fd6fa88b001eaa222789d6be35b83f9bf90a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67948541"
---
# <a name="connecting-to-sql-server-sybasetosql"></a>Connessione a SQL Server (SybaseToSQL)
Per eseguire la migrazione dei database di Sybase Adaptive Server Enterprise ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ASE) a, è necessario connettersi a una delle istanze [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]di di destinazione di. Quando si esegue la connessione, SSMA ottiene i metadati relativi a tutti i database nell' [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] istanza di e Visualizza i [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] metadati del database in Esplora metadati. SSMA archivia informazioni sull'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a cui si è connessi, ma non archivia le password.  
  
La connessione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] rimane attiva fino a quando non si chiude il progetto. Quando si riapre il progetto, è necessario riconnettersi a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se si desidera una connessione attiva al server. È possibile lavorare offline fino a quando non si caricano oggetti di database in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e si migrano i dati.  
  
I metadati relativi all'istanza [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di non vengono sincronizzati automaticamente. Se invece si desidera aggiornare i metadati in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Esplora metadati, è necessario aggiornare manualmente i [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] metadati, come descritto nella sezione "sincronizzazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dei metadati" più avanti in questo argomento.  
  
## <a name="required-sql-server-permissions"></a>Autorizzazioni SQL Server richieste  
L'account utilizzato per la connessione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] richiede autorizzazioni diverse a seconda delle azioni eseguite dall'account.  
  
-   Per convertire gli oggetti dell' [!INCLUDE[tsql](../../includes/tsql-md.md)] ambiente del servizio app in sintassi [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], per aggiornare i metadati da o per salvare la sintassi convertita in script, l'account deve disporre dell' [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]autorizzazione per accedere all'istanza di.  
  
-   Per caricare oggetti di database [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]in, il requisito di autorizzazione minimo è l'appartenenza al ruolo del database **db_owner** nel database di destinazione.  
  
-   Per eseguire la migrazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]dei dati a, l'account deve essere un membro del ruolo del server **sysadmin** . Questa operazione è necessaria per eseguire [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] i pacchetti di migrazione dei dati dell'agente.  
  
-   Per eseguire il codice generato da SSMA, l'account deve disporre delle autorizzazioni **Execute** per tutte le funzioni definite dall'utente nello schema **ssma_syb** del database **sysdb** . Queste funzioni forniscono funzionalità equivalenti delle funzioni di sistema dell'ambiente del servizio app e vengono usate dagli oggetti convertiti.  
  
Se l'account utilizzato per la connessione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consiste nell'eseguire tutte le attività di migrazione, l'account deve essere un membro del ruolo del server **sysadmin** .  
  
## <a name="establishing-a-sql-server-connection"></a>Creazione di una connessione SQL Server  
Prima di convertire gli oggetti di database [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dell'ambiente del servizio app nella sintassi, è necessario stabilire [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] una connessione all'istanza di in cui si vuole eseguire la migrazione del database o dei database dell'ambiente del servizio app.  
  
Quando si definiscono le proprietà di connessione, è inoltre necessario specificare il database in cui verrà eseguita la migrazione degli oggetti e dei dati. È possibile personalizzare questo mapping a livello di schema dell'ambiente del servizio app [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]dopo la connessione a. Per altre informazioni, vedere mapping di schemi dell'ambiente del servizio app [Sybase a schemi SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-schemas-to-sql-server-schemas-sybasetosql.md).  
  
> [!IMPORTANT]  
> Prima di provare a connettersi a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], verificare che l'istanza di sia [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in esecuzione e che sia in grado di accettare le connessioni.  
  
**Per eseguire la connessione a SQL Server**  
  
1.  Scegliere **Connetti a SQL Server**dal menu **file** .  
  
    Se in precedenza si è [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]connessi a, il nome del comando verrà **riconnesso a SQL Server**.  
  
2.  Nella finestra di dialogo connessione immettere o selezionare il nome dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
    -   Se ci si connette all'istanza predefinita nel computer locale, è possibile immettere **localhost** o un punto (**.**).  
  
    -   Se ci si connette all'istanza predefinita in un altro computer, immettere il nome del computer.  
  
    -   Se ci si connette a un'istanza denominata in un altro computer, immettere il nome del computer seguito da una barra rovesciata e quindi dal nome dell'istanza, ad esempio MyServer\MyInstance.  
  
3.  Se l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è configurata in modo da accettare connessioni su una porta non predefinita, immettere il numero di porta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizzato per le connessioni nella casella **porta server** . Per l'istanza predefinita di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], il numero di porta predefinito è 1433. Per le istanze denominate, SSMA proverà a ottenere il numero [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di porta dal servizio browser.  
  
4.  Nella casella **database** immettere il nome del database di destinazione.  
  
    Questa opzione non è disponibile quando si esegue la riconnessione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
5.  Nella casella **autenticazione** selezionare il tipo di autenticazione da utilizzare per la connessione. Per utilizzare l'account di Windows corrente, selezionare **autenticazione di Windows**. Per usare un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] account di accesso, selezionare **SQL Server autenticazione** e quindi specificare il nome e la password dell'account di accesso.  
  
6.  Per una connessione protetta vengono aggiunti due controlli, ovvero le caselle di controllo **Encrypt connection** e **TrustServerCertificate** . La casella di controllo **TrustServerCertificate** è visibile solo quando è selezionata l'opzione **Crittografa connessione** . Quando si seleziona la casella di controllo **Crittografa connessione** (true) e **TrustServerCertificate** è deselezionata (false), verrà convalidato il certificato SSL SQL Server. La convalida del certificato del server fa parte dell'handshake SSL e assicura che il server a cui si esegue la connessione sia quello corretto. Per garantire questo problema, è necessario installare un certificato sul lato client e sul lato server.  
  
7.  Fare clic su **Connetti**.  
  
**Compatibilità delle versioni superiore**  
  
-   Sarà [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] possibile connettersi a 2008 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 quando il progetto di migrazione creato è [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005.  
  
-   Sarà [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] possibile connettersi a 2012 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 quando il progetto di migrazione creato sarà [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008, ma non sarà possibile connettersi a versioni inferiori, ad esempio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005.  
  
-   Sarà possibile connettersi solo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a 2012 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 quando il progetto creato è SQL Server 2012.  
  
-   La compatibilità con le versioni successive non è valida per SQL Azure.  
  
||||||||
|-|-|-|-|-|-|-|
|**TIPO di progetto rispetto alla versione del SERVER di destinazione**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2005<br /> (Versione: 9. x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2008<br /> (Versione: 10. x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2012 <br />(Versione: 11. x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2014 <br />(Versione: 12. x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 <br />(Versione: 13. x)|SQL Azure|
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2005|Sì|Sì|Sì|Sì|Sì||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2008||Sì|Sì|Sì|Sì||
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2012|||Sì|Sì|Sì||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2014||||Sì|Sì|| 
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016|||||Sì||  
|SQL Azure||||||Sì|  
  
> [!IMPORTANT]
> La conversione degli oggetti di database viene eseguita in base al tipo di progetto, ma non a seconda della versione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di a cui si è connessi. Nel caso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] un progetto 2005, la conversione viene eseguita in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] base a 2005 anche se si è connessi a una versione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] successiva [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008 o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012 o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014 o 2016)  
  
## <a name="reconnecting-to-sql-server"></a>Riconnessione a SQL Server  
La connessione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] rimane attiva fino a quando non si chiude il progetto. Quando si riapre il progetto, è necessario riconnettersi a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se si desidera una connessione attiva al server. È possibile lavorare offline fino a quando non si aggiornano i metadati [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], si caricano oggetti di database e si esegue la migrazione dei dati  
  
La procedura per la riconnessione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è identica alla procedura per stabilire una connessione.  
  
## <a name="synchronizing-sql-server-metadata"></a>Sincronizzazione di metadati di SQL Server  
I metadati relativi [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ai database non vengono aggiornati automaticamente. I metadati in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Esplora metadati sono uno snapshot dei metadati alla prima connessione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]oppure l'ultima volta che sono stati aggiornati manualmente i metadati. È possibile aggiornare manualmente i metadati per tutti i database o per qualsiasi singolo database o oggetto di database.  
  
**Per sincronizzare i metadati**  
  
1.  Assicurarsi di essere connessi a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
2.  In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Esplora metadati selezionare la casella di controllo accanto al database o allo schema del database che si desidera aggiornare.  
  
    Ad esempio, per aggiornare i metadati per tutti i database, selezionare la casella accanto a **database**.  
  
3.  Fare clic con il pulsante destro del mouse su database o sul database singolo o sullo schema del database, quindi scegliere **Sincronizza con database**.  
  
## <a name="next-step"></a>passaggio successivo  
Il passaggio successivo della migrazione dipende dalle esigenze del progetto:  
  
-   Se si vuole personalizzare il mapping tra i database dell'ambiente del servizio app [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e gli schemi e i database e gli schemi, vedere mapping degli schemi dell'ambiente del servizio app [Sybase a schemi SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-schemas-to-sql-server-schemas-sybasetosql.md).  
  
-   Se si desidera personalizzare le opzioni di configurazione per i progetti, vedere [impostazione delle opzioni del progetto &#40;SybaseToSQL&#41;](../../ssma/sybase/setting-project-options-sybasetosql.md).  
  
-   Se si vuole personalizzare il mapping dei tipi di dati di origine e di destinazione, vedere Mapping dei tipi di [dati di Sybase ASE e SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-and-sql-server-data-types-sybasetosql.md).  
  
-   Se non è necessario eseguire nessuna di queste operazioni, è possibile convertire le definizioni degli oggetti di database Sybase ASE [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in definizioni di oggetti. Per altre informazioni, vedere [conversione di oggetti di database Sybase ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/converting-sybase-ase-database-objects-sybasetosql.md).  
  
## <a name="see-also"></a>Vedere anche  
[Migrazione dei database Sybase ASE a SQL Server-database SQL di Azure &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
