---
title: Guida introduttiva per la verifica dell'esistenza di R in SQL Server
description: Guida introduttiva per la verifica dell'esistenza di R e Machine Learning Services in SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
ms.openlocfilehash: 951ffc07a32434b2f8d333140445f12c2971b811
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/24/2019
ms.locfileid: "68470620"
---
# <a name="quickstart-verify-r-exists-in-sql-server"></a>Avvio rapido: Verificare la presenza di R in SQL Server 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

SQL Server include il supporto del linguaggio R per data science Analytics sui dati SQL Server residenti. Lo script R può essere costituito da funzioni R Open Source, librerie R di terze parti o librerie Microsoft R predefinite, ad esempio [RevoScaleR](../r/revoscaler-overview.md) , per l'analisi predittiva su larga scala.

L'esecuzione di script avviene tramite stored procedure, usando uno degli approcci seguenti:

+ [Sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) incorporato stored procedure, passando lo script R in come parametro di input.
+ Eseguire il wrapping dello script R in un [stored procedure personalizzato](sqldev-in-database-r-for-sql-developers.md) creato dall'utente.

In questa Guida introduttiva verrà verificato che sia installato e configurato [SQL Server 2017 Machine Learning Services](../what-is-sql-server-machine-learning.md) o [2016 SQL Server R Services](../r/sql-server-r-services.md) .

## <a name="prerequisites"></a>Prerequisiti

Questo esercizio richiede l'accesso a un'istanza di SQL Server con uno dei seguenti elementi già installati:

+ [SQL Server 2017 Machine Learning Services](../install/sql-machine-learning-services-windows-install.md)con il linguaggio R installato
+ [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md)

L'istanza di SQL Server può trovarsi in una macchina virtuale di Azure o in locale. È sufficiente tenere presente che la funzionalità di scripting esterno è disabilitata per impostazione predefinita, pertanto potrebbe essere necessario abilitare l'esecuzione di [script esterni](../install/sql-machine-learning-services-windows-install.md#bkmk_enableFeature) e verificare che **launchpad di SQL Server servizio** sia in esecuzione prima di iniziare.

È anche necessario uno strumento per l'esecuzione di query SQL. È possibile eseguire gli script R usando qualsiasi strumento di gestione del database o query, purché sia in grado di connettersi a un'istanza di SQL Server ed eseguire una query T-SQL o stored procedure. Questa Guida introduttiva usa [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms).

## <a name="verify-r-exists"></a>Verifica R esistente

È possibile verificare che Machine Learning Services (con R) sia abilitato per l'istanza di SQL Server e la versione di R installata. Attenersi alla procedura riportata di seguito.

1. Aprire SQL Server Management Studio e connettersi all'istanza di SQL Server.

2. Eseguire il codice riportato di seguito. 

    ```SQL
    EXECUTE sp_execute_external_script
    @language =N'R',
    @script=N'print(version)';
    GO
    ```

3. La funzione `print` R restituisce la versione alla finestra **messages** . Nell'output di esempio seguente è possibile notare che SQL Server in questo caso è installata la versione 3.3.3 di R.

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

Se vengono generati errori da questa query, escludere eventuali problemi di installazione. La configurazione post-installazione è necessaria per consentire l'uso di librerie di codice esterno. Vedere [install SQL Server 2017 Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) o [Install 2016 SQL Server R Services](../install/sql-r-services-windows-install.md). Analogamente, assicurarsi che il servizio Launchpad sia in esecuzione.

A seconda dell'ambiente, potrebbe essere necessario abilitare gli account di lavoro R per la connessione a SQL Server, installare librerie di rete aggiuntive, abilitare l'esecuzione remota del codice o riavviare l'istanza dopo aver completato la configurazione. Per altre informazioni, vedere [domande frequenti sull'installazione e sull'aggiornamento di R Services](../r/upgrade-and-installation-faq-sql-server-r-services.md).

## <a name="list-r-packages"></a>Elencare i pacchetti R

Microsoft fornisce una serie di pacchetti R pre-installati con Machine Learning Services nell'istanza di SQL Server. Per visualizzare un elenco dei pacchetti R installati, incluse le informazioni sulla versione, le dipendenze, le licenze e il percorso di libreria, seguire questa procedura.

1. Eseguire lo script seguente nell'istanza di SQL Server.

    ```SQL
    EXECUTE sp_execute_external_script @language = N'R'
    , @script = N'
    OutputDataSet <- data.frame(installed.packages()[,c("Package", "Version", "Depends", "License", "LibPath")]);'
    WITH result sets((Package NVARCHAR(255), Version NVARCHAR(100), Depends NVARCHAR(4000)
        , License NVARCHAR(1000), LibPath NVARCHAR(2000)));
    ```

2. L'output è da `installed.packages()` in R e restituito come set di risultati.

    **Risultati**

    ![Pacchetti installati in R](./media/rsql-installed-packages.png)

## <a name="next-steps"></a>Passaggi successivi

A questo punto, dopo aver verificato che l'istanza è pronta per l'uso con R, esaminare in dettaglio un'interazione R di base.

> [!div class="nextstepaction"]
> [Avvio rapido: Script R "Hello World" in SQL Server](quickstart-r-run-using-tsql.md)
