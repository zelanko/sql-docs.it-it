---
title: La connessione a MySQL (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Connecting to MySQL, MySQL permission
- Connecting to MySQL,reconnecting
ms.assetid: 084c7020-f729-4f91-90e0-143f85fa68d1
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 233b6824ef527a9ed4e7e02164a08e31e41f3699
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63253330"
---
# <a name="connecting-to-mysql-mysqltosql"></a>Connessione a MySQL (MySQLToSQL)
Per eseguire la migrazione di database MySQL a SQL Server o SQL Azure, è necessario connettersi al database MySQL che si desidera eseguire la migrazione. Quando ci si connette, SSMA Ottiene i metadati relativi a tutti gli schemi di MySQL e quindi visualizzato nel riquadro di esplorazione di metadati di MySQL. SSMA archivia le informazioni sui server di database, ma non archivia le password.  
  
La connessione al database rimane attiva fino a quando non si chiude il progetto. Quando si riapre il progetto, è necessario riconnettere se si desidera che una connessione attiva al database.  
  
I metadati relativi al database MySQL non viene aggiornato automaticamente. In alternativa, se si desidera aggiornare i metadati nel Visualizzatore metadati MySQL, è necessario aggiornare manualmente lo. Per altre informazioni, vedere la sezione "Aggiornamento dei metadati di MySQL" più avanti in questo argomento.  
  
## <a name="required-mysql-permissions"></a>Autorizzazioni necessarie MySQL  
L'account utilizzato per connettersi al database MySQL deve avere almeno **CONNECT** autorizzazioni. In questo modo di SSMA ottenere i metadati da schema proprietà dell'utente che esegue la connessione. Per ottenere i metadati per gli oggetti in altri schemi e quindi convertire gli oggetti presenti negli schemi, l'account deve disporre delle autorizzazioni seguenti:  
  
-   "SHOW" i privilegi per gli oggetti di database  
  
-   Privilegio 'SELECT' per 'Information_schema'  
  
-   'SELECT' privilegio per mysql (per funzioni definite dall'utente)  
  
## <a name="establishing-a-connection-to-mysql"></a>Stabilire una connessione a MySQL  
Quando ci si connette a un database, SSMA legge i metadati del database e quindi aggiunge i metadati del file di progetto. Questi metadati viene usato da SSMA durante la conversione di oggetti per la sintassi di SQL Server o SQL Azure, e quando la migrazione dei dati in SQL Server o SQL Azure. È possibile esplorare i metadati nel riquadro di esplorazione di metadati di MySQL e le proprietà di singoli oggetti di database.  
  
> [!IMPORTANT]  
> Prima di provare a connettersi, verificare che il server di database è in esecuzione e può accettare connessioni.  
  
**Per connettersi a MySQL**  
  
1.  Nel **File** dal menu **connettersi a MySQL** (questa opzione verrà attivata dopo la creazione del progetto).  
  
    Se in precedenza si è connessi a MySQL, il nome del comando sarà **Riconnetti a MySQL**.  
  
2.  Nel **Provider** selezionare MySQL 5.1 provider ODBC (attendibili). È il provider predefinito in modalità standard.  
  
3.  Nel **modalità** , quindi selezionare **modalità Standard**. Si tratta della modalità predefinita.  
  
    Usare la modalità standard per specificare il nome del server e la porta.  
  
4.  Nelle **modalità Standard**, specificare i valori seguenti:  
  
    1.  Nel **nome Server** immettere il nome del server MySQL. Nel **porta Server** immettere il numero di porta per essere 3306. È la porta predefinita.  
  
    2.  Nel **nome utente** immettere un account di MySQL che dispone delle autorizzazioni necessarie.  
  
    3.  Nel **Password** casella, immettere la password per il nome utente specificato.  
  
5.  **SSL:** Se si desidera connettersi in modo sicuro a MySQL, assicurarsi di usare di Secure Socket Layer (SSL), controllare la **SSL** casella di controllo.  
  
6.  **Configurare:** Fornisce un'opzione per configurare la connessione a MySQL tramite Secure Socket Layer (SSL).  
  
    > [!NOTE]  
    > Per abilitare **Configure**, SSL deve essere impostata su **True**.  
  
    Facendo clic sul pulsante "Configura", viene visualizzata una finestra di dialogo. Utilizzare la crittografia durante la connessione al MySQL Database, percorso file tre certificato seguenti presente nella finestra di dialogo deve essere definito [Privacy avanzata posta certificati (PEM)]:  
  
    -   **Autorità di certificazione SSL:** Specifica il percorso di un file con un elenco di attendibilità SSL CA.  
  
    -   **Certificato SSL:** Specifica il nome del file del certificato SSL da utilizzare per stabilire una connessione sicura.  
  
    -   **CHIAVE SSL:** Specifica il nome del file di chiave SSL da utilizzare per stabilire una connessione sicura.  
  
    > [!NOTE]  
    > -   Il **OK** pulsante viene abilitato quando sono state fornite le informazioni necessarie. Se sono presenti i percorsi dei file non validi, il pulsante "OK" rimarrà disabilitato.  
    > -   Il **annullare** pulsante chiude la finestra di dialogo e **disattiva** l'opzione SSL dal Form di connessione principale.  
  
7.  Per altre informazioni, vedere [connettersi a MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/connect-to-mysql-mysqltosql.md)  
  
## <a name="reconnecting-to-mysql"></a>La riconnessione a MySQL  
La connessione al server di database rimane attiva fino a quando non si chiude il progetto. Quando si riapre il progetto, è necessario riconnettere se si desidera che una connessione attiva al database. È possibile lavorare offline fino a quando non si desidera aggiornare i metadati, caricare gli oggetti di database in SQL Server o SQL Azure e la migrazione dei dati.  
  
## <a name="refreshing-mysql-metadata"></a>Aggiornamento dei metadati di MySQL  
I metadati relativi al database MySQL non viene aggiornato automaticamente. I metadati nel Visualizzatore metadati MySQL sono uno snapshot dei metadati quando si è connessi prima di tutto, oppure dall'ultima volta aggiornate manualmente i metadati. È possibile aggiornare manualmente i metadati per tutti gli schemi, un singolo schema o singoli oggetti di database.  
  
**Per aggiornare i metadati**  
  
1.  Assicurarsi di essere connessi al database.  
  
2.  Nel Visualizzatore metadati di MySQL, selezionare la casella di controllo accanto a ogni oggetto di database o dello schema che si desidera aggiornare.  
  
3.  Fare doppio clic su **schemi**, o schema singoli o database dell'oggetto e quindi selezionare **aggiornare dal Database**.  
  
    Se non hai una connessione attiva, SSMA visualizzerà il **connettersi a MySQL** finestra di dialogo, in modo che sia possibile connettersi.  
  
4.  Nell'aggiornamento dalla finestra di dialogo di Database, specificare gli oggetti da aggiornare.  
  
    -   Per aggiornare un oggetto, scegliere il **Active** campo adiacente all'oggetto fino a quando non viene visualizzata una freccia.  
  
    -   Per evitare che un oggetto in fase di aggiornamento, fare clic sui **Active** campo adiacente all'oggetto fino a un **X** viene visualizzata.  
  
    -   Per aggiornare o rifiutare una categoria di oggetti, scegliere il **Active** campo accanto alla cartella categoria.  
  
    -   Per visualizzare le definizioni della codifica a colori, scegliere il **legenda** pulsante.  
  
5.  Fare clic su **OK**.  
  
## <a name="next-step"></a>Passaggio successivo  
Il passaggio successivo del processo di migrazione consiste [connessione a SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-sql-server-mysqltosql.md)  
  
## <a name="see-also"></a>Vedere anche  
[Database di migrazione da MySQL a SQL Server - Azure SQL database &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
