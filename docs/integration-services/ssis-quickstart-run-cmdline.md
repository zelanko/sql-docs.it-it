---
title: Eseguire un pacchetto SSIS dal prompt dei comandi | Microsoft Docs
ms.date: 05/21/2018
ms.topic: quickstart
ms.prod: sql
ms.prod_service: integration-services
ms.custom: ''
ms.technology: integration-services
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d1a3a27bfce0a62aa70d047e221f54ccc33c0c6b
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/16/2019
ms.locfileid: "65717548"
---
# <a name="run-an-ssis-package-from-the-command-prompt-with-dtexecexe"></a>Eseguire un pacchetto SSIS dal prompt dei comandi con DTExec.exe

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


Questa guida introduttiva illustra come eseguire un pacchetto SSIS al prompt dei comandi eseguendo `DTExec.exe` con i parametri appropriati.

> [!NOTE]
> Il metodo descritto in questo articolo non è stato testato con i pacchetti distribuiti in un server di database SQL di Azure.

Per altre informazioni su `DTExec.exe`, vedere [Utilità dtexec](https://docs.microsoft.com/sql/integration-services/packages/dtexec-utility).

## <a name="supported-platforms"></a>Piattaforme supportate

È possibile usare le informazioni di questa guida introduttiva per eseguire un pacchetto SSIS nelle piattaforme seguenti:

-   SQL Server in Windows.

Il metodo descritto in questo articolo non è stato testato con i pacchetti distribuiti in un server di database SQL di Azure. Per altre informazioni sulla distribuzione e l'esecuzione di pacchetti in Azure, vedere [Spostare i carichi di lavoro di SQL Server Integration Services nel cloud](lift-shift/ssis-azure-lift-shift-ssis-packages-overview.md).

Non è possibile usare le informazioni di questa guida introduttiva per eseguire un pacchetto SSIS in Linux. Per altre informazioni sull'esecuzione di pacchetti in Linux, vedere [Estrarre, trasformare e caricare i dati in Linux con SSIS](../linux/sql-server-linux-migrate-ssis.md).

## <a name="run-a-package-with-dtexec"></a>Eseguire un pacchetto con dtexec

Se la cartella che contiene `DTExec.exe` non si trova nella variabile di ambiente `path`, può essere necessario usare il comando `cd` per passare alla directory corrispondente. Per SQL Server 2017 questa cartella è in genere `C:\Program Files (x86)\Microsoft SQL Server\140\DTS\Binn`.

Con i valori dei parametri usati nell'esempio seguente, il programma esegue il pacchetto nel percorso della cartella specificato nel server SSIS, ovvero il server che ospita il database del catalogo SSIS (SSISDB). Il parametro `/Server` specifica il nome del server. Il programma si connette come utente corrente con l'autenticazione integrata di Windows. Per usare l'autenticazione SQL, specificare i parametri `/User` e `Password` con i valori appropriati.

1. Aprire la finestra del prompt dei comandi.

2. Eseguire `DTExec.exe` e specificare i valori almeno per i parametri `ISServer` e `Server`, come illustrato nell'esempio seguente:

    ```cmd
    dtexec /ISServer "\SSISDB\Project1Folder\Integration Services Project1\Package.dtsx" /Server "localhost"
    ```

## <a name="next-steps"></a>Passaggi successivi
- Prendere in considerazione altri modi per eseguire un pacchetto.
    - [Eseguire un pacchetto SSIS con SSMS](./ssis-quickstart-run-ssms.md)
    - [Eseguire un pacchetto SSIS con Transact-SQL (SSMS)](./ssis-quickstart-run-tsql-ssms.md)
    - [Eseguire un pacchetto SSIS con Transact-SQL (Visual Studio Code)](ssis-quickstart-run-tsql-vscode.md)
    - [Eseguire un pacchetto SSIS con PowerShell](ssis-quickstart-run-powershell.md)
    - [Eseguire un pacchetto SSIS con C#](./ssis-quickstart-run-dotnet.md) 
