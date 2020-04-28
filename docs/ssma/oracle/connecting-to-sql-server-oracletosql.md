---
title: Connessione a SQL Server (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Connecting to SQL Server,Synchronizing SQL Server Metadata
ms.assetid: 1b2a8059-1829-4904-a82f-9c06de1e245f
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: cd8f0e57554f32d3b02a6e0e98d3a3645d683bac
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "68266156"
---
# <a name="connecting-to-sql-server-oracletosql"></a>Connessione a SQL Server (OracleToSQL)
Per eseguire la migrazione dei [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database Oracle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a 2005 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , 2008, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008 R2 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o 2012 o 2014 è necessario connettersi a una di queste [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]istanze di destinazione di. Quando si esegue la connessione, SSMA ottiene i metadati relativi a tutti i database nell' [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] istanza di e Visualizza i [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] metadati del database in Esplora metadati. SSMA archivia informazioni sull'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a cui si è connessi, ma non archivia le password.  
  
La connessione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] rimane attiva fino a quando non si chiude il progetto. Quando si riapre il progetto, è necessario riconnettersi a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se si desidera una connessione attiva al server. È possibile lavorare offline fino a quando non si caricano oggetti di database in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e si migrano i dati.  
  
I metadati relativi all'istanza [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di non vengono sincronizzati automaticamente. Per aggiornare i metadati in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Esplora metadati, è invece necessario aggiornare manualmente i [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] metadati. Per ulteriori informazioni, vedere la sezione relativa alla [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sincronizzazione dei metadati più avanti in questo argomento.  
  
## <a name="required-sql-server-permissions"></a>Autorizzazioni SQL Server richieste  
L'account utilizzato per la connessione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] richiede autorizzazioni diverse a seconda delle azioni eseguite dall'account:  
  
-   Per convertire gli oggetti Oracle [!INCLUDE[tsql](../../includes/tsql-md.md)] in sintassi, per aggiornare i [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]metadati da o per salvare la sintassi convertita in script, l'account deve disporre dell'autorizzazione per accedere all' [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]istanza di.  
  
-   Per caricare oggetti di database [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]in, l'account deve essere un membro del ruolo del server **sysadmin** . Questa operazione è necessaria per installare gli assembly CLR.  
  
-   Per eseguire la migrazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]dei dati a, l'account deve essere un membro del ruolo del server **sysadmin** . Questa operazione è necessaria per eseguire [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] i pacchetti di migrazione dei dati dell'agente.  
  
-   Per eseguire il codice generato da SSMA, l'account deve disporre delle autorizzazioni **Execute** per tutte le funzioni definite dall'utente nello schema **ssma_oracle** del database di destinazione. Queste funzioni forniscono funzionalità equivalenti delle funzioni di sistema Oracle e vengono utilizzate dagli oggetti convertiti.  
  
Se l'account utilizzato per la connessione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consiste nell'eseguire tutte le attività di migrazione, l'account deve essere un membro del ruolo del server **sysadmin** .  
  
