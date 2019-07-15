---
title: Gli strumenti di SQL e le utilità per SQL Server, Database SQL di Azure e Azure SQL Data Warehouse | Microsoft Docs
ms.custom: ''
ms.date: 11/19/2018
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
ms.assetid: ''
author: markingmyname
ms.author: maghan
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 0d7683ed4f45a2d2e28843b24d9abd2592b08fae
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/10/2019
ms.locfileid: "67731593"
---
# <a name="sql-tools-and-utilities-for-sql-server-azure-sql-database-and-azure-sql-data-warehouse"></a>Gli strumenti di SQL e le utilità per SQL Server, Database SQL di Azure e Azure SQL Data Warehouse
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

Per gestire (query, monitoraggio e così via) del database è necessario uno strumento. Mentre i database possono essere in esecuzione nel cloud, su Windows o su [Linux](../linux/sql-server-linux-overview.md), lo strumento non è necessario per l'esecuzione sulla stessa piattaforma del database. 

Sono disponibili molti strumenti di database, in modo che questo articolo fornisce le descrizioni e collegamenti ad alcuni degli strumenti disponibili per l'utilizzo dei database SQL. Se è necessaria assistenza per decidere quale strumento è necessario, vedere [quale strumento devo usare?](#which-tool-should-i-choose).

## <a name="gui-tools-to-manage-databases"></a>Strumenti di interfaccia utente grafica per gestire i database  

Di seguito sono gli strumenti dell'interfaccia utente principale di con interfaccia grafica.

| Strumento | Descrizione | Viene eseguito in |
|:--|:--|:--|
| [[!INCLUDE[name-sos](../includes/name-sos.md)]](../sql-operations-studio/download.md) | [!INCLUDE[name-sos](../includes/name-sos-short.md)] è uno strumento gratuito, leggero, per la gestione di database ogni volta che sono in esecuzione. Questa versione di anteprima fornisce funzionalità di gestione di database, tra cui un editor Transact-SQL esteso e personalizzabile approfondite lo stato operativo dei database. | **[!INCLUDE[name-sos](../includes/name-sos-short.md)] viene eseguito in Windows, macOS e Linux**.|
| [SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms.md) | Usare SQL Server Management Studio (SSMS) per eseguire una query, progettare e gestire SQL Server, Database SQL di Azure e Azure SQL Data Warehouse. | **SSMS viene eseguito in Windows**.|
| [SQL Server Data Tools (SSDT)](../ssdt/download-sql-server-data-tools-ssdt.md) | Trasforma Visual Studio in un ambiente di sviluppo avanzato per SQL Server, Database SQL di Azure e Azure SQL Data Warehouse.| **SSDT viene eseguito in Windows**.|
| [Visual Studio Code](https://code.visualstudio.com/)| Dopo aver installato Visual Studio Code, installare il [estensione mssql](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql) per lo sviluppo di Microsoft SQL Server, Database SQL di Azure e SQL Data Warehouse.| **Visual Studio Code viene eseguito in Windows, macOS e Linux**.|


## <a name="command-line-tools-to-manage-databases"></a>Strumenti da riga di comando per gestire i database

Di seguito sono i principali strumenti da riga di comando:

| Strumento | Descrizione | Viene eseguito in |
|:--|:--|:--|
|[**mssql-cli (anteprima)** ](mssql-cli.md)|**MSSQL-cli** è uno strumento da riga di comando interattivo per l'esecuzione di query SQL Server. | Windows, macOS e Linux|
| [**sqlpackage**](sqlpackage.md) |**Sqlpackage** è un'utilità della riga di comando che consente di automatizzare diverse attività di sviluppo di database. macOS e Linux versioni di sqlpackage sono attualmente in anteprima. | Windows, macOS e Linux|
|[**SQL Server PowerShell**](../powershell/sql-server-powershell.md)| **SQL Server PowerShell** fornisce cmdlet per l'utilizzo di SQL| Windows, macOS e Linux|
| [**sqlcmd**](sqlcmd-utility.md) |**SQLCMD** utilità consente di immettere istruzioni Transact-SQL, procedure di sistema e file script al prompt dei comandi. | Windows, macOS e Linux|
|[**bcp**](https://docs.microsoft.com/sql/tools/bcp-utility?view=sql-server-2014)|L'utilità del **p**rogramma di **c**opia **b**ulk (**bcp**) esegue operazioni di copia bulk di dati tra un'istanza di [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e un file di dati in un formato specificato dall'utente.|Windows, macOS e Linux|
|[**mssql-scripter (anteprima)** ](https://github.com/Microsoft/mssql-scripter)|**MSSQL-scripter** è un'esperienza della riga di comando multipiattaforma per lo script di database di SQL Server|Windows, macOS e Linux|
|[**mssql-conf**](../linux/sql-server-linux-configure-mssql-conf.md)|**MSSQL-conf** configura SQL Server in esecuzione in Linux.|Linux|



## <a name="which-tool-should-i-choose"></a>Quale strumento devo scegliere?

- Si desidera gestire un'istanza di SQL Server o database, in un editor leggero in Windows, Linux o Mac? Scegliere [[!INCLUDE[name-sos](../includes/name-sos.md)]](../sql-operations-studio/download.md)
- Si desidera gestire un'istanza di SQL Server o database in Windows con il supporto di interfaccia utente grafica completo? Scegliere [SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms.md)
- Eseguire operazioni che si desidera creare o mantenere il codice di database, tra cui la convalida della fase di compilazione, refactoring e progettazione di supporto in Windows? Scegliere [SQL Server Data Tools (SSDT)](../ssdt/download-sql-server-data-tools-ssdt.md)
- Si desidera eseguire una query SQL Server con uno strumento da riga di comando che offre IntelliSense, illuminazione-sintassi elevata, e così via? Scegliere [mssql-cli](mssql-cli.md)
- Si desidera scrivere gli script T-SQL in un editor leggero in Windows, Linux o Mac? Scegli [Visual Studio Code](https://code.visualstudio.com/) e il [estensione mssql](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql)



## <a name="additional-tools"></a>Strumenti aggiuntivi

| Strumento | Descrizione |
|:--|:--|
| [Gestione configurazione](../tools/configuration-manager/sql-server-configuration-manager-help.md) | Utilizzare Gestione configurazione SQL Server per configurare servizi di SQL Server e configurare la connettività di rete. Configuration Manager viene eseguito in Windows|
| [SQL Server Migration Assistant](../ssma/sql-server-migration-assistant.md) | Usare SQL Server Migration Assistant per automatizzare la migrazione di database a SQL Server da Microsoft Access, DB2, MySQL, Oracle e Sybase.|
| [Database Experimentation Assistant](../dea/database-experimentation-assistant-overview.md) | Usare Database sperimentazione Assistant per valutare una versione di destinazione di SQL per un determinato carico di lavoro. |
| [Riesecuzione distribuita](../tools/distributed-replay/install-distributed-replay-overview.md) | Usare la funzionalità riesecuzione distribuita che consentono di valutare l'impatto dei futuri aggiornamenti di SQL Server. Inoltre, utilizzare Distributed Replay per valutare l'impatto dell'hardware e aggiornamenti del sistema operativo e ottimizzazione di SQL Server. |
| [ssbdiagnose](../tools/ssbdiagnose/ssbdiagnose-utility-service-broker.md) | L'utilità ssbdiagnose segnala i problemi in conversazioni di Service Broker o la configurazione dei servizi di Service Broker. |

Se si sta cercando strumenti aggiuntivi che non sono stati citati in questa pagina, vedere [utilità del prompt dei comandi SQL](command-prompt-utility-reference-database-engine.md).

