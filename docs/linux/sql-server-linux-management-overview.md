---
title: Gestire SQL Server in Linux | Microsoft Docs
description: Questo articolo fornisce collegamenti a attività comuni di gestione e strumenti per SQL Server in esecuzione su Linux.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 03/17/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 6bd8eb0b-593d-467e-87ea-ab1c4dbcd1ea
ms.openlocfilehash: f1f949db84689fae7e362f81cb686824f249c564
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66705228"
---
# <a name="choose-the-right-tool-to-manage-sql-server-on-linux"></a>Scegliere lo strumento giusto per la gestione di SQL Server in Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Esistono diversi modi per gestire SQL Server in Linux. La sezione seguente fornisce una rapida panoramica di gestione diversi strumenti e tecniche con i puntatori ad altre risorse.

## <a name="mssql-conf"></a>mssql-conf 

Il **mssql-conf** strumento consente di configurare SQL Server in Linux. Per altre informazioni, vedere [configurare SQL Server in Linux con mssql-conf](sql-server-linux-configure-mssql-conf.md).

## <a name="transact-sql"></a>Transact-SQL

Quasi tutto ciò che è possibile eseguire in uno strumento client può essere eseguita anche con istruzioni Transact-SQL. SQL Server fornisce [viste a gestione dinamica (DMV)](../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md) che eseguono una query lo stato e configurazione di SQL Server. Esistono inoltre [comandi Transact-SQL](../t-sql/language-reference.md) per attività di gestione di database. È possibile eseguire questi comandi in qualsiasi strumento client che supporta la connessione a SQL Server e l'esecuzione di query Transact-SQL, ad esempio [sqlcmd](sql-server-linux-setup-tools.md) oppure [Visual Studio Code](sql-server-linux-develop-use-vscode.md).

## <a name="azure-data-studio"></a>Azure Data Studio

Il nuovo Studio dati Azure è uno strumento multipiattaforma per la gestione di SQL Server. Per altre informazioni, vedere [Studio di Azure Data](../azure-data-studio/what-is.md).

## <a name="sql-server-management-studio-on-windows"></a>SQL Server Management Studio per Windows

SQL Server Management Studio (SSMS) è un'applicazione Windows che fornisce un'interfaccia utente grafica per la gestione di SQL Server. Anche se è attualmente in esecuzione solo su Windows, è possibile usarlo per connettersi in remoto alle istanze di Linux di SQL Server. Per altre informazioni sull'uso di SSMS per gestire SQL Server, vedere [usare SSMS per gestire SQL Server in Linux](sql-server-linux-manage-ssms.md).

## <a name="mssql-cli-preview"></a>MSSQL-cli (anteprima)

Microsoft ha rilasciato un nuovo strumento di scripting cross-platform per SQL Server, [mssql-cli](https://blogs.technet.microsoft.com/dataplatforminsider/2017/12/12/try-mssql-cli-a-new-interactive-command-line-tool-for-sql-server/). Questo strumento è attualmente in anteprima.

## <a name="powershell"></a>PowerShell

PowerShell offre un ambiente completo della riga di comando per la gestione di SQL Server in Linux. Per altre informazioni, vedere [usare PowerShell per gestire SQL Server in Linux](sql-server-linux-manage-powershell.md).

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni su SQL Server in Linux, vedere [SQL Server in Linux](sql-server-linux-overview.md).