## <a name="establishing-a-sql-server-connection"></a>Creazione di una connessione SQL Server  
Prima di convertire gli oggetti di database [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Oracle in sintassi, è necessario stabilire una connessione all'istanza [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di in cui si desidera eseguire la migrazione del database o dei database Oracle.  
  
Quando si definiscono le proprietà di connessione, è inoltre necessario specificare il database in cui verrà eseguita la migrazione degli oggetti e dei dati. È possibile personalizzare questo mapping a livello di schema Oracle dopo la connessione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per ulteriori informazioni, vedere [mapping di schemi Oracle a schemi SQL Server &#40;&#41;OracleToSQL ](../../ssma/oracle/mapping-oracle-schemas-to-sql-server-schemas-oracletosql.md).  
  
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
  
5.  Nella casella **autenticazione** selezionare il tipo di autenticazione da utilizzare per la connessione. Per utilizzare l'account di Windows corrente, selezionare **autenticazione di Windows**. Per usare un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] account di accesso, selezionare **SQL Server autenticazione**e quindi specificare il nome e la password dell'account di accesso.  
  
6.  Per una connessione protetta vengono aggiunti due controlli, ovvero le caselle di controllo **Encrypt connection** e **TrustServerCertificate** . La casella di controllo **TrustServerCertificate** è visibile solo quando è selezionata l'opzione **Crittografa connessione** . Quando si seleziona la casella di controllo **Crittografa connessione** (true) e **TrustServerCertificate** è deselezionata (false), verrà convalidato il certificato SSL SQL Server. La convalida del certificato del server fa parte dell'handshake SSL e assicura che il server a cui si esegue la connessione sia quello corretto. Per garantire questo problema, è necessario installare un certificato sul lato client e sul lato server.  
  
7.  Fare clic su **Connetti**.  
  
**Compatibilità delle versioni superiore**  
  
-   Sarà [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] possibile connettersi a 2008 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 quando il progetto di migrazione creato è [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005.  
  
-   Sarà [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] possibile connettersi a 2012 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 quando il progetto di migrazione creato sarà [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008, ma non sarà possibile connettersi a versioni inferiori, ad esempio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005.  
  
-   Sarà possibile connettersi a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 quando il progetto creato è SQL Server 2012.  
  
||||||||  
|-|-|-|-|-|-|-|  
|**TIPO di progetto rispetto alla versione del SERVER di destinazione**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005<br /> (Versione: 9. x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008<br /> (Versione: 10. x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012 <br />(Versione: 11. x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2014 <br />(Versione: 12. x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 <br />(Versione: 13. x)|Database SQL di Azure|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005|Sì|Sì|Sì|Sì|Sì||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008||Sì|Sì|Sì|Sì||
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012|||Sì|Sì|Sì||
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2014||||Sì|Sì||
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016|||||Sì||
|Database SQL di Azure||||||Sì|
  
> [!IMPORTANT]
> La conversione degli oggetti di database viene eseguita in base al tipo di progetto, ma non a seconda della versione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di a cui si è connessi. Nel caso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] un progetto 2005, la conversione viene eseguita in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] base a 2005 anche se si è connessi a una versione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] successiva [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008 o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012 o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014 o 2016).  
  
## <a name="synchronizing-sql-server-metadata"></a>Sincronizzazione di metadati di SQL Server  
I metadati [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] relativi ai database non vengono aggiornati automaticamente. I metadati in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Esplora metadati sono uno snapshot dei metadati alla prima connessione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]oppure l'ultima volta che sono stati aggiornati manualmente i metadati. È possibile aggiornare manualmente i metadati per tutti i database o per qualsiasi singolo database o oggetto di database.  
  
**Per sincronizzare i metadati**  
  
1.  Assicurarsi di essere connessi a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
2.  In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Esplora metadati selezionare la casella di controllo accanto al database o allo schema del database che si desidera aggiornare.  
  
    Ad esempio, per aggiornare i metadati per tutti i database, selezionare la casella accanto a **database**.  
  
3.  Fare clic con il pulsante destro del mouse su **database**o sul database singolo o sullo schema del database, quindi scegliere **Sincronizza con database**.  
  
## <a name="next-step"></a>passaggio successivo  
Il passaggio successivo della migrazione dipende dalle esigenze del progetto:  
  
-   Per personalizzare il mapping tra schemi Oracle e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database e schemi, vedere [mapping di schemi oracle a schemi SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/mapping-oracle-schemas-to-sql-server-schemas-oracletosql.md).  
  
-   Per personalizzare le opzioni di configurazione per i progetti, vedere [impostazione delle opzioni del progetto &#40;OracleToSQL&#41;](../../ssma/oracle/setting-project-options-oracletosql.md).  
  
-   Per personalizzare il mapping dei tipi di dati di origine e di destinazione, vedere [mapping di tipi di dati Oracle e SQL Server &#40;&#41;OracleToSQL ](../../ssma/oracle/mapping-oracle-and-sql-server-data-types-oracletosql.md).  
  
-   Se non è necessario eseguire alcuna di queste attività, è possibile convertire le definizioni degli oggetti di database Oracle in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] definizioni di oggetti. Per ulteriori informazioni, vedere la pagina relativa alla [conversione di schemi Oracle &#40;OracleToSQL&#41;](../../ssma/oracle/converting-oracle-schemas-oracletosql.md).  
  
## <a name="see-also"></a>Vedere anche  
[Migrazione di database Oracle a SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
