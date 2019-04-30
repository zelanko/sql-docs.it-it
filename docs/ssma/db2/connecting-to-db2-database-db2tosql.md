---
title: La connessione al Database di DB2 (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 5eb5801d-f0c3-4127-97c0-0b1ef49f4844
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: ce6a13eec87b60480ed2e68aa3d21a4c4f90ba1b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63299352"
---
# <a name="connecting-to-db2-database-db2tosql"></a>La connessione al Database di DB2 (DB2ToSQL)
Per eseguire la migrazione di database DB2 a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è necessario connettersi al database DB2 che si desidera eseguire la migrazione. Quando ci si connette, SSMA Ottiene i metadati relativi a tutti gli schemi DB2 e successivamente visualizzata nel riquadro di esplorazione di metadati di DB2. SSMA archivia le informazioni sui server di database, ma non archivia le password.  
  
La connessione al database rimane attiva fino a quando non si chiude il progetto. Quando si riapre il progetto, è necessario riconnettere se si desidera che una connessione attiva al database.  
  
I metadati relativi a database DB2 non viene aggiornato automaticamente. In alternativa, se si desidera aggiornare i metadati nel Visualizzatore metadati DB2, è necessario aggiornare manualmente lo. Per altre informazioni, vedere la sezione "Aggiornamento dei metadati di DB2" più avanti in questo argomento.  
  
## <a name="required-db2-permissions"></a>Autorizzazioni di DB2 richiesto  
Autorizzazione utente definisce l'elenco dei comandi e gli oggetti che sono disponibili per un utente. Questo elenco controlla quindi le azioni dell'utente. In DB2, sono presenti gruppi predeterminati di privilegi per l'autorizzazione a livello di istanza sia a livello di un database DB2. In questo modo di SSMA ottenere i metadati da schema proprietà dell'utente che esegue la connessione. Per ottenere i metadati per gli oggetti in altri schemi e quindi convertire gli oggetti presenti negli schemi, l'account deve disporre delle autorizzazioni seguenti:  
  
-   L'accesso dello schema per la migrazione dello schema in genere è impostata su PUBLIC a meno che non è stata utilizzata la parola chiave RESTRICT in Crea  
  
-   DATAACCESS richiede l'accesso ai dati per la migrazione dei dati  
  
## <a name="establishing-a-connection-to-db2"></a>Stabilire una connessione a DB2  
Quando ci si connette a un database, SSMA legge i metadati del database e quindi aggiunge i metadati del file di progetto. Questi metadati vengono utilizzati da SSMA durante la conversione di oggetti [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] informazioni sulla sintassi, e quando esegue la migrazione di dati a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. È possibile esplorare i metadati nel riquadro di esplorazione di metadati di DB2 e le proprietà di singoli oggetti di database.  
  
> [!IMPORTANT]  
> Prima di provare a connettersi, verificare che il server di database è in esecuzione e può accettare connessioni.  
  
**Per la connessione a DB2**  
  
1.  Nel **File** dal menu **Connetti a DB2**.  
  
    Se in precedenza connesso a DB2, il nome del comando sarà **Riconnetti a DB2**.  
  
2.  Nel **Provider** casella verrà visualizzato il **Provider OLE DB** che è attualmente l'unico provider di accesso client DB2.  
  
3.  Nel **gestore** finestra è possibile selezionare uno **Db2 per zOs**, o **DB2 per LUW**  
  
4.  Nel **modalità** seleziona **modalità Standard**, o **modalità stringa di connessione**.  
  
    Usare la modalità standard per specificare il nome del server e la porta. Usare la modalità nome del servizio per specificare il nome del servizio DB2 manualmente. Usare modalità stringa di connessione per fornire una stringa di connessione completa.  
  
5.  Se si seleziona **modalità Standard**, specificare i valori seguenti:  
  
    -   Nel **nome Server** casella, immettere o selezionare il nome o l'indirizzo IP del server di database.  
  
    -   Se il server di database non è configurato per accettare le connessioni nel valore predefinito (1521) di porta, immettere il numero di porta che viene usato per le connessioni di DB2 nel **porta Server** casella.  
  
    -   Nel **porta Server** casella, immettere il numero di porta TCP/IP.  
  
    -   Nel **Initial Catalog** immettere il nome del database  
  
    -   Nel **nome utente** immettere un account di DB2 dotato delle autorizzazioni necessarie.  
  
    -   Nel **Password** casella, immettere la password per il nome utente specificato.  
  
6.  Se si seleziona **modalità stringa di connessione**, specificare una stringa di connessione nel **stringa di connessione** casella.  
  
    L'esempio seguente illustra una stringa di connessione OLE DB:  
  
    `Provider=OraOLEDB.DB2;Data Source=MyDB2DB;User Id=myUsername;Password=myPassword;`  
  
    Nell'esempio seguente mostra una stringa di connessione Client DB2 che utilizza la sicurezza integrata:  
  
    `Data Source=MyDB2DB;Integrated Security=yes;`  
  
    Per altre informazioni, vedere [connettersi a Oracle &#40;OracleToSQL&#41;](../../ssma/oracle/connect-to-oracle-oracletosql.md).  
  
## <a name="reconnecting-to-db2"></a>La riconnessione a DB2  
La connessione al server di database rimane attiva fino a quando non si chiude il progetto. Quando si riapre il progetto, è necessario riconnettere se si desidera che una connessione attiva al database. È possibile lavorare offline fino a quando non si desidera aggiornare i metadati, caricare gli oggetti di database in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ed eseguire la migrazione dei dati.  
  
## <a name="refreshing-db2-metadata"></a>Aggiornamento dei metadati di DB2  
I metadati relativi a database DB2 non viene aggiornato automaticamente. I metadati nel Visualizzatore metadati DB2 sono uno snapshot dei metadati quando si è connessi prima di tutto, oppure dall'ultima volta aggiornate manualmente i metadati. È possibile aggiornare manualmente i metadati per tutti gli schemi, un singolo schema o singoli oggetti di database.  
  
**Per aggiornare i metadati**  
  
1.  Assicurarsi di essere connessi al database.  
  
2.  Nel Visualizzatore metadati DB2, selezionare la casella di controllo accanto a ogni oggetto di database o dello schema che si desidera aggiornare.  
  
3.  Fare doppio clic su **schemi**, o schema singoli o database dell'oggetto e quindi selezionare **aggiornare dal Database**.  
  
    Se non hai una connessione attiva, SSMA visualizzerà il **connettersi a DB2** finestra di dialogo, in modo che sia possibile connettersi.  
  
4.  Nell'aggiornamento dalla finestra di dialogo di Database, specificare gli oggetti da aggiornare.  
  
    -   Per aggiornare un oggetto, scegliere il **Active** campo adiacente all'oggetto fino a quando non viene visualizzata una freccia.  
  
    -   Per evitare che un oggetto in fase di aggiornamento, fare clic sui **Active** campo adiacente all'oggetto fino a un **X** viene visualizzata.  
  
    -   Per aggiornare o rifiutare una categoria di oggetti, scegliere il **Active** campo accanto alla cartella categoria.  
  
    Per visualizzare le definizioni della codifica a colori, scegliere il **legenda** pulsante.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="next-step"></a>Passaggio successivo  
  
-   Il passaggio successivo del processo di migrazione consiste [connessione a SQL Server](https://msdn.microsoft.com/b59803cb-3cc6-41cc-8553-faf90851410e).  
  
## <a name="see-also"></a>Vedere anche  
[Database DB2 la migrazione a SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)  
  
