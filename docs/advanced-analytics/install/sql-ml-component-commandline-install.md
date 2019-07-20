---
title: Installazione del prompt dei comandi di componenti R e Python
description: Eseguire SQL Server installazione della riga di comando per aggiungere il linguaggio R e l'integrazione di Python a un'istanza del motore di database SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 86f17e9775108e9b075b3733df59202654888d62
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345033"
---
# <a name="install-sql-server-machine-learning-r-and-python-components-from-the-command-line"></a>Installare SQL Server componenti R e Python di Machine Learning dalla riga di comando
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Questo articolo fornisce istruzioni per l'intalling di SQL Server componenti di machine learning da una riga di comando:

+ [Nuova istanza nel database](#indb)
+ [Aggiungi a un'istanza del motore di database esistente](#add-existing)
+ [Installazione invisibile all'utente](#silent)
+ [Nuovo server autonomo](#shared-feature)

È possibile specificare un'interazione invisibile, di base o completa con l'interfaccia utente del programma di installazione. Questo articolo integra l' [installazione SQL Server dal prompt dei comandi](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md), coprendo i parametri univoci per i componenti di R e Python Machine Learning.

## <a name="pre-install-checklist"></a>Elenco di controllo pre-installazione

+ Eseguire comandi da un prompt dei comandi con privilegi elevati. 

+ Un'istanza del motore di database è necessaria per le installazioni nel database. Non è possibile installare solo le funzionalità di R o Python, sebbene sia possibile [aggiungerle in modo incrementale a un'istanza esistente](#add-existing). Se si vuole solo R e Python senza il motore di database, installare il [server autonomo](#shared-feature).

+ Non installare in un cluster di failover. Il meccanismo di sicurezza usato per isolare i processi R e Python non è compatibile con un ambiente cluster di failover di Windows Server.

+ Non installare in un controller di dominio. Il Machine Learning Services parte del programma di installazione avrà esito negativo.

+ Evitare di installare istanze autonome e nel database nello stesso computer. Un server autonomo eseguirà la competizione per le stesse risorse, compromettendo le prestazioni di entrambe le installazioni.


## <a name="command-line-arguments"></a>Argomenti della riga di comando

L'argomento FEATUREs è obbligatorio, così come i contratti di licenza. 

In caso di installazione dal prompt dei comandi, in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è supportata la modalità non interattiva completa tramite il parametro /Q o la modalità non interattiva semplice tramite il parametro /QS. L'opzione /QS indica semplicemente lo stato di avanzamento, non accetta alcun input e non consente di visualizzare eventuali messaggi di errore. Il parametro /QS è supportato solo quando viene specificato /Action=install.

| Argomenti | Descrizione |
|-----------|-------------|
| /FEATURES = AdvancedAnalytics | Installa la versione nel database: SQL Server 2017 Machine Learning Services (in-database) o SQL Server 2016 R Services (in-database).  |
| /FEATURES = SQL_INST_MR | Si applica solo a SQL Server 2017. Associare questo insieme a AdvancedAnalytics. Installa la funzionalità R (in-database), inclusi Microsoft R Open e i pacchetti R proprietari. La funzionalità SQL Server 2016 R Services è solo R, quindi non esiste alcun parametro per tale versione.|
| /FEATURES = SQL_INST_MPY | Si applica solo a SQL Server 2017. Associare questo insieme a AdvancedAnalytics. Installa la funzionalità Python (in-database), inclusi Anaconda e i pacchetti Python proprietari. |
| /FEATURES = SQL_SHARED_MR | Installa la funzionalità R per la versione autonoma: SQL Server 2017 Machine Learning Server (autonomo) o SQL Server 2016 R Server (standalone). Un server autonomo è una "funzionalità condivisa" non associata a un'istanza del motore di database.|
| /FEATURES = SQL_SHARED_MPY | Si applica solo a SQL Server 2017. Installa la funzionalità Python per la versione autonoma: SQL Server 2017 Machine Learning Server (standalone). Un server autonomo è una "funzionalità condivisa" non associata a un'istanza del motore di database.|
| /IACCEPTROPENLICENSETERMS  | Indica che sono state accettate le condizioni di licenza per l'uso dei componenti R Open Source. |
| /IACCEPTPYTHONLICENSETERMS | Indica che sono state accettate le condizioni di licenza per l'uso dei componenti di Python. |
| /IACCEPTSQLSERVERLICENSETERMS | Indica che sono state accettate le condizioni di licenza per l'utilizzo di SQL Server.|
| /MRCACHEDIRECTORY | Per l'installazione offline, imposta la cartella che contiene i file CAB del componente R. |
| /MPYCACHEDIRECTORY | Riservato per utilizzi futuri. Utilizzare% TEMP% per archiviare i file CAB dei componenti Python per l'installazione nei computer che non dispongono di una connessione Internet. |


## <a name="indb"></a>Installazioni di istanze nel database

Le analisi nel database sono disponibili per le istanze del motore di database, necessarie per aggiungere la funzionalità **AdvancedAnalytics** all'installazione. È possibile installare un'istanza del motore di database con Advanced Analytics o [aggiungerla a un'istanza esistente](#add-existing). 

Per visualizzare le informazioni sullo stato di avanzamento senza la richiesta interattiva sullo schermo, usare l'argomento/QS.

> [!IMPORTANT]
> Dopo l'installazione, restano due passaggi di configurazione aggiuntivi. L'integrazione non è completa fino a quando non vengono eseguite queste attività. Per istruzioni, vedere [attività di post-installazione](#post-install) .

### <a name="sql-server-2017-database-engine-advanced-analytics-with-python-and-r"></a>SQL Server 2017: motore di database, Advanced Analytics con Python e R

Per un'installazione simultanea dell'istanza del motore di database, specificare il nome dell'istanza e un account di accesso Administrator (Windows). Includere le funzionalità per l'installazione dei componenti di base e della lingua, oltre all'accettazione di tutte le condizioni di licenza.

```cmd
Setup.exe /qs /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MR,SQL_INST_MPY
/INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="<Windows-username>" 
/IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS /IACCEPTPYTHONLICENSETERMS
```

Questo è lo stesso comando, ma con un SQL Server account di accesso in un motore di database usando l'autenticazione mista.

```cmd
Setup.exe /q /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MR,SQL_INST_MPY
/INSTANCENAME=MSSQLSERVER /SECURITYMODE=SQL /SAPWD="%password%" /SQLSYSADMINACCOUNTS="<sql-username>" 
/IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS /IACCEPTPYTHONLICENSETERMS
```

Questo esempio è solo Python, mostrando che è possibile aggiungere una lingua omettendo una funzionalità.

```cmd  
Setup.exe /qs /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MPY 
/INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="<username>" 
/IACCEPTSQLSERVERLICENSETERMS  /IACCEPTPYTHONLICENSETERMS
```

### <a name="sql-server-2016-database-engine-and-advanced-analytics-with-r"></a>SQL Server 2016: motore di database e Advanced Analytics con R

Questo comando è identico a SQL Server 2017, ma senza gli elementi Python, che non sono disponibili nel programma di installazione di SQL Server 2016.

```cmd  
Setup.exe /qs /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MR
/INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="<Windows-username>" 
/IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS 
```

## <a name="post-install"></a>Configurazione successiva all'installazione (obbligatorio)

Si applica solo alle installazioni nel database.

Al termine dell'installazione, si disporrà di un'istanza del motore di database con R e Python, i pacchetti Microsoft R e Python, Microsoft R Open, Anaconda, strumenti, esempi e script che fanno parte della distribuzione. 

Per completare l'installazione sono necessarie altre due attività:

1. Riavviare il servizio motore di database.

1. Abilitare gli script esterni prima di poter usare la funzionalità. Seguire le istruzioni riportate in [installare SQL Server 2017 Machine Learning Services (in-database)](sql-machine-learning-services-windows-install.md) come passaggio successivo. 

Per SQL Server 2016, usare questo articolo per [installare SQL Server 2016 R Services (in-database)](sql-r-services-windows-install.md).

## <a name="add-existing"></a>Aggiungi analisi avanzata a un'istanza del motore di database esistente

Quando si aggiunge l'analisi avanzata nel database a un'istanza del motore di database esistente, specificare il nome dell'istanza. Ad esempio, se in precedenza è stato installato un motore di database SQL Server 2017 e Python, è possibile usare questo comando per aggiungere R.

```cmd  
Setup.exe /qs /ACTION=Install /FEATURES=SQL_INST_MR /INSTANCENAME=MSSQLSERVER 
/IACCEPTSQLSERVERLICENSETERMS  /IACCEPTROPENLICENSETERMS
```



## <a name="silent"></a>Installazione invisibile all'utente

Un'installazione invisibile all'utente evita la verifica dei percorsi dei file con estensione cab. Per questo motivo, è necessario specificare il percorso in cui devono essere decompressi i file con estensione cab. Per Python, i file CAB devono trovarsi in% TEMP *. Per R, è possibile impostare il percorso della cartella usando la directory Temp.
 
```cmd  
Setup.exe /q /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MR,SQL_INST_MPY 
/INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="<username>" 
/IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS /IACCEPTPYTHONLICENSETERMS 
/MRCACHEDIRECTORY=%temp% 
```

## <a name="shared-feature"></a>Installazioni Server autonome

Un server autonomo è una "funzionalità condivisa" non associata a un'istanza del motore di database. Negli esempi seguenti viene illustrata la sintassi valida per entrambe le versioni.

SQL Server 2017 supporta Python e R in un server autonomo:

```cmd
Setup.exe /q /ACTION=Install /FEATURES=SQL_SHARED_MR,SQL_SHARED_MPY  
/IACCEPTROPENLICENSETERMS /IACCEPTPYTHONLICENSETERMS /IACCEPTSQLSERVERLICENSETERMS
```

SQL Server 2016 è solo R:

```cmd
Setup.exe /q /ACTION=Install /FEATURES=SQL_SHARED_MR 
/IACCEPTROPENLICENSETERMS /IACCEPTSQLSERVERLICENSETERMS
```

Al termine dell'installazione, sono disponibili un server, pacchetti Microsoft, distribuzioni open source di R e Python, strumenti, esempi e script che fanno parte della distribuzione. 

Per aprire una finestra della console R, passare a \Programmi\microsoft SQL Server\140 (o 130) \R_SERVER\bin\x64 e fare doppio clic su **RGui. exe**. Non si ha familiarità con R? Provare questa esercitazione: [Comandi R di base e funzioni RevoScaleR: 25 esempi](https://docs.microsoft.com/machine-learning-server/r/tutorial-r-to-revoscaler)comuni.

Per aprire un comando Python, passare a \Programmi\microsoft SQL Server\140\PYTHON_SERVER\bin\x64 e fare doppio clic su **Python. exe**.

## <a name="get-help"></a>Supporto

Serve aiuto per l'installazione o l'aggiornamento? Per le risposte alle domande più comuni e ai problemi noti, vedere l'articolo seguente:

* [Domande frequenti sull'installazione e sull'aggiornamento-Machine Learning Services](../r/upgrade-and-installation-faq-sql-server-r-services.md)

Per verificare lo stato di installazione dell'istanza di e risolvere i problemi comuni, provare questi report personalizzati.

* [Report personalizzati per R Services per SQL Server](../r/monitor-r-services-using-custom-reports-in-management-studio.md)

## <a name="next-steps"></a>Passaggi successivi

Gli sviluppatori r possono iniziare a usare alcuni semplici esempi e apprendere le nozioni di base sul funzionamento di R con SQL Server. Per il passaggio successivo, vedere i collegamenti seguenti:

+ [Esercitazione: Eseguire R in T-SQL](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)
+ [Esercitazione: Analisi nel database per sviluppatori R](../tutorials/sqldev-in-database-r-for-sql-developers.md)

Gli sviluppatori Python possono apprendere come usare Python con SQL Server seguendo queste esercitazioni:

+ [Esercitazione: Eseguire Python in T-SQL](../tutorials/run-python-using-t-sql.md)
+ [Esercitazione: Analisi nel database per sviluppatori Python](../tutorials/sqldev-in-database-python-for-sql-developers.md)

Per visualizzare esempi di machine learning basati su scenari reali, vedere Esercitazioni su [Machine Learning](../tutorials/machine-learning-services-tutorials.md).