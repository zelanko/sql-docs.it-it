---
title: Prompt dei comandi di installazione dei componenti di R e Python, SQL Server Machine Learning
description: Eseguire l'installazione della riga di comando di SQL Server per aggiungere linguaggio R e Python integrazione a un'istanza di motore di database di SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 6ffd4b13d5ab92187ac998fd983e8fa8416e4401
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962899"
---
# <a name="install-sql-server-machine-learning-r-and-python-components-from-the-command-line"></a>Installare i componenti di R e Python dalla riga di comando di apprendimento automatico SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Questo articolo fornisce istruzioni per la macchina di SQL Server intalling componenti dalla riga di comando di apprendimento:

+ [Istanza di nuovo nel Database](#indb)
+ [Aggiungere a un'istanza di motore di database esistente](#add-existing)
+ [Installazione invisibile all'utente](#silent)
+ [Nuovo server autonomo](#shared-feature)

È possibile specificare l'interazione invisibile all'utente, di base o completa con l'interfaccia utente di configurazione. Questo articolo integra [installare SQL Server dal Prompt dei comandi](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md), illustrando i parametri univoci per R e Python componenti di apprendimento automatico.

## <a name="pre-install-checklist"></a>Elenco di controllo pre-installazione

+ Eseguire i comandi al prompt dei comandi con privilegi elevati. 

+ Un'istanza del motore di database è necessaria per le installazioni nel database. Non è possibile installare solo le funzionalità di R o Python, sebbene sia possibile [aggiungerli in modo incrementale a un'istanza esistente](#add-existing). Se si desidera semplicemente R e Python senza il motore di database, installare il [server autonomo](#shared-feature).

+ Non installare in un cluster di failover. Il meccanismo di sicurezza utilizzato per isolare i processi R e Python non è compatibile con un ambiente cluster di failover di Windows Server.

+ Non installare un controller di dominio. La parte di servizi di Machine Learning del programma di installazione avrà esito negativo.

+ Evitare l'installazione autonoma e le istanze nel database nello stesso computer. Un server autonomo verrà si contendono le risorse stesse, compromettendo le prestazioni di entrambe le installazioni.


## <a name="command-line-arguments"></a>Argomenti della riga di comando

L'argomento di funzionalità è necessaria, perché sono termine contratti di licenza. 

In caso di installazione dal prompt dei comandi, in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è supportata la modalità non interattiva completa tramite il parametro /Q o la modalità non interattiva semplice tramite il parametro /QS. L'opzione /QS indica semplicemente lo stato di avanzamento, non accetta alcun input e non consente di visualizzare eventuali messaggi di errore. Il parametro /QS è supportato solo quando viene specificato /Action=install.

| Argomenti | Descrizione |
|-----------|-------------|
| / FEATURES = AdvancedAnalytics | Installa la versione in-database: Machine Learning Services (In-Database) di SQL Server 2017 o SQL Server 2016 R Services (In-Database).  |
| /FEATURES = SQL_INST_MR | Si applica a SQL Server 2017. Abbinato a AdvancedAnalytics. Installa la funzionalità (In-Database) R, tra cui Microsoft R Open e i pacchetti R proprietari. La funzionalità di SQL Server 2016 R Services è R sola, pertanto non presenta alcun parametro per tale versione.|
| /FEATURES = SQL_INST_MPY | Si applica a SQL Server 2017. Abbinato a AdvancedAnalytics. Installa la funzionalità di Python (In-Database), inclusi i pacchetti Python proprietari e Anaconda. |
| /FEATURES = SQL_SHARED_MR | Installa la funzionalità di R per la versione autonoma: Machine Learning Server (Standalone) di SQL Server 2017 o SQL Server 2016 R Server (Standalone). Un server autonomo è una "funzionalità condivise" non è associata a un'istanza del motore di database.|
| /FEATURES = SQL_SHARED_MPY | Si applica a SQL Server 2017. Installa la funzionalità di Python per la versione autonoma: SQL Server 2017 Machine Learning Server (Standalone). Un server autonomo è una "funzionalità condivise" non è associata a un'istanza del motore di database.|
| /IACCEPTROPENLICENSETERMS  | Indica che si hanno accettato le condizioni di licenza per l'uso di componenti di R open source. |
| /IACCEPTPYTHONLICENSETERMS | Indica che si hanno accettato le condizioni di licenza per l'uso di componenti Python. |
| /IACCEPTSQLSERVERLICENSETERMS | Indica che si hanno accettato le condizioni di licenza per l'uso di SQL Server.|
| /MRCACHEDIRECTORY | Per l'installazione offline, imposta la cartella che contiene i file CAB dei componenti R. |
| / MPYCACHEDIRECTORY | Riservato per utilizzi futuri. Utilizzare % TEMP % per archiviare i file CAB dei componenti Python per l'installazione nei computer che non dispongono di una connessione a internet. |


## <a name="indb"></a> Le installazioni di istanze nel database

Analitica nel database è disponibili per istanze del motore di database necessari per l'aggiunta di **AdvancedAnalytics** funzionalità all'installazione. È possibile installare un'istanza del motore di database con analitica avanzata, oppure [aggiungerlo a un'istanza esistente](#add-existing). 

Per visualizzare le informazioni di stato di avanzamento senza l'oggetto interattivo su schermo prompt, usare l'argomento /qs.

> [!IMPORTANT]
> Dopo l'installazione, rimangono due ulteriori passaggi di configurazione. Integrazione non è completa fino a quando non vengono eseguite queste attività. Visualizzare [attività post-installazione](#post-install) per le istruzioni.

### <a name="sql-server-2017-database-engine-advanced-analytics-with-python-and-r"></a>SQL Server 2017: motore di database, advanced analitica con Python e R

Per un'installazione simultanea dell'istanza del motore di database, specificare il nome dell'istanza e un account di accesso di amministratore (Windows). Include funzionalità per l'installazione di base e componenti del linguaggio, nonché l'accettazione di tutte le condizioni di licenza.

```cmd
Setup.exe /qs /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MR,SQL_INST_MPY
/INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="<Windows-username>" 
/IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS /IACCEPTPYTHONLICENSETERMS
```

Questo comando stesso, ma con un account di accesso di SQL Server in un motore di database tramite autenticazione mista.

```cmd
Setup.exe /q /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MR,SQL_INST_MPY
/INSTANCENAME=MSSQLSERVER /SECURITYMODE=SQL /SAPWD="%password%" /SQLSYSADMINACCOUNTS="<sql-username>" 
/IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS /IACCEPTPYTHONLICENSETERMS
```

Questo esempio è solo Python che mostra che è possibile aggiungere una sola lingua omettendo una funzionalità.

```cmd  
Setup.exe /qs /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MPY 
/INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="<username>" 
/IACCEPTSQLSERVERLICENSETERMS  /IACCEPTPYTHONLICENSETERMS
```

### <a name="sql-server-2016-database-engine-and-advanced-analytics-with-r"></a>SQL Server 2016: motore di database e analitica avanzata con R

Questo comando è identico a SQL Server 2017, ma senza gli elementi di Python, che non sono disponibili nel programma di installazione di SQL Server 2016.

```cmd  
Setup.exe /qs /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MR
/INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="<Windows-username>" 
/IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS 
```

## <a name="post-install"></a> Configurazione di post-installazione (obbligatorio)

Si applica alle installazioni solo nel database.

Al termine dell'installazione, si dispone di un'istanza del motore di database con i pacchetti R e Python, il Microsoft R e Python, Microsoft R Open, Anaconda, strumenti, esempi e script che fanno parte della distribuzione. 

Per completare l'installazione sono necessari due altre attività:

1. Riavviare il servizio motore di database.

1. Prima di poter usare la funzionalità, abilitare gli script esterni. Seguire le istruzioni in [installare SQL Server 2017 Machine Learning Services (In-Database)](sql-machine-learning-services-windows-install.md) come passaggio successivo. 

Per SQL Server 2016, usare invece questo articolo [installare SQL Server 2016 R Services (In-Database)](sql-r-services-windows-install.md).

## <a name="add-existing"></a> Aggiungere l'analitica avanzata a un'istanza di motore di database esistente

Quando si aggiunge l'analitica avanzata nel database a un'istanza di motore di database esistente, fornire il nome dell'istanza. Ad esempio, se si è precedentemente installato un motore di database di SQL Server 2017 e Python, si può utilizzare questo comando per aggiungere R.

```cmd  
Setup.exe /qs /ACTION=Install /FEATURES=SQL_INST_MR /INSTANCENAME=MSSQLSERVER 
/IACCEPTSQLSERVERLICENSETERMS  /IACCEPTROPENLICENSETERMS
```



## <a name="silent"></a> Installazione invisibile all'utente

Un'installazione invisibile all'utente elimina il controllo per i percorsi di file con estensione cab. Per questo motivo, è necessario specificare il percorso in cui devono essere decompressi file con estensione cab. Per Python, file CAB devono trovarsi nella cartella % TEMP *. Per R, è possibile impostare la cartella percorso usando è possibile nella directory temporanea per l'oggetto.
 
```cmd  
Setup.exe /q /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MR,SQL_INST_MPY 
/INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="<username>" 
/IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS /IACCEPTPYTHONLICENSETERMS 
/MRCACHEDIRECTORY=%temp% 
```

## <a name="shared-feature"></a> Installazioni di server autonomi

Un server autonomo è una "funzionalità condivise" non è associata a un'istanza del motore di database. Gli esempi seguenti illustrano la sintassi valida per entrambe le versioni.

SQL Server 2017 supporta R e Python in un server autonomo:

```cmd
Setup.exe /q /ACTION=Install /FEATURES=SQL_SHARED_MR,SQL_SHARED_MPY  
/IACCEPTROPENLICENSETERMS /IACCEPTPYTHONLICENSETERMS /IACCEPTSQLSERVERLICENSETERMS
```

SQL Server 2016 è solo R:

```cmd
Setup.exe /q /ACTION=Install /FEATURES=SQL_SHARED_MR 
/IACCEPTROPENLICENSETERMS /IACCEPTSQLSERVERLICENSETERMS
```

Al termine dell'installazione, si dispone di un server, Microsoft pacchetti, distribuzioni open source di R e Python, strumenti, esempi e script che fanno parte della distribuzione. 

Per aprire una finestra della console di R, passare a \Programmi\Microsoft SQL Server\140 (o 130) \R_SERVER\bin\x64 e fare doppio clic su **RGui.exe**. Non si ha familiarità con R? Provare a eseguire questa esercitazione: [I comandi R di base e funzioni RevoScaleR: esempi comuni 25](https://docs.microsoft.com/machine-learning-server/r/tutorial-r-to-revoscaler).

Per aprire un comando di Python, andare a \Programmi\Microsoft SQL Server\140\PYTHON_SERVER\bin\x64 e fare doppio clic su **python.exe**.

## <a name="get-help"></a>Supporto

Serve aiuto con l'installazione o aggiornamento? Per le risposte alle domande più frequenti e problemi noti, vedere l'articolo seguente:

* [Aggiornamento e installazione domande frequenti: servizi di Machine Learning](../r/upgrade-and-installation-faq-sql-server-r-services.md)

Per controllare lo stato dell'installazione dell'istanza e risolvere problemi comuni, provare questi report personalizzati.

* [Report personalizzati per SQL Server R Services](../r/monitor-r-services-using-custom-reports-in-management-studio.md)

## <a name="next-steps"></a>Passaggi successivi

Gli sviluppatori di R possono iniziare a usare alcuni semplici esempi e informazioni di base del funzionamento di R con SQL Server. Per il passaggio successivo, vedere i collegamenti seguenti:

+ [Esercitazione: Eseguire R in T-SQL](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)
+ [Esercitazione: Analitica nel database per gli sviluppatori di R](../tutorials/sqldev-in-database-r-for-sql-developers.md)

Gli sviluppatori di Python è possono imparare a usare Python con SQL Server seguendo queste esercitazioni:

+ [Esercitazione: Eseguire Python in T-SQL](../tutorials/run-python-using-t-sql.md)
+ [Esercitazione: Analitica nel database per sviluppatori Python](../tutorials/sqldev-in-database-python-for-sql-developers.md)

Per visualizzare esempi di machine learning basate su scenari reali, vedere [di Machine learning esercitazioni](../tutorials/machine-learning-services-tutorials.md).