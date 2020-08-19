---
description: Connettersi a un'origine dati SQL Server (Importazione/Esportazione guidata SQL Server)
title: Connettersi a un'origine dati SQL Server (Importazione/Esportazione guidata SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/29/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 386cedbb-fae5-45ce-9363-c4a417f80a2f
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 87d7a1a9132d4a41bdc73100b4f86d51de5c6d08
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88495580"
---
# <a name="connect-to-a-sql-server-data-source-sql-server-import-and-export-wizard"></a>Connettersi a un'origine dati SQL Server (Importazione/Esportazione guidata SQL Server)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


Questo argomento illustra come connettersi a un'origine dati **Microsoft SQL Server** dalla pagina **Scelta origine dati** o **Scelta destinazione** dell'Importazione/Esportazione guidata SQL Server. Sono disponibili diversi provider di dati che è possibile usare per connettersi a SQL Server.

> [!TIP]
> Se si usa una rete con più server, può risultare più semplice immettere il nome del server anziché espandere l'elenco a discesa dei server. Se si fa clic sull'elenco a discesa, la ricerca di tutti i server disponibili nella rete può richiedere molto tempo ed è possibile che il nome del server desiderato non sia incluso nei risultati.

## <a name="connect-to-sql-server-with-the-net-framework-data-provider-for-sql-server"></a>Connettersi a SQL Server con il provider di dati .NET Framework per SQL Server 
Dopo aver selezionato **Provider di dati .NET Framework per SQL Server** nella pagina **Scelta origine dati** o **Scelta destinazione** della procedura guidata, viene visualizzato nella pagina un elenco raggruppato di opzioni per il provider. Molti dei nomi visualizzati sono complessi e le impostazioni non sono riconoscibili. Fortunatamente, per connettersi a qualsiasi database aziendale è in genere necessario specificare solo alcune informazioni. È possibile ignorare i valori predefiniti delle altre impostazioni.

> [!NOTE]
> Le opzioni di connessione per il provider di dati sono le stesse sia nel caso in cui SQL Server rappresenti l'origine sia nel caso in cui rappresenti la destinazione. Ovvero, le opzioni visualizzate sono le stesse in entrambe le pagine **Scelta origine dati** e **Scelta destinazione** della procedura guidata.

|Informazioni obbligatorie|Proprietà Provider di dati .NET Framework per SQL Server|
|---|---|
|Authentication|**NotSpecified** come valore predefinito per "Sicurezza integrata". In alternativa, è possibile scegliere un'altra modalità di autenticazione. Non è supportato il valore "Autenticazione interattiva di Active Directory". |
|Nome server|**Origine dati**|
|Informazioni di autenticazione (accesso)|**Sicurezza integrata** oppure **ID utente** e **Password**<br/>Per visualizzare un elenco a discesa dei database nel server, è necessario innanzitutto specificare informazioni di accesso valide.|
|Nome database|**Catalogo iniziale**|

![Connettersi a SQL con il provider .NET](../../integration-services/import-export-data/media/connect-to-sql-with-net-provider.jpg)

### <a name="options-to-specify-net-framework-data-provider-for-sql-server"></a>Opzioni da specificare (Provider di dati .NET Framework per SQL Server)

> [!NOTE]
> Le opzioni di connessione per il provider di dati sono le stesse sia nel caso in cui SQL Server rappresenti l'origine sia nel caso in cui rappresenti la destinazione. Ovvero, le opzioni visualizzate sono le stesse in entrambe le pagine **Scelta origine dati** e **Scelta destinazione** della procedura guidata.

**Origine dati**  
 Immettere il nome o l'indirizzo IP del server di origine o destinazione oppure selezionare un server dall'elenco a discesa.  
 
 Per specificare una porta TCP non standard, digitare una virgola dopo il nome o l'indirizzo IP del server e quindi digitare il numero di porta.
 
 **Catalogo iniziale**  
 Immettere il nome del database di origine o destinazione oppure selezionare un database dall'elenco a discesa.  
  
 **Sicurezza integrata**  
 Specificare **True** per connettersi con l'autenticazione integrata di Windows (scelta consigliata) oppure **False** per connettersi con l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se si specifica **False**, è necessario immettere un ID utente e una password. Il valore predefinito è **False**.  
  
 **ID utente**  
 Se si usa l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], immettere un nome utente.  
  
 **Password**  
 Se si usa l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], immettere la password.  

## <a name="connect-to-sql-server-with-the-odbc-driver-for-sql-server"></a>Connettersi a SQL Server con il driver ODBC per SQL Server 
I driver ODBC non sono presenti nell'elenco a discesa delle origini dati. Per connettersi con un driver ODBC, selezionare innanzitutto **Provider di dati .NET Framework per ODBC** come origine dati. Questo provider funge da wrapper per il driver ODBC.

