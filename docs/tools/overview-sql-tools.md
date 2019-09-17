---
title: Strumenti di gestione e query SQL per SQL Server, SQL di Azure (database SQL di Azure, istanze gestite di SQL di Azure, macchine virtuali SQL) e data warehouse di Azure SQL | Microsoft Docs
description: Strumenti di gestione e query SQL per SQL Server, Azure SQL (database SQL di Azure, istanza gestita di SQL di Azure, macchine virtuali SQL) e Azure SQL data warehouse
ms.custom: ''
ms.date: 09/11/2019
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
ms.assetid: ''
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 56ed7a0cf53a026b470c90c36b37da95f02ac5bc
ms.sourcegitcommit: 3bd813ab2c56b415a952e5fbd5cfd96b361c72a2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/11/2019
ms.locfileid: "70913572"
---
# <a name="sql-query-and-management-tools-for-sql-server-azure-sql-azure-sql-database-azure-sql-managed-instance-sql-virtual-machines-and-azure-sql-data-warehouse"></a>Strumenti di gestione e query SQL per SQL Server, Azure SQL (database SQL di Azure, istanza gestita di SQL di Azure, macchine virtuali SQL) e Azure SQL data warehouse
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

Per gestire (eseguire query, monitorare e così via) il database è necessario uno strumento. Mentre i database possono essere eseguiti nel cloud, in Windows o in [Linux](../linux/sql-server-linux-overview.md), non è necessario che lo strumento venga eseguito sulla stessa piattaforma del database. 

Sono disponibili molti strumenti di database, pertanto questo articolo fornisce le descrizioni e i puntatori ad alcuni degli strumenti disponibili per l'uso dei database SQL. Se è necessario contribuire a decidere quale strumento è necessario, vedere [quale strumento si deve usare?](#which-tool-should-i-choose).

Per ulteriori informazioni e per scaricare uno strumento, selezionare i collegamenti nella colonna strumento nelle tabelle seguenti. Per scaricare SQL Server, vedere [Install SQL Server](../database-engine/install-windows/install-sql-server.md). 

## <a name="gui-tools-to-manage-databases"></a>Strumenti dell'interfaccia utente grafica per la gestione dei database  

Gli strumenti seguenti forniscono un'interfaccia utente grafica (GUI):

