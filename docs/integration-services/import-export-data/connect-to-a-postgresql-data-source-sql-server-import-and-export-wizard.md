---
title: Connettersi a un'origine dati PostgreSQL (Importazione/Esportazione guidata SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: b7a75a72-b267-444f-9eb8-d23eb333fc35
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 168e53dde51641d79569eb3ef6a1930d0084d10f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65723980"
---
# <a name="connect-to-a-postgresql-data-source-sql-server-import-and-export-wizard"></a>Connettersi a un'origine dati PostgreSQL (Importazione/Esportazione guidata SQL Server)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


Questo argomento illustra come connettersi a un'origine dati **PostgreSQL** dalla pagina **Scelta origine dati** o **Scelta destinazione** dell'Importazione/Esportazione guidata SQL Server. 

> [!IMPORTANT]
> Le informazioni dettagliate sui requisiti e i prerequisiti per la connessione a un database PostgreSQL non rientrano nell'ambito di questo articolo di Microsoft. Questo articolo presuppone che sia già stato installato il software client PostgreSQL e che sia già possibile connettersi al database PostgreSQL di destinazione. Per altre informazioni, contattare l'amministratore del database PostgreSQL o consultare la documentazione di PostgreSQL.

## <a name="get-the-postgresql-odbc-driver"></a>Ottenere il driver ODBC PostgreSQL

### <a name="install-the-odbc-driver-with-stack-builder"></a>Installare il driver ODBC con il generatore di stack
Eseguire il generatore di stack per aggiungere il driver ODBC PostgreSQL (psqlODBC) all'installazione di PostgreSQL.

![Installare il driver ODBC PostgreSQL con il generatore di stack](../../integration-services/import-export-data/media/install-postgresql-odbc-with-stack-builder.png)

### <a name="or-download-the-latest-odbc-driver"></a>Scaricare il driver ODBC più recente
In alternativa, scaricare il programma di installazione di Windows per la versione più recente del driver ODBC PostgreSQL (psqlODBC) direttamente da questo sito FTP: [https://www.postgresql.org/ftp/odbc/versions/msi/](https://www.postgresql.org/ftp/odbc/versions/msi/). Estrarre i file dal file con estensione zip ed eseguire il file con estensione msi.

## <a name="connect-to-postgresql-with-the-postgresql-odbc-driver-psqlodbc"></a>Connettersi a PostgreSQL con il driver ODBC PostgreSQL (psqlODBC)
I driver ODBC non sono presenti nell'elenco a discesa delle origini dati. Per connettersi con un driver ODBC, selezionare innanzitutto **Provider di dati .NET Framework per ODBC** come origine dati nella pagina **Scelta origine dati** o **Scelta destinazione**. Questo provider funge da wrapper per il driver ODBC.

Di seguito è riportata la schermata generica che viene visualizzata dopo aver selezionato il Provider di dati .NET Framework per ODBC.

![Connettersi a PostgreSQL con ODBC (prima)](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-before.jpg)

### <a name="options-to-specify-postgresql-odbc-driver"></a>Opzioni da specificare (Driver ODBC PostgreSQL)

> [!NOTE]
> Le opzioni di connessione per il provider di dati e il driver ODBC sono le stesse sia nel caso in cui PostgreSQL rappresenti l'origine sia nel caso in cui rappresenti la destinazione. Ovvero, le opzioni visualizzate sono le stesse in entrambe le pagine **Scelta origine dati** e **Scelta destinazione** della procedura guidata.

Per connettersi a PostgreSQL con il driver ODBC PostgreSQL, assemblare una stringa di connessione che includa le impostazioni seguenti e i relativi valori. Il formato di una stringa di connessione completa segue immediatamente l'elenco di impostazioni.

> [!TIP]
> Ottenere informazioni per assemblare la stringa di connessione più adatta. In alternativa, anziché specificare una stringa di connessione, immettere un DSN esistente (nome dell'origine dati) o crearne uno nuovo. Per altre informazioni su queste opzioni, vedere [Connettersi a un'origine dati ODBC](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md).

**Driver**  
Nome del driver ODBC, **PostgreSQL ODBC Driver(UNICODE)** o **PostgreSQL ODBC Driver(ANSI)** .

**Server**  
Nome del server PostgreSQL. 

**Porta**  
Porta da usare per la connessione al server PostgreSQL.

**Database**  
Nome del database PostgreSQL.

**Uid** e **Pwd**   
**Uid** (ID utente) e **Pwd** (password) per la connessione.

### <a name="connection-string-format"></a>Formato della stringa di connessione
Di seguito è riportato il formato di una stringa di connessione tipica. 

    ```
    Driver={PostgreSQL ODBC Driver(UNICODE)};Server=<server>;Port=<port>;Database=<database>;UID=<user id>;PWD=<password>
    ```

### <a name="enter-the-connection-string"></a>Immettere la stringa di connessione
Immettere la stringa di connessione nel campo **ConnectionString** oppure il nome DSN nel campo **Dsn** nella pagina **Scelta origine dati** o **Scelta destinazione**. Dopo avere immesso la stringa di connessione, la procedura guidata analizza la stringa e visualizza le singole proprietà e i relativi valori nell'elenco.

L'esempio seguente usa questa stringa di connessione.

    ```
    Driver={PostgreSQL ODBC Driver(UNICODE)};Server=127.0.0.1;Port=5432;Database=postgres;UID=postgres;PWD=********
    ```

Di seguito è riportata la schermata che viene visualizzata dopo aver immesso la stringa di connessione.

![Connettersi a PostgreSQL con ODBC](../../integration-services/import-export-data/media/connect-to-postgresql-with-odbc.png)

## <a name="other-data-providers-and-more-info"></a>Altri provider di dati e altre informazioni
Per informazioni su come connettersi a PostgreSQL con un provider di dati non elencato, vedere [PostgreSQL connection strings](https://www.connectionstrings.com/postgresql/) (Stringhe di connessione di PostgreSQL). Questo sito di terze parti contiene anche informazioni sui provider di dati e i parametri di connessione descritti in questa pagina.

## <a name="see-also"></a>Vedere anche
[Scelta origine dati](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[Scelta destinazione](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)

