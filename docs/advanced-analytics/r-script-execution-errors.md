---
title: Errori e risoluzione dei problemi di script R
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/31/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 268b3df72d468170fbefae2557892c49fd15515c
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/24/2019
ms.locfileid: "68470301"
---
# <a name="r-scripting-errors-in-sql-server"></a>Errori di script R in SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Questo articolo documenta diversi scriptin gerrors quando si esegue il codice R in SQL Server. L'elenco non è completo. Sono presenti molti pacchetti e gli errori possono variare tra le versioni dello stesso pacchetto. Si consiglia di pubblicare errori di script nel [forum Machine Learning server](https://social.msdn.microsoft.com/Forums/en-US/home?category=MicrosoftR), che supporta i componenti di Machine Learning usati in R Services (in-database), Microsoft R Client e Microsoft R server.

**Si applica a:** SQL Server 2016 R Services, SQL Server 2017 Machine Learning Services


## <a name="valid-script-fails-in-t-sql-or-in-stored-procedures"></a>Errore di script valido in T-SQL o nelle stored procedure

Prima di eseguire il wrapping del codice R in una stored procedure, è consigliabile eseguire il codice R in un IDE esterno o in uno degli strumenti R, ad esempio RTerm o RGui. Usando questi metodi, è possibile testare ed eseguire il debug del codice usando i messaggi di errore dettagliati restituiti da R.

Tuttavia, a volte il codice che funziona perfettamente in un IDE o un'utilità esterna potrebbe non essere eseguito in un stored procedure o in un contesto di calcolo SQL Server. In tal caso, è possibile che si verifichi una serie di problemi prima di poter presupporre che il pacchetto non funzioni in SQL Server.

1. Controllare se Launchpad è in esecuzione.

2. Esaminare i messaggi per verificare se i dati di input o di output contengono colonne con tipi di dati incompatibili o non supportati. Ad esempio, le query su un database SQL spesso restituiscono GUID o ROWGUID, entrambe non supportate. Per altre informazioni, vedere [librerie R e tipi di dati](r/r-libraries-and-data-types.md).

3. Esaminare le pagine della Guida per le singole funzioni R per determinare se tutti i parametri sono supportati per il SQL Server contesto di calcolo. Per la guida scaler, usare i comandi della Guida di R inline o vedere il [riferimento al pacchetto](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler).

Se il runtime di R è funzionante ma lo script restituisce errori, è consigliabile provare a eseguire il debug dello script in un ambiente di sviluppo R dedicato, ad esempio R Tools per Visual Studio.

Si consiglia inoltre di rivedere e riscrivere leggermente lo script per correggere eventuali problemi con i tipi di dati che possono verificarsi quando si spostano i dati tra R e il motore di database. Per altre informazioni, vedere [librerie R e tipi di dati](r/r-libraries-and-data-types.md).

Inoltre, è possibile usare il pacchetto sqlrutils per aggregare lo script R in un formato più facilmente utilizzato come stored procedure. Per altre informazioni, vedere:
* [pacchetto sqlrutils](r/ref-r-sqlrutils.md)
* [Creare una stored procedure usando sqlrutils](r/how-to-create-a-stored-procedure-using-sqlrutils.md)

## <a name="script-returns-inconsistent-results"></a>Lo script restituisce risultati incoerenti

Gli script R possono restituire valori diversi in un contesto di SQL Server, per diversi motivi:

- La conversione implicita dei tipi viene eseguita automaticamente su alcuni tipi di dati, quando i dati vengono passati tra SQL Server e R. Per altre informazioni, vedere [librerie R e tipi di dati](r/r-libraries-and-data-types.md).

- Determinare se bit è un fattore. Spesso, ad esempio, esistono differenze nei risultati delle operazioni matematiche per le librerie a virgola mobile a 32 bit e 64 bit.

- Determinare se NaNs sono stati prodotti in qualsiasi operazione. Questa operazione può invalidare i risultati.

- È possibile amplificare piccole differenze quando si accetta una reciproca di un numero vicino a zero.

- Gli errori di arrotondamento accumulati possono causare elementi come valori minori di zero anziché zero.

## <a name="implied-authentication-for-remote-execution-via-odbc"></a>Autenticazione implicita per l'esecuzione remota tramite ODBC

Se ci si connette al [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] computer per eseguire i comandi R usando le funzioni **RevoScaleR** , è possibile che si ottenga un errore quando si usano chiamate ODBC che scrivono i dati nel server. Questo errore si verifica solo quando si usa l'autenticazione di Windows.

Il motivo è che gli account di lavoro creati per R Services non dispongono dell'autorizzazione per la connessione al server. Non è pertanto possibile eseguire chiamate ODBC per conto dell'utente. Il problema non si verifica con gli account di accesso SQL perché, con gli account di accesso SQL, le credenziali vengono passate in modo esplicito dal client R all'istanza di SQL Server e quindi a ODBC. Tuttavia, l'utilizzo di account di accesso SQL è anche meno sicuro rispetto all'utilizzo dell'autenticazione di Windows.

Per consentire il passaggio sicuro delle credenziali di Windows da uno script avviato in modalità remota, SQL Server necessario emulare le credenziali. Questo processo è definito _autenticazione implicita_. Per eseguire questa operazione, gli account di lavoro che eseguono script R o Python nel computer SQL Server devono disporre delle autorizzazioni corrette.

1. Aprire [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] come amministratore nell'istanza in cui si vuole eseguire il codice R.

2. Eseguire lo script seguente. Assicurarsi di modificare il nome del gruppo di utenti, se è stato modificato il valore predefinito e i nomi del computer e dell'istanza.

    ```sql
    USE [master]
    GO
    
    CREATE LOGIN [computername\\SQLRUserGroup] FROM WINDOWS WITH
    DEFAULT_DATABASE=[master], DEFAULT_LANGUAGE=[language]
    GO
    ```

## <a name="avoid-clearing-the-workspace-while-youre-running-r-in-a-sql-compute-context"></a>Evitare di cancellare l'area di lavoro durante l'esecuzione di R in un contesto di calcolo SQL

Sebbene la cancellazione dell'area di lavoro sia comune quando si usa la console di R, può avere conseguenze impreviste in un contesto di calcolo SQL.

`revoScriptConnection`è un oggetto nell'area di lavoro R che contiene informazioni su una sessione R chiamata da SQL Server. Tuttavia, se il codice R include un comando per cancellare l'area di lavoro, `rm(list=ls())`ad esempio, vengono cancellate anche tutte le informazioni sulla sessione e sugli altri oggetti nell'area di lavoro r.

Come soluzione alternativa, evitare la cancellazione indiscriminata di variabili e altri oggetti durante l'esecuzione di R in SQL Server. È possibile eliminare variabili specifiche usando la funzione **Remove** :

```R
remove('name1', 'name2', ...)
```

Se sono presenti più variabili da eliminare, è consigliabile salvare i nomi delle variabili temporanee in un elenco e quindi eseguire periodicamente operazioni di Garbage Collection nell'elenco.



## <a name="next-steps"></a>Passaggi successivi

[Machine Learning Services risoluzione dei problemi e problemi noti](machine-learning-troubleshooting-faq.md)

[Raccolta di dati per la risoluzione dei problemi di Machine Learning](data-collection-ml-troubleshooting-process.md)

[Domande frequenti sull'installazione e sull'aggiornamento](r/upgrade-and-installation-faq-sql-server-r-services.md)

[Risolvere i problemi delle connessioni al motore di database](../database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine.md)
