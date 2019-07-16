---
title: Guida introduttiva per la verifica per determinare se R è presente in SQL Server
description: Guida introduttiva per la verifica dell'esistenza R e Machine Learning Services in SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
ms.openlocfilehash: f294f5f12e3efd734d1e54ace3041702c39d390a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67961968"
---
# <a name="quickstart-verify-r-exists-in-sql-server"></a>Avvio rapido: Verificare la presenza di R in SQL Server 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server include il supporto del linguaggio R per analitica di analisi scientifica dei dati residenti in dati di SQL Server. Lo script R può includere funzioni R open source, le librerie R di terze parti o librerie Microsoft R incorporate, ad esempio [RevoScaleR](../r/revoscaler-overview.md) per analitica predittiva su larga scala.

L'esecuzione dello script è tramite le stored procedure, usando uno degli approcci seguenti:

+ Incorporati [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) stored procedure, il passaggio di script R in come parametro di input.
+ Eseguire il wrapping dello script R in un [stored procedure di custom](sqldev-in-database-r-for-sql-developers.md) creato.

In questa Guida introduttiva, si verificherà [servizi di SQL Server 2017 Machine Learning](../what-is-sql-server-machine-learning.md) oppure [SQL Server 2016 R Services](../r/sql-server-r-services.md) viene installato e configurato.

## <a name="prerequisites"></a>Prerequisiti

Questo esercizio richiede l'accesso a un'istanza di SQL Server con uno dei già installati i componenti seguenti:

+ [Machine Learning Services di SQL Server 2017](../install/sql-machine-learning-services-windows-install.md), con il linguaggio R installato
+ [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md)

Istanza di SQL Server può essere in una macchina virtuale di Azure o in locale. Tieni presente che la funzionalità di script esterna è disabilitata per impostazione predefinita, pertanto potrebbe essere necessario [abilita la creazione di script esterni](../install/sql-machine-learning-services-windows-install.md#bkmk_enableFeature) e verificare che **Launchpad di SQL Server service** è in esecuzione prima di iniziare.

È anche necessario uno strumento per l'esecuzione di query SQL. È possibile eseguire gli script R tramite la gestione di qualsiasi database o eseguire una query dello strumento, purché possa connettersi a un'istanza di SQL Server ed eseguire una query T-SQL o una stored procedure. Questa Guida introduttiva Usa [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms).

## <a name="verify-r-exists"></a>Verificare il che esistenza di R

È possibile confermare che i servizi di Machine Learning (con R) è abilitato per l'istanza di SQL Server e la versione di R installata. Attenersi alla procedura seguente.

1. Aprire SQL Server Management Studio e connettersi all'istanza di SQL Server.

2. Eseguire il codice riportato di seguito. 

    ```SQL
    EXECUTE sp_execute_external_script
    @language =N'R',
    @script=N'print(version)';
    GO
    ```

3. R `print` funzione restituisce la versione per il **messaggi** finestra. Nell'output di esempio seguente, si noterà che SQL Server sono in questo caso R versione 3.3.3 installato.

    **Risultati**

    ```text
    platform       x86_64-w64-mingw32          
    arch           x86_64                      
    os             mingw32                     
    system         x86_64, mingw32             
    status                                     
    major          3                           
    minor          3.3                         
    year           2017                        
    month          03                          
    day            06                          
    svn rev        72310                       
    language       R                           
    version.string R version 3.3.3 (2017-03-06)
    nickname       Another Canoe               
    ```

Se si verificano eventuali errori da questa query, la regola gli eventuali problemi di installazione. Configurazione dopo l'installazione è necessaria per abilitare l'uso delle librerie di codice esterno. Visualizzare [installare SQL Server 2017 servizi di Machine Learning](../install/sql-machine-learning-services-windows-install.md) oppure [installare SQL Server 2016 R Services](../install/sql-r-services-windows-install.md). Analogamente, assicurarsi che il servizio Launchpad sia in esecuzione.

A seconda dell'ambiente, potrebbe essere necessario abilitare gli account di lavoro R per la connessione a SQL Server, installare librerie di rete aggiuntive, abilitare l'esecuzione remota del codice o riavviare l'istanza dopo aver completato la configurazione. Per altre informazioni, vedere [domande frequenti di eseguire l'aggiornamento e installazione di R Services](../r/upgrade-and-installation-faq-sql-server-r-services.md).

## <a name="list-r-packages"></a>Pacchetti R di elenco

Microsoft fornisce una serie di pacchetti R preinstallati con Machine Learning Services nell'istanza di SQL Server. Per visualizzare un elenco di R che vengono installati i pacchetti, incluse versione, dipendenze, licenza e informazioni sul percorso di libreria, attenersi alla procedura seguente.

1. Eseguire lo script seguente nell'istanza di SQL Server.

    ```SQL
    EXECUTE sp_execute_external_script @language = N'R'
    , @script = N'
    OutputDataSet <- data.frame(installed.packages()[,c("Package", "Version", "Depends", "License", "LibPath")]);'
    WITH result sets((Package NVARCHAR(255), Version NVARCHAR(100), Depends NVARCHAR(4000)
        , License NVARCHAR(1000), LibPath NVARCHAR(2000)));
    ```

2. L'output è tratto dal `installed.packages()` in R e di conseguenza restituito gruppo.

    **Risultati**

    ![I pacchetti installati in R](./media/rsql-installed-packages.png)

## <a name="next-steps"></a>Passaggi successivi

Ora che hai confermato che l'istanza è pronta per funzionare con R, esaminiamo più da vicino un'interazione di R di base.

> [!div class="nextstepaction"]
> [Avvio rapido: Script R di "Hello world" in SQL Server](quickstart-r-run-using-tsql.md)
