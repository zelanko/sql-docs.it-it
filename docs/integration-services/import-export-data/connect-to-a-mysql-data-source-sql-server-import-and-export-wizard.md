---
title: Connettersi a un'origine dati MySQL (Importazione/Esportazione guidata SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/20/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 3d7c5a38-18d3-4cc9-a241-04422cb250d3
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 9fc1128ff50a6b5f6fbb459dca23f518cbcd4f26
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/26/2019
ms.locfileid: "71285688"
---
# <a name="connect-to-a-mysql-data-source-sql-server-import-and-export-wizard"></a>Connettersi a un'origine dati MySQL (Importazione/Esportazione guidata SQL Server)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


Questo argomento illustra come connettersi a un'origine dati **MySQL** dalla pagina **Scelta origine dati** o **Scelta destinazione** dell'Importazione/Esportazione guidata SQL Server. Sono disponibili diversi provider di dati che è possibile usare per connettersi a MySQL.

> [!IMPORTANT]
> Le informazioni dettagliate sui requisiti e i prerequisiti per la connessione a un database MySQL non rientrano nell'ambito di questo articolo di Microsoft. Questo articolo presuppone che sia già stato installato il software client MySQL e che sia già possibile connettersi al database MySQL di destinazione. Per altre informazioni, contattare l'amministratore del database MySQL o consultare la documentazione di MySQL.

## <a name="get-the-mysql-connectors"></a>Ottenere i connettori MySQL
Scaricare i provider e i driver descritti in questo argomento dalla pagina [MySQL Connectors](https://dev.mysql.com/downloads/connector/) (Connettori MySQL).

## <a name="connect-to-mysql-with-the-net-framework-data-provider-for-mysql"></a>Connettersi a MySQL con il provider di dati .NET Framework per MySQL
Dopo aver selezionato **Provider di dati .NET Framework per MySQL** nella pagina **Scelta origine dati** o **Scelta destinazione** della procedura guidata, viene visualizzato nella pagina un elenco raggruppato di opzioni per il provider. Molti dei nomi visualizzati sono complessi e le impostazioni non sono riconoscibili. Fortunatamente, è necessario specificare solo alcune informazioni. È possibile ignorare i valori predefiniti delle altre impostazioni.

> [!NOTE]
> Le opzioni di connessione per il provider di dati sono le stesse sia nel caso in cui MySQL rappresenti l'origine sia nel caso in cui rappresenti la destinazione. Ovvero, le opzioni visualizzate sono le stesse in entrambe le pagine **Scelta origine dati** e **Scelta destinazione** della procedura guidata.

|Informazioni obbligatorie|Proprietà Provider di dati .NET Framework per MySQL|
|---|---|
|Nome server|**Server**|
|Nome database|**Database**|
|Informazioni di autenticazione (accesso)|**ID utente** e **Password**|

Non è necessario immettere la stringa di connessione nel campo **ConnectionString** dell'elenco. Dopo avere immesso i singoli valori per il nome del server MySQL (**Server**) e le informazioni di accesso, la procedura guidata assembla la stringa di connessione in base alle singole proprietà e ai relativi valori. 

![Connettersi a MySQL con il provider .NET, 1 di 2](../../integration-services/import-export-data/media/connect-to-mysql-with-the-net-provider-1-of-2.png)

![Connettersi a MySQL con il provider .NET, 2 di 2](../../integration-services/import-export-data/media/connect-to-mysql-with-the-net-provider-2-of-2.png)

## <a name="connect-to-mysql-with-the-mysql-odbc-driver"></a>Connettersi a MySQL con il driver ODBC per MySQL
I driver ODBC non sono presenti nell'elenco a discesa delle origini dati. Per connettersi con un driver ODBC, selezionare innanzitutto **Provider di dati .NET Framework per ODBC** come origine dati nella pagina **Scelta origine dati** o **Scelta destinazione**. Questo provider funge da wrapper per il driver ODBC.

Di seguito è riportata la schermata generica che viene visualizzata dopo aver selezionato il Provider di dati .NET Framework per ODBC.

![Connettersi a SQL con ODBC (prima)](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-before.jpg)

### <a name="options-to-specify-mysql-odbc-driver"></a>Opzioni da specificare (Driver ODBC MySQL)

> [!NOTE]
> Le opzioni di connessione per il provider di dati e il driver ODBC sono le stesse sia nel caso in cui MySQL rappresenti l'origine sia nel caso in cui rappresenti la destinazione. Ovvero, le opzioni visualizzate sono le stesse in entrambe le pagine **Scelta origine dati** e **Scelta destinazione** della procedura guidata.

Per connettersi a MySQL con il driver ODBC MySQL, assemblare una stringa di connessione che includa le impostazioni seguenti e i relativi valori. Il formato di una stringa di connessione completa segue immediatamente l'elenco di impostazioni.

> [!TIP]
> Ottenere informazioni per assemblare la stringa di connessione più adatta. In alternativa, anziché specificare una stringa di connessione, immettere un DSN esistente (nome dell'origine dati) o crearne uno nuovo. Per altre informazioni su queste opzioni, vedere [Connettersi a un'origine dati ODBC](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md).

**Driver**  
Nome del driver ODBC.

**Server**  
Nome del server MySQL. 

**Database**  
Nome del database MySQL.

**UID** e **PWD**   
ID utente e password per la connessione.

### <a name="connection-string-format"></a>Formato della stringa di connessione
Di seguito è riportato il formato di una stringa di connessione tipica.

    ```
    Driver={MySQL ODBC 5.3 Unicode Driver};Server=<server>;Database=<database>;UID=<user id>;PWD=<password>
    ```

### <a name="enter-the-connection-string"></a>Immettere la stringa di connessione
Immettere la stringa di connessione nel campo **ConnectionString** oppure il nome DSN nel campo **Dsn** nella pagina **Scelta origine dati** o **Scelta destinazione**. Dopo avere immesso la stringa di connessione, la procedura guidata analizza la stringa e visualizza le singole proprietà e i relativi valori nell'elenco.

L'esempio seguente usa questa stringa di connessione.

    ```
    Driver={MySQL ODBC 5.3 Unicode Driver};Server=127.0.0.1;Database=world;UID=root;PWD=********
    ```

Di seguito è riportata la schermata che viene visualizzata dopo aver immesso la stringa di connessione.

![Connettersi a MySQL con ODBC](../../integration-services/import-export-data/media/connect-to-mysql-with-odbc.png)

## <a name="other-data-providers-and-more-info"></a>Altri provider di dati e altre informazioni
Per informazioni su come connettersi a MySQL con un provider di dati non elencato, vedere [MySQL connection strings](https://www.connectionstrings.com/mysql/) (Stringhe di connessione di MySQL). Questo sito di terze parti contiene anche informazioni sui provider di dati e i parametri di connessione descritti in questa pagina.

## <a name="see-also"></a>Vedere anche
[Scelta origine dati](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[Scelta destinazione](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)

