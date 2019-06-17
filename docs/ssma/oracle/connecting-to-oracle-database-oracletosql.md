---
title: La connessione al Database Oracle (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Refreshing Oracle Metadata
ms.assetid: e276cdbf-3ebc-4ba8-b40d-a7a42befa2b6
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 4ad868122fd8986c642bace1b2c9cf419bb89182
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63288394"
---
# <a name="connecting-to-oracle-database-oracletosql"></a>Connessione a un database Oracle (OracleToSQL)
Eseguire la migrazione di database Oracle a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è necessario connettersi al database Oracle che vuoi eseguire la migrazione. Quando ci si connette, SSMA Ottiene i metadati relativi a tutti gli schemi di Oracle e quindi visualizzato nel riquadro di esplorazione di metadati di Oracle. SSMA archivia le informazioni sui server di database, ma non archivia le password.  
  
La connessione al database rimane attiva fino a quando non si chiude il progetto. Quando si riapre il progetto, è necessario riconnettere se si desidera che una connessione attiva al database.  
  
I metadati relativi al database Oracle non viene aggiornato automaticamente. In alternativa, se si desidera aggiornare i metadati nel Visualizzatore metadati Oracle, è necessario aggiornare manualmente lo. Per altre informazioni, vedere la sezione "Aggiornamento dei metadati Oracle" più avanti in questo argomento.  
  
## <a name="required-oracle-permissions"></a>Autorizzazioni necessarie Oracle  
L'account utilizzato per connettersi al database Oracle deve disporre di almeno **CONNECT** autorizzazioni. In questo modo di SSMA ottenere i metadati da schema proprietà dell'utente che esegue la connessione. Per ottenere i metadati per gli oggetti in altri schemi e quindi convertire gli oggetti presenti negli schemi, l'account deve disporre delle autorizzazioni seguenti:  
  
-   CREARE UNA ROUTINE  
  
-   ESEGUIRE EVENTUALI PROCEDURE  
  
-   SELEZIONARE UNA TABELLA  
  
-   SELEZIONARE QUALSIASI SEQUENZA  
  
-   CREARE QUALSIASI TIPO  
  
-   CREARE UN QUALSIASI TRIGGER  
  
-   SELEZIONARE QUALSIASI DIZIONARIO  
  
## <a name="establishing-a-connection-to-oracle"></a>Stabilire una connessione a Oracle  
Quando ci si connette a un database, SSMA legge i metadati del database e quindi aggiunge i metadati del file di progetto. Questi metadati vengono utilizzati da SSMA durante la conversione di oggetti [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] informazioni sulla sintassi, e quando esegue la migrazione di dati a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. È possibile esplorare i metadati nel riquadro di esplorazione di metadati Oracle e le proprietà di singoli oggetti di database.  
  
> [!IMPORTANT]  
> Prima di provare a connettersi, verificare che il server di database è in esecuzione e può accettare connessioni.  
  
**Per connettersi a Oracle**  
  
1.  Nel **File** dal menu **Connect to Oracle**.  
  
    Se in precedenza connesso a Oracle, il nome del comando sarà **Riconnetti a Oracle**.  
  
2.  Nel **Provider** , quindi selezionare **Provider Client Oracle** oppure **Provider OLE DB**, a seconda di quale provider è installato. Il valore predefinito è il client Oracle.  
  
3.  Nel **modalità** seleziona **modalità Standard**, **modalità TNSNAME**, oppure **modalità stringa di connessione**.  
  
    Usare la modalità standard per specificare il nome del server e la porta. Usare la modalità nome del servizio per specificare manualmente il nome del servizio Oracle. Usare modalità stringa di connessione per fornire una stringa di connessione completa.  
  
4.  Se si seleziona **modalità Standard**, specificare i valori seguenti:  
  
    1.  Nel **nome Server** casella, immettere o selezionare il nome o l'indirizzo IP del server di database.  
  
    2.  Se il server di database non è configurato per accettare le connessioni nel valore predefinito (1521) di porta, immettere il numero di porta che viene usato per le connessioni di Oracle nel **porta Server** casella.  
  
    3.  Nel **SID Oracle** immettere l'identificatore del sistema.  
  
    4.  Nel **nome utente** immettere un account di Oracle che dispone delle autorizzazioni necessarie.  
  
    5.  Nel **Password** casella, immettere la password per il nome utente specificato.  
  
5.  Se si seleziona **modalità TNSNAME**, specificare i valori seguenti:  
  
    1.  Nel **connettere identificatore** immettere connettersi identificatore (alias TNS) del database.  
  
    2.  Nel **nome utente** immettere un account di Oracle che dispone delle autorizzazioni necessarie.  
  
    3.  Nel **Password** casella, immettere la password per il nome utente specificato.  
  
6.  Se si seleziona **modalità stringa di connessione**, specificare una stringa di connessione nel **stringa di connessione** casella.  
  
    L'esempio seguente illustra una stringa di connessione OLE DB:  
  
    `Provider=OraOLEDB.Oracle;Data Source=MyOracleDB;User Id=myUsername;Password=myPassword;`  
  
    Nell'esempio seguente mostra una stringa di connessione del Client Oracle che usa la sicurezza integrata:  
  
    `Data Source=MyOracleDB;Integrated Security=yes;`  
  
    Per altre informazioni, vedere [connettersi a Oracle &#40;OracleToSQL&#41;](../../ssma/oracle/connect-to-oracle-oracletosql.md).  
  
## <a name="reconnecting-to-oracle"></a>Connettersi a Oracle  
La connessione al server di database rimane attiva fino a quando non si chiude il progetto. Quando si riapre il progetto, è necessario riconnettere se si desidera che una connessione attiva al database. È possibile lavorare offline fino a quando non si desidera aggiornare i metadati, caricare gli oggetti di database in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ed eseguire la migrazione dei dati.  
  
## <a name="refreshing-oracle-metadata"></a>Aggiornamento dei metadati di Oracle  
I metadati relativi al database Oracle non viene aggiornato automaticamente. I metadati nel Visualizzatore metadati Oracle sono uno snapshot dei metadati quando si è connessi prima di tutto, oppure dall'ultima volta aggiornate manualmente i metadati. È possibile aggiornare manualmente i metadati per tutti gli schemi, un singolo schema o singoli oggetti di database.  
  
**Per aggiornare i metadati**  
  
1.  Assicurarsi di essere connessi al database.  
  
2.  Nel Visualizzatore metadati Oracle, selezionare la casella di controllo accanto a ogni oggetto di database o dello schema che si desidera aggiornare.  
  
3.  Fare doppio clic su **schemi**, o schema singoli o database dell'oggetto e quindi selezionare **aggiornare dal Database**.  
  
    Se non hai una connessione attiva, SSMA visualizzerà il **Connetti a Oracle** finestra di dialogo, in modo che sia possibile connettersi.  
  
4.  Nell'aggiornamento dalla finestra di dialogo di Database, specificare gli oggetti da aggiornare.  
  
    -   Per aggiornare un oggetto, scegliere il **Active** campo adiacente all'oggetto fino a quando non viene visualizzata una freccia.  
  
    -   Per evitare che un oggetto in fase di aggiornamento, fare clic sui **Active** campo adiacente all'oggetto fino a un **X** viene visualizzata.  
  
    -   Per aggiornare o rifiutare una categoria di oggetti, scegliere il **Active** campo accanto alla cartella categoria.  
  
    Per visualizzare le definizioni della codifica a colori, scegliere il **legenda** pulsante.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="next-step"></a>Passaggio successivo  
  
-   Il passaggio successivo del processo di migrazione consiste [connettersi a un'istanza di SQL Server](connecting-to-sql-server-oracletosql.md).  
  
## <a name="see-also"></a>Vedere anche  
[La migrazione da Oracle database in SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