| Strumento | Descrizione | Viene eseguito in |
|:--|:--|:--|
| [[!INCLUDE[name-sos](../includes/name-sos.md)]](../sql-operations-studio/download.md) | [!INCLUDE[name-sos](../includes/name-sos-short.md)]è uno strumento gratuito e leggero per la gestione dei database ovunque si trovino. Questa versione di anteprima offre funzionalità di gestione di database, tra cui un editor Transact-SQL esteso e informazioni dettagliate personalizzabili sullo stato operativo dei database. | **[!INCLUDE[name-sos](../includes/name-sos-short.md)] viene eseguito in Windows, macOS e Linux**.|
| [SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms.md) | Usare SQL Server Management Studio (SSMS) per eseguire query, progettare e gestire i SQL Server, il database SQL di Azure e Azure SQL Data Warehouse. | **SSMS viene eseguito in Windows**.|
| [SQL Server Data Tools (SSDT)](../ssdt/download-sql-server-data-tools-ssdt.md) | Trasforma Visual Studio in un ambiente di sviluppo avanzato per SQL Server, database SQL di Azure e Azure SQL Data Warehouse.| **SSDT viene eseguito in Windows**.|
| [Visual Studio Code](https://code.visualstudio.com/)| Dopo l'installazione di Visual Studio Code, installare l' [estensione MSSQL](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql) per lo sviluppo di Microsoft SQL Server, database SQL di Azure e SQL data warehouse.| **Visual Studio Code viene eseguito in Windows, MacOS e Linux**.|


## <a name="command-line-tools-to-manage-databases"></a>Strumenti da riga di comando per la gestione dei database

Di seguito sono riportati gli strumenti principali da riga di comando:

| Strumento | Descrizione | Viene eseguito in |
|:--|:--|:--|
|[**mssql-cli (anteprima)** ](mssql-cli.md)|**MSSQL-CLI** è uno strumento da riga di comando interattivo per eseguire query SQL Server. | Windows, macOS e Linux|
| [**sqlpackage**](sqlpackage.md) |**SqlPackage** è un'utilità della riga di comando che automatizza diverse attività di sviluppo di database. le versioni macOS e Linux di SqlPackage sono attualmente in anteprima. | Windows, macOS e Linux|
|[**SQL Server PowerShell**](../powershell/sql-server-powershell.md)| **SQL Server PowerShell** fornisce cmdlet per l'utilizzo di SQL| Windows, macOS e Linux|
| [**sqlcmd**](sqlcmd-utility.md) |l'utilità **SQLCMD** consente di immettere istruzioni Transact-SQL, procedure di sistema e file script al prompt dei comandi. | Windows, macOS e Linux|
|[**bcp**](https://docs.microsoft.com/sql/tools/bcp-utility?view=sql-server-2014)|L'utilità del **p**rogramma di **c**opia **b**ulk (**bcp**) esegue operazioni di copia bulk di dati tra un'istanza di [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e un file di dati in un formato specificato dall'utente.|Windows, macOS e Linux|
|[**mssql-scripter (anteprima)** ](https://github.com/Microsoft/mssql-scripter)|**MSSQL-Scripter** è un'esperienza della riga di comando multipiattaforma per la creazione di script per database SQL Server|Windows, macOS e Linux|
|[**mssql-conf**](../linux/sql-server-linux-configure-mssql-conf.md)|**MSSQL-conf** configura SQL Server in esecuzione su Linux.|Linux|



## <a name="which-tool-should-i-choose"></a>Quale strumento scegliere?

- Si desidera gestire un'istanza o un database di SQL Server, in un editor leggero in Windows, Linux o Mac? Scegliere [[!INCLUDE[name-sos](../includes/name-sos.md)]](../sql-operations-studio/download.md)
- Si desidera gestire un'istanza o un database SQL Server in Windows con supporto GUI completo? Scegliere [SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms.md)
- Si desidera creare o gestire il codice del database, inclusa la convalida del tempo di compilazione, il refactoring e il supporto della finestra di progettazione in Windows? Scegliere [SQL Server Data Tools (SSDT)](../ssdt/download-sql-server-data-tools-ssdt.md)
- Si desidera eseguire una query SQL Server con uno strumento da riga di comando che include IntelliSense, la sintassi ad alta illuminazione e altro ancora? Scegliere [mssql-cli](mssql-cli.md)
- Si desidera scrivere gli script T-SQL in un editor leggero in Windows, Linux o Mac? Scegliere [Visual Studio Code](https://code.visualstudio.com/) e l' [estensione MSSQL](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql)



## <a name="additional-tools"></a>Strumenti aggiuntivi

| Strumento | Descrizione |
|:--|:--|
| [Gestione configurazione](../tools/configuration-manager/sql-server-configuration-manager-help.md) | Usare Gestione configurazione SQL Server per configurare i servizi SQL Server e configurare la connettività di rete. Configuration Manager viene eseguito in Windows|
| [SQL Server Migration Assistant](../ssma/sql-server-migration-assistant.md) | Usare SQL Server Migration Assistant per automatizzare la migrazione di database a SQL Server da Microsoft Access, DB2, MySQL, Oracle e Sybase.|
| [Database Experimentation Assistant](../dea/database-experimentation-assistant-overview.md) | Usare Database Experimentation Assistant per valutare una versione di SQL di destinazione per un determinato carico di lavoro. |
| [Riesecuzione distribuita](../tools/distributed-replay/install-distributed-replay-overview.md) | Utilizzare la funzionalità Riesecuzione distribuita per valutare l'effetto degli aggiornamenti SQL Server futuri. Usare inoltre Riesecuzione distribuita per valutare l'effetto degli aggiornamenti hardware e del sistema operativo e SQL Server l'ottimizzazione. |
| [ssbdiagnose](../tools/ssbdiagnose/ssbdiagnose-utility-service-broker.md) | L'utilità ssbdiagnose segnala i problemi in Service Broker conversazioni o la configurazione di Service Broker Services. |

Per ulteriori strumenti non citati in questa pagina, vedere [utilità del prompt dei comandi SQL](command-prompt-utility-reference-database-engine.md).

