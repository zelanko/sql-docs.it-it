---
title: Scaricare il modulo PowerShell di SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 01/31/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: scripting
ms.topic: conceptual
keywords:
- installare sql server powershell, scaricare sql server powershell
ms.assetid: ''
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: f3870f3ddbcc39f0ba9ae9573b8647d9caf72a64
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/10/2019
ms.locfileid: "67730729"
---
# <a name="install-sql-server-powershell-module"></a>Installare il modulo PowerShell SqlServer
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

Questo articolo include indicazioni per l'installazione del modulo PowerShell **SqlServer**.
> [!NOTE]
> Esistono due moduli SQL Server PowerShell: 
> * **SQLPS**: questo modulo è incluso nell'installazione di SQL Server (per la compatibilità con le versioni precedenti), ma non viene più aggiornato. Il modulo PowerShell più aggiornato è il modulo **SqlServer**.
> * **SqlServer**: questo modulo include nuovi cmdlet per supportare le funzionalità più recenti di SQL. Il modulo contiene anche le versioni aggiornate dei cmdlet in **SQLPS**. 

Le versioni precedenti del modulo **SqlServer** *erano* incluse con SQL Server Management Studio (SSMS), ma solo con le versioni 16.x di SQL Server Management Studio. Per usare PowerShell con SSMS 17.0 e versioni successive, è necessario installare il modulo **SqlServer** da [PowerShell Gallery](https://www.powershellgallery.com/packages/Sqlserver).
La versione corrente del modulo **SqlServer** è la 21.1.18080. È basata sulla versione v150 di Microsoft.SQLServer.SMO e supporta la versione successiva di SQL Server. L'ultima versione del modulo basata sulla versione v140 di Microsoft.SQLServer.SMO è la 21.0.17279.

Versioni non definitive del modulo possono essere rese disponibili con una maggiore frequenza: vedere la sezione alla fine di questa pagina su come ottenere queste versioni del modulo.

Per installare il modulo **SqlServer** da PowerShell Gallery, avviare una sessione di [PowerShell](https://docs.microsoft.com/powershell/scripting/powershell-scripting) e usare i comandi seguenti. Se si verificano problemi durante l'installazione, vedere la [documentazione per l'installazione del modulo](https://docs.microsoft.com/powershell/gallery/psget/module/psget_install-module) e la [guida di riferimento per l'installazione del modulo](https://docs.microsoft.com/powershell/module/powershellget/Install-Module).

Per installare il modulo **SqlServer**:

```Install-Module -Name SqlServer```

Se nel computer sono presenti versioni precedenti del modulo **SqlServer** può essere possibile usare `Update-Module` (descritto più avanti in questo articolo) o specificare il parametro `-AllowClobber`:  

```Install-Module -Name SqlServer -AllowClobber```

Se non è possibile eseguire la sessione di PowerShell come amministratore, è possibile eseguire l'installazione per l'utente corrente:

```Install-Module -Name SqlServer -Scope CurrentUser```

Quando sono disponibili versioni aggiornate del modulo **SqlServer**, è possibile aggiornare la versione usando `Update-Module`:

```Update-Module -Name SqlServer```

Per visualizzare le versioni del modulo installate:

```Get-Module SqlServer -ListAvailable```

Per usare una versione specifica del modulo è possibile importarlo con un numero di versione specifico, come indicato di seguito:

```Import-Module SqlServer -Version 21.1.18080```

> [!NOTE]
> Versioni non definitive (o di "anteprima") del modulo possono essere disponibili in PowerShell Gallery. Possono essere rilevate e installate mediante i cmdlet aggiornati *Find-Module* e *Install-Module* incluse nel modulo [PowerShellGet](https://www.powershellgallery.com/packages/PowerShellGet) passando l'opzione *-AllowPrerelease*.
>
> Per individuare la versione non definitiva/di anteprima del modulo, è possibile eseguire il comando seguente:
>
> ```Find-Module SqlServer -AllowPrerelease```
>
> Per installare una versione non definitiva/di anteprima specifica del modulo è possibile installarla con un numero di versione specifico, come indicato di seguito:
>
> ```Install-Module SqlServer -RequiredVersion 21.1.18040-preview -AllowPrerelease```
> 

Le versioni del modulo **SqlServer** disponibili in PowerShell Gallery supportano il controllo delle versioni e richiedono PowerShell versione 5.0 o successiva. 

* [Modulo SqlServer in PowerShell Gallery](https://www.powershellgallery.com/packages/Sqlserver) 
* [Cmdlet di SQL Server](https://docs.microsoft.com/powershell/module/sqlserver)
* [Cmdlet di SQLPS](https://docs.microsoft.com/powershell/module/sqlps)
