---
title: Connettersi a un'origine dati Oracle (Importazione/Esportazione guidata SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/29/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: b0bd1f5a-34dd-4be3-9ac8-f9f87727781b
author: chugugrace
ms.author: chugu
ms.openlocfilehash: c114a5e17c95d21d999819e73dcfd53f84179802
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85773557"
---
# <a name="connect-to-an-oracle-data-source-sql-server-import-and-export-wizard"></a>Connettersi a un'origine dati Oracle (Importazione/Esportazione guidata SQL Server)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


Questo argomento illustra come connettersi a un'origine dati **Oracle** dalla pagina **Scelta origine dati** o **Scelta destinazione** dell'Importazione/Esportazione guidata SQL Server. Sono disponibili diversi provider di dati che è possibile usare per connettersi a Oracle.

> [!IMPORTANT]
> Le informazioni dettagliate sui requisiti e i prerequisiti per la connessione a un database Oracle non rientrano nell'ambito di questo articolo di Microsoft. Questo articolo presuppone che sia già stato installato il software client Oracle e che sia già possibile connettersi al database Oracle di destinazione. Per altre informazioni, contattare l'amministratore del database Oracle o consultare la documentazione di Oracle.

## <a name="connect-to-oracle-with-the-net-framework-data-provider-for-oracle"></a>Connettersi a Oracle con il provider di dati .NET Framework per Oracle
Dopo aver selezionato **Provider di dati .NET Framework per Oracle** nella pagina **Scelta origine dati** o **Scelta destinazione** della procedura guidata, viene visualizzato nella pagina un elenco raggruppato di opzioni per il provider. Molti dei nomi visualizzati sono complessi e le impostazioni non sono riconoscibili. Fortunatamente, è necessario specificare solo alcune informazioni. È possibile ignorare i valori predefiniti delle altre impostazioni.

> [!NOTE]
> Le opzioni di connessione per il provider di dati sono le stesse sia nel caso in cui Oracle rappresenti l'origine sia nel caso in cui rappresenti la destinazione. Ovvero, le opzioni visualizzate sono le stesse in entrambe le pagine **Scelta origine dati** e **Scelta destinazione** della procedura guidata.

|Informazioni obbligatorie|Proprietà Provider di dati .NET Framework per Oracle|
|---|---|
|Nome server|**Origine dati**|
|Informazioni di autenticazione (accesso)|**ID utente** e **Password** oppure **Sicurezza integrata**|
|||

Non è necessario immettere la stringa di connessione nel campo **ConnectionString** dell'elenco. Dopo avere immesso i singoli valori per il nome del server Oracle (**Origine dati**) e le informazioni di accesso, la procedura guidata assembla la stringa di connessione in base alle singole proprietà e ai relativi valori. 

![Connettersi a Oracle con il provider .NET](../../integration-services/import-export-data/media/connect-to-oracle-with-net-provider.jpg)

## <a name="connect-to-oracle-with-the-microsoft-odbc-driver-for-oracle"></a>Connettersi a Oracle con il driver ODBC di Microsoft per Oracle
I driver ODBC non sono presenti nell'elenco a discesa delle origini dati. Per connettersi con un driver ODBC, selezionare innanzitutto **Provider di dati .NET Framework per ODBC** come origine dati nella pagina **Scelta origine dati** o **Scelta destinazione**. Questo provider funge da wrapper per il driver ODBC.

Di seguito è riportata la schermata generica che viene visualizzata dopo aver selezionato il Provider di dati .NET Framework per ODBC.

![Connettersi a Oracle con ODBC (prima)](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-before.jpg)

### <a name="options-to-specify-odbc-driver-for-oracle"></a>Opzioni da specificare (Driver ODBC per Oracle)

> [!NOTE]
> Le opzioni di connessione per il provider di dati e il driver ODBC sono le stesse sia nel caso in cui Oracle rappresenti l'origine sia nel caso in cui rappresenti la destinazione. Ovvero, le opzioni visualizzate sono le stesse in entrambe le pagine **Scelta origine dati** e **Scelta destinazione** della procedura guidata.

Per connettersi a Oracle con il driver ODBC per Oracle, assemblare una stringa di connessione che includa le impostazioni seguenti e i relativi valori. Il formato di una stringa di connessione completa segue immediatamente l'elenco di impostazioni.

> [!TIP]
> Ottenere informazioni per assemblare la stringa di connessione più adatta. In alternativa, anziché specificare una stringa di connessione, immettere un DSN esistente (nome dell'origine dati) o crearne uno nuovo. Per altre informazioni su queste opzioni, vedere [Connettersi a un'origine dati ODBC](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md).

**Driver**  
Nome del driver ODBC, **Microsoft ODBC per Oracle**.

**Server**  
Nome del server Oracle. 

**Uid** e **Pwd**   
ID utente e password per la connessione.

### <a name="connection-string-format"></a>Formato della stringa di connessione
Di seguito è riportato il formato di una stringa di connessione tipica.

```console
Driver={Microsoft ODBC for Oracle};Server=myServerAddress;Uid=myUsername;Pwd=myPassword;
```

### <a name="enter-the-connection-string"></a>Immettere la stringa di connessione
Immettere la stringa di connessione nel campo **ConnectionString** oppure il nome DSN nel campo **Dsn** nella pagina **Scelta origine dati** o **Scelta destinazione**. Dopo avere immesso la stringa di connessione, la procedura guidata analizza la stringa e visualizza le singole proprietà e i relativi valori nell'elenco.

Di seguito è riportata la schermata che viene visualizzata dopo aver immesso la stringa di connessione.

![Connettersi a Oracle con ODBC](../../integration-services/import-export-data/media/connect-to-oracle-with-odbc.jpg)

## <a name="whats-my-oracle-server-name"></a>Individuare il nome del server Oracle
Eseguire una delle query seguenti per ottenere il nome del server Oracle.

`SELECT host_name FROM v$instance`

o

`SELECT sys_context('USERENV','SERVER_HOST') FROM dual`

## <a name="other-data-providers-and-more-info"></a>Altri provider di dati e altre informazioni
Per informazioni su come connettersi a Oracle con un provider di dati non elencato, vedere [Oracle connection strings](https://www.connectionstrings.com/oracle/) (Stringhe di connessione di Oracle). Questo sito di terze parti contiene anche informazioni sui provider di dati e i parametri di connessione descritti in questa pagina.

## <a name="see-also"></a>Vedere anche
[Scelta origine dati](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[Scegliere una destinazione](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)

