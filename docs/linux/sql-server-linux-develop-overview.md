---
title: Sviluppare applicazioni per SQL Server in Linux
description: ''
author: VanMSFT
ms.author: vanto
manager: jroth
ms.date: 11/17/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 758cb738-b018-465b-9ab0-59a24b892e66
ms.openlocfilehash: 737fd2776c3320e9f71b9dfa372aa6de646516e6
ms.sourcegitcommit: 93d1566b9fe0c092c9f0f8c84435b0eede07019f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2019
ms.locfileid: "67833818"
---
# <a name="how-to-get-started-developing-applications-for-sql-server-on-linux"></a>Come iniziare a sviluppare applicazioni per SQL Server in Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

È possibile creare applicazioni che si connettono e usano SQL Server in Linux da un'ampia gamma di linguaggi di programmazione, ad esempio c#, Java, Node. js, PHP, Python, Ruby e C++. È anche possibile usare i framework web popolari e i framework di ORM Object Relational Mapping ().

> [!VIDEO https://channel9.msdn.com/events/Connect/2017/T153/player]

> [!TIP]
> Queste opzioni di sviluppo stesso consentono inoltre di destinazione di SQL Server in altre piattaforme. Le applicazioni possono con destinazione SQL Server in esecuzione in locale o nel cloud, in Linux, Windows o Docker su macOS. O è possibile scegliere come destinazione Database SQL di Azure e Azure SQL Data Warehouse.

## <a name="try-the-tutorials"></a>Prova le esercitazioni

Il modo migliore per iniziare e crea applicazioni con SQL Server è per provarlo subito per se stessi.

- Passare a [esercitazioni introduttive](https://aka.ms/sqldev).
- Selezionare la piattaforma di sviluppo e il linguaggio.
- Provare gli esempi di codice.

> [!TIP]
> Se si desidera sviluppare per SQL Server in Docker, esaminiamo il **macOS** esercitazioni.

## <a name="create-new-applications"></a>Creare nuove applicazioni

Se si crea una nuova applicazione, esaminare un elenco del [librerie di connettività](sql-server-linux-develop-connectivity-libraries.md) per un riepilogo dei connettori e i framework più diffusi disponibili per diversi linguaggi di programmazione.

## <a name="use-existing-applications"></a>Usare le applicazioni esistenti

Se si dispone di un'applicazione di database esistente, è possibile modificare semplicemente la relativa stringa di connessione alla destinazione di SQL Server in Linux. Assicurarsi che conoscere le [problemi noti](sql-server-linux-release-notes.md) in SQL Server in Linux.

## <a name="use-existing-sql-tools-on-windows-with-sql-server-on-linux"></a>Usare gli strumenti esistenti di SQL in Windows con SQL Server in Linux

Gli strumenti che attualmente eseguono in Windows, ad esempio PowerShell, SQL Server Management Studio e SSDT funzionano anche con SQL Server in Linux. Anche se non vengono eseguite in modo nativo in Linux, è comunque possibile gestire le istanze remote di SQL Server in Linux. 

Vedere gli argomenti seguenti per altre informazioni:

- [SQL Server Management Studio (SSMS)](sql-server-linux-manage-ssms.md)
- [SQL Server Data Tools (SSDT)](sql-server-linux-develop-use-ssdt.md)
- [SQL PowerShell](sql-server-linux-manage-powershell.md)

> [!Note]
> Assicurarsi che usi le versioni più recenti di questi strumenti per risultati ottimali.

## <a name="use-new-sql-tools-for-linux"></a>Utilizzare nuovi strumenti di SQL per Linux

È possibile usare le nuove [estensione mssql](https://aka.ms/mssql-marketplace) per [Visual Studio Code](https://code.visualstudio.com) su Linux, macOS e Windows. Per una procedura dettagliata, vedere l'esercitazione seguente:

- [Usare Visual Studio Code](sql-server-linux-develop-use-vscode.md)

È anche possibile usare nuovi strumenti da riga di comando nativi per Linux. Questi strumenti comprendono quanto segue:

- [sqlcmd](../tools/sqlcmd-utility.md)
- [bcp](sql-server-linux-migrate-bcp.md)
- [mssql-conf](sql-server-linux-configure-mssql-conf.md)

## <a name="next-steps"></a>Passaggi successivi

Per iniziare, installare SQL Server in Linux con una delle seguenti esercitazioni di avvio rapido:

- [Installare in Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md)
- [Installare in SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
- [Eseguire l'installazione in Ubuntu](quickstart-install-connect-ubuntu.md)
- [Esecuzione in Docker](quickstart-install-connect-ubuntu.md)
