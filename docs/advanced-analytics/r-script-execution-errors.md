---
title: R lo scripting di errori e risoluzione dei problemi - servizi di SQL Server Machine Learning
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/31/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 2df4fa2fd9ef52fe5edbca9440f73f351553f1ed
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58511528"
---
# <a name="r-scripting-errors-in-sql-server"></a>Errori di script R in SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Questo articolo documenta gerrors scriptin diversi durante l'esecuzione di codice R in SQL Server. L'elenco non è completo. Sono presenti molti pacchetti e gli errori possono variare tra versioni diverse dello stesso pacchetto. Si consiglia di pubblicare gli errori di script nel [forum di Machine Learning Server](https://social.msdn.microsoft.com/Forums/en-US/home?category=MicrosoftR), che supporta l'apprendimento automatico componenti usati in R Services (In-Database), Microsoft R Client e Microsoft R Server.

**Si applica a:** SQL Server 2016 R Services, SQL Server 2017 Machine Learning Services


## <a name="valid-script-fails-in-t-sql-or-in-stored-procedures"></a>Script valido ha esito negativo in T-SQL o nelle stored procedure

Prima di eseguire il wrapping del codice R in una stored procedure, è consigliabile eseguire il codice R in un IDE esterno o in uno degli strumenti di R, ad esempio RGui o RTerm. Usando questi metodi, è possibile testare e il debug del codice tramite messaggi di errore dettagliati vengono restituiti da R.

Tuttavia, in alcuni casi il codice che funziona perfettamente nell'IDE o utilità esterna potrebbe non riuscire per l'esecuzione in una stored procedure o contesto di calcolo in un Server SQL. In questo caso, esistono una serie di problemi cercare prima che si può presupporre che il pacchetto non funziona in SQL Server.

1. Verificare se Launchpad è in esecuzione.

2. Esaminare i messaggi per verificare se i dati di input o i dati di output contengono colonne con tipi di dati incompatibili o non è supportato. Le query in un database SQL, ad esempio, restituiscono spesso valori GUID o rowguid, che non sono supportati. Per altre informazioni, vedere [tipi di dati e le librerie R](r/r-libraries-and-data-types.md).

3. Vedere le pagine della Guida per le singole funzioni R determinare se tutti i parametri sono supportati per il contesto di calcolo di SQL Server. Per la Guida di ScaleR, usare i comandi della Guida in linea di R, oppure vedere [riferimento al pacchetto](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler).

Se il runtime di R è funzionante, ma lo script restituisce errori, è consigliabile provare a debug dello script in un ambiente di sviluppo R dedicato, ad esempio R Tools per Visual Studio.

È consigliabile anche rivedere e leggermente riscrivere lo script per correggere eventuali problemi con tipi di dati che potrebbero verificarsi quando si spostano i dati tra R e il motore di database. Per altre informazioni, vedere [tipi di dati e le librerie R](r/r-libraries-and-data-types.md).

Inoltre, è possibile usare il pacchetto sqlrutils creare un bundle di script R in un formato più facilmente utilizzabile come stored procedure. Per altre informazioni, vedere:
* [pacchetto sqlrutils](r/ref-r-sqlrutils.md)
* [Creare una stored procedure con sqlrutils](r/how-to-create-a-stored-procedure-using-sqlrutils.md)

## <a name="script-returns-inconsistent-results"></a>Lo script restituisce risultati incoerenti

Gli script R possono restituire valori diversi in un contesto di SQL Server, per diversi motivi:

- Conversione implicita del tipo viene eseguita automaticamente alcuni tipi di dati, quando i dati vengono passati tra SQL Server e R. Per altre informazioni, vedere [tipi di dati e le librerie R](r/r-libraries-and-data-types.md).

- Determinare se è un fattore in numero di bit. Ad esempio, sono spesso presenti differenze nei risultati delle operazioni matematiche per librerie di punto a virgola mobile a 32 e 64 bit.

- Determinare se sono stati prodotti NaN in qualsiasi operazione. Questa operazione può invalidare i risultati.

- Piccole differenze possono risultare amplificate quando si acquisisce un reciproco di un numero quasi zero.

- Errori di arrotondamento accumulati possono causare elementi come i valori che sono minori di zero anziché zero.

## <a name="implied-authentication-for-remote-execution-via-odbc"></a>Autenticazione implicita per l'esecuzione remota tramite ODBC

Se ci si connette al [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] dei comandi di computer per eseguire R usando la **RevoScaleR** funzioni, è possibile ottenere un errore quando si utilizzano chiamate ODBC che scrivono dati sul server. Questo errore si verifica solo quando si usa l'autenticazione di Windows.

Il motivo è che gli account di lavoro che vengono creati per R Services non è autorizzato a connettersi al server. Pertanto, chiamate ODBC non possono essere eseguite automaticamente. Il problema non viene eseguito con gli account di accesso SQL perché, con gli account di accesso SQL, le credenziali vengono passate in modo esplicito dal client R all'istanza di SQL Server e quindi a ODBC. Tuttavia, usando gli account di accesso SQL è anche meno sicura rispetto all'uso di autenticazione di Windows.

Per abilitare le credenziali di Windows deve essere passato in modo sicuro da uno script che ha avviato in modalità remota, SQL Server deve emulare le proprie credenziali. Questo processo è detto _l'autenticazione implicita_. Per eseguire questa operazione, gli account di lavoro che eseguono script R o Python nel computer SQL Server devono disporre delle autorizzazioni corrette.

1. Apri [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] come amministratore nell'istanza in cui si desidera eseguire il codice R.

2. Eseguire lo script seguente. Assicurarsi di modificare il nome del gruppo utente, se è stato cambiato quello predefinito e i nomi di computer e dell'istanza.

    ```sql
    USE [master]
    GO
    
    CREATE LOGIN [computername\\SQLRUserGroup] FROM WINDOWS WITH
    DEFAULT_DATABASE=[master], DEFAULT_LANGUAGE=[language]
    GO
    ```

## <a name="avoid-clearing-the-workspace-while-youre-running-r-in-a-sql-compute-context"></a>Non deselezionare l'area di lavoro mentre in esecuzione R in un contesto di calcolo SQL

Anche se l'area di lavoro di cancellazione è comune quando si lavora nella console di R, può avere conseguenze impreviste in un database SQL di contesto di calcolo.

`revoScriptConnection` è un oggetto nell'area di lavoro di R che contiene informazioni su una sessione di R che viene chiamata da SQL Server. Tuttavia, se il codice R include un comando per cancellare l'area di lavoro (ad esempio `rm(list=ls())`), tutte le informazioni relative alla sessione e altri oggetti nell'area di lavoro R vengono cancellate.

In alternativa, evitare indiscriminato variabili e altri oggetti mentre in esecuzione R in SQL Server. È possibile eliminare variabili specifiche usando il **rimuovere** funzione:

```R
remove('name1', 'name2', ...)
```

Se sono presenti più variabili da eliminare, è consigliabile che salva i nomi delle variabili temporanee in un elenco e quindi eseguire periodicamente operazioni di garbage collection nell'elenco.



## <a name="next-steps"></a>Passaggi successivi

[Problemi noti e risoluzione dei problemi di Machine Learning Services](machine-learning-troubleshooting-faq.md)

[Raccolta dei dati per la risoluzione dei problemi di apprendimento automatico](data-collection-ml-troubleshooting-process.md)

[Domande frequenti sull'installazione e sull'aggiornamento](r/upgrade-and-installation-faq-sql-server-r-services.md)

[Risolvere i problemi di connessioni al motore del database](../database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine.md)