> [!TIP]
> **Ottenere il driver più recente**. Scaricare [Microsoft ODBC Driver for SQL Server](https://aka.ms/downloadmsodbcsql).

Di seguito è riportata la schermata generica che viene visualizzata dopo aver selezionato il Provider di dati .NET Framework per ODBC.

![Connettersi a SQL con ODBC (prima)](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-before.jpg)

### <a name="options-to-specify-odbc-driver-for-sql-server"></a>Opzioni da specificare (Driver ODBC per SQL Server)

> [!NOTE]
> Le opzioni di connessione per il driver ODBC sono le stesse sia nel caso in cui SQL Server rappresenti l'origine sia nel caso in cui rappresenti la destinazione. Ovvero, le opzioni visualizzate sono le stesse in entrambe le pagine **Scelta origine dati** e **Scelta destinazione** della procedura guidata.

Per connettersi a SQL Server con il driver ODBC più recente, assemblare una stringa di connessione che includa le impostazioni seguenti e i relativi valori. Il formato di una stringa di connessione completa segue immediatamente l'elenco di impostazioni.

> [!TIP]
> Ottenere informazioni per assemblare la stringa di connessione più adatta. In alternativa, anziché specificare una stringa di connessione, immettere un DSN esistente (nome dell'origine dati) o crearne uno nuovo. Per altre informazioni su queste opzioni, vedere [Connettersi a un'origine dati ODBC](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md).

**Driver**  
Nome del driver ODBC. Il nome è diverso a seconda della versione del driver.

**Server**  
Nome del server SQL Server.

**Database**  
Nome del database.  

**Trusted_Connection** oppure **Uid** e **Pwd**  
Specificare **Trusted_Connection=Yes** per connettersi con l'autenticazione integrata di Windows oppure specificare **Uid** (ID utente) e **Pwd** (password) per connettersi con l'autenticazione di SQL Server.

### <a name="connection-string-format"></a>Formato della stringa di connessione
Di seguito è riportato il formato di una stringa di connessione che usa l'autenticazione integrata di Windows.

`Driver={ODBC Driver 13 for SQL Server};server=<server>;database=<database>;trusted_connection=Yes;`

Di seguito è riportato il formato di una stringa di connessione che usa l'autenticazione di SQL Server anziché l'autenticazione integrata di Windows.

`Driver={ODBC Driver 13 for SQL Server};server=<server>;database=<database>;uid=<user id>;pwd=<password>;`

### <a name="enter-the-connection-string"></a>Immettere la stringa di connessione
Immettere la stringa di connessione nel campo **ConnectionString** oppure il nome DSN nel campo **Dsn** nella pagina **Scelta origine dati** o **Scelta destinazione**. Dopo avere immesso la stringa di connessione, la procedura guidata analizza la stringa e visualizza le singole proprietà e i relativi valori nell'elenco.

L'esempio seguente usa questa stringa di connessione.

`Driver={ODBC Driver 13 for SQL Server};server=localhost;database=WideWorldImporters;trusted_connection=Yes;`

Di seguito è riportata la schermata che viene visualizzata dopo aver immesso la stringa di connessione.

![Connettersi a SQL con ODBC (dopo)](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-after.jpg)

## <a name="connect-to-sql-server-with-the-microsoft-ole-db-provider-for-sql-server-or-sql-server-native-client"></a>Connettersi a SQL Server con il provider Microsoft OLE DB per SQL Server o SQL Server Native Client

> [!IMPORTANT]
> Il provider Microsoft OLE DB per SQL Server e SQL Server Native Client non sono supportati nelle versioni di SQL Server successive alla versione SQL Server 2012. In alternativa, usare il driver ODBC. Per altre informazioni sulla transizione al driver ODBC, vedere i post di blog seguenti.
>   -   [Microsoft is Aligning with ODBC for Native Relational Data Access](https://blogs.msdn.microsoft.com/sqlnativeclient/2011/08/29/microsoft-is-aligning-with-odbc-for-native-relational-data-access/) (Microsoft si allinea a ODBC per l'accesso ai dati relazionali nativi)
>   -   [Introducing the new Microsoft ODBC Drivers for SQL Server](https://blogs.msdn.microsoft.com/sqlnativeclient/2013/01/23/introducing-the-new-microsoft-odbc-drivers-for-sql-server/) (Introduzione ai nuovi driver ODBC Microsoft per SQL Server)

## <a name="other-data-providers-and-more-info"></a>Altri provider di dati e altre informazioni
Per informazioni su come connettersi a SQL Server con un provider di dati non elencato, vedere [SQL Server connection strings](https://www.connectionstrings.com/sql-server/) (Stringhe di connessione di SQL Server). Questo sito di terze parti contiene anche informazioni sui provider di dati e i parametri di connessione descritti in questa pagina.

## <a name="see-also"></a>Vedere anche
[Scelta origine dati](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[Scegliere una destinazione](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)

