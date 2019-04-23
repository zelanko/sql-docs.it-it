---
title: Estensione di PowerShell
titleSuffix: Azure Data Studio
description: Installare e usare PowerShell per Azure Data Studio
ms.custom: seodec18
ms.date: 04/19/2019
ms.reviewer: alayu; sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: SQLvariant
ms.author: aanelson
manager: matthend
ms.openlocfilehash: 0ffb46d5d498ba04a6916e7e2d56ffccaaa71aef
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2019
ms.locfileid: "59981205"
---
# <a name="powershell-editor-support-for-azure-data-studio"></a>Supporto dell'Editor PowerShell per Azure Data Studio

Questa estensione offre supporto avanzato editor di PowerShell in [Studio di Azure Data](https://github.com/Microsoft/azuredatastudio).
A questo punto è possibile scrivere e il debug degli script di PowerShell usando l'interfaccia simile a IDE eccellente forniti da Studio dei dati di Azure.

![Estensione di PowerShell](media/powershell-extension/powershell-extension.png)


## <a name="features"></a>Funzionalità

- L'evidenziazione della sintassi
- Frammenti di codice
- IntelliSense per i cmdlet e altro ancora
- Analisi basata su regole fornite da [PowerShell Script Analyzer](http://github.com/PowerShell/PSScriptAnalyzer)
- Vai a definizione dei cmdlet e delle variabili
- Trovare i riferimenti dei cmdlet e delle variabili
- Area di lavoro e documento di individuazione di simboli
- Esegui selezione selezionata dell'uso di codice PowerShell <kbd>F8</kbd>
- Avviare la Guida online per il simbolo sotto il cursore utilizzando <kbd>Ctrl</kbd>+<kbd>F1</kbd>
- Supporto di base console interattiva.


## <a name="installing-the-extension"></a>L'installazione dell'estensione

È possibile installare la versione ufficiale dell'estensione di PowerShell seguendo i passaggi descritti nel [documentazione di Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/extensions).
Nel riquadro estensioni, cercare "PowerShell" estensione e installarlo non esiste.  È possibile ricevere una notifica automaticamente su tutti gli aggiornamenti di estensione futura.

È anche possibile installare un pacchetto VSIX dal nostro [pagina dei rilasci](https://github.com/PowerShell/vscode-powershell/releases) e l'installazione tramite la riga di comando:

```powershell
azuredatastudio --install-extension PowerShell-<version>.vsix
```

## <a name="platform-support"></a>Supporto della piattaforma

- **Windows 7 a 10** con Windows PowerShell versione 3 e versioni successive e PowerShell Core
- **Linux** con PowerShell Core (distribuzioni PowerShell supportato tutti)
- **macOS** con PowerShell Core

Leggere il [domande frequenti su](https://github.com/PowerShell/vscode-powershell/wiki/FAQ) per le risposte alle domande più comuni.

## <a name="installing-powershell-core"></a>Installazione di PowerShell Core

Se si esegue Data Studio di Azure in MacOS o Linux, è anche necessario installare PowerShell Core.

PowerShell Core è un progetto Open Source sul [GitHub](https://github.com/powershell/powershell).
Per altre informazioni sull'installazione di PowerShell Core in MacOS o Linux piattaforme, vedere gli articoli seguenti:

- [Installazione di PowerShell Core in Linux](https://docs.microsoft.com/powershell/scripting/install/installing-powershell-core-on-linux?view=powershell-6)
- [Installazione di PowerShell Core in macOS](https://docs.microsoft.com/powershell/scripting/install/installing-powershell-core-on-macos?view=powershell-6)

## <a name="example-scripts"></a>Script di esempio

Sono disponibili alcuni script di esempio dell'estensione `examples` cartella in cui è possibile usare per rilevare la modifica e funzionalità di debug di PowerShell.  Consulta l'inclusa [README.md](https://github.com/PowerShell/vscode-powershell/blob/master/examples/README.md) file per altre informazioni su come usarli.

Questa cartella è reperibile nel percorso seguente:

```powershell
$HOME/.azuredatastudio/extensions/ms-vscode.PowerShell-<version>/examples
```

o se si usa la versione di anteprima dell'estensione

 ```powershell
$HOME/.azuredatastudio/extensions/ms-vscode.powershell-preview-<version>/examples
```

Per aprire/visualizzazione esempi dell'estensione in Azure Data Studio, eseguire il comando seguente dal prompt dei comandi di PowerShell:

```powershell
azuredatastudio (Get-ChildItem $Home\.azuredatastudio\extensions\ms-vscode.PowerShell-*\examples)[-1]
```

### <a name="sql-powershell-examples"></a>Esempi di SQL PowerShell
Per usare questi esempi (sotto), è necessario installare il modulo SqlServer dal [PowerShell Gallery](https://www.powershellgallery.com/packages/SqlServer).

```powershell
Install-Module -Name SqlServer
```

> [!NOTE]
> Con la versione `21.1.18102` e successive, il `SqlServer` modulo supporta [PowerShell Core](https://github.com/PowerShell/PowerShell) 6.2 e remote, oltre a Windows PowerShell.

In questo esempio, utilizziamo il `Get-SqlInstance` per ottenere gli oggetti Server SMO per ServerA e ServerB.  Il valore predefinito di output per questo comando includerà il nome dell'istanza, versione, Service Pack & livello di aggiornamento di aggiornamento Cumulativo delle istanze.

```powershell
Get-SqlInstance -ServerInstance ServerA, ServerB
```

Di seguito è riportato un esempio di come output sarà simile:

```
Instance Name             Version    ProductLevel UpdateLevel  HostPlatform HostDistribution
-------------             -------    ------------ -----------  ------------ ----------------
ServerA                   13.0.5233  SP2          CU4          Windows      Windows Server 2016 Datacenter
ServerB                   14.0.3045  RTM          CU12         Linux        Ubuntu
```

Nell'esempio seguente, si farà un `dir` (alias di `Get-ChildItem`) per ottenere l'elenco di tutte le istanze di SQL Server sia incluso nel file server registrati e quindi usare il `Get-SqlDatabase` per ottenere un elenco di database per ognuna di tali istanze.

```powershell
dir 'SQLSERVER:\SQLRegistration\Database Engine Server Group' -Recurse |
WHERE { $_.Mode -ne 'd' } |
FOREACH {
    Get-SqlDatabase -ServerInstance $_.Name
}
```

Di seguito è riportato un esempio di come output sarà simile:

```
Name                 Status           Size     Space  Recovery Compat. Owner
                                            Available  Model     Level
----                 ------           ---- ---------- -------- ------- -----
AdventureWorks2017   Normal      336.00 MB   57.01 MB Simple       140 sa
master               Normal        6.00 MB  368.00 KB Simple       140 sa
model                Normal       16.00 MB    5.53 MB Full         140 sa
msdb                 Normal       48.44 MB    1.70 MB Simple       140 sa
PBIRS                Normal      144.00 MB   55.95 MB Full         140 sa
PBIRSTempDB          Normal       16.00 MB    4.20 MB Simple       140 sa
SSISDB               Normal      325.06 MB   26.21 MB Full         140 sa
tempdb               Normal       72.00 MB   61.25 MB Simple       140 sa
WideWorldImporters   Normal         3.2 GB     2.6 GB Simple       130 sa
```

Questo esempio Usa la `Get-SqlDatabase` cmdlet per recuperare un elenco di tutti i database nell'istanza ServerB, quindi presenta una griglia di tabella (utilizzando la `Out-GridView` cmdlet) per selezionare i database di eseguire il backup.  Una volta che l'utente fa clic sul pulsante "OK", solo i database evidenziati verranno sottoposti a backup.

```powershell
Get-SqlDatabase -ServerInstance ServerB |
Out-GridView -PassThru |
Backup-SqlDatabase -CompressionOption On
```

Questo esempio, anche in questo caso, ottiene l'elenco di tutte le istanze di SQL Server sia incluso nel file server registrati, quindi chiama il `Get-SqlAgentJobHistory` quali report sono trascorsi dalla mezzanotte, per ogni istanza di SQL Server elencata ogni processo di SQL Agent non riuscito.

```powershell
dir 'SQLSERVER:\SQLRegistration\Database Engine Server Group' -Recurse |
WHERE {$_.Mode -ne 'd' } |
FOREACH {
    Get-SqlAgentJobHistory -ServerInstance  $_.Name -Since Midnight -OutcomesType Failed
}
```

### <a name="sql-powershell-examples"></a>Esempi di SQL PowerShell
Per usare questi esempi (sotto), è necessario installare il modulo SqlServer dal [PowerShell Gallery](https://www.powershellgallery.com/packages/SqlServer).

```powershell
Install-Module -Name SqlServer -AllowPrerelease
```

In questo esempio, utilizziamo il `Get-SqlInstance` per ottenere gli oggetti Server SMO per ServerA e ServerB.  Il valore predefinito di output per questo comando includerà il nome dell'istanza, versione, Service Pack & livello di aggiornamento di aggiornamento Cumulativo delle istanze.

```powershell
Get-SqlInstance -ServerInstance ServerA, ServerB
```

Di seguito è riportato un esempio di come output sarà simile:

```
Instance Name             Version    ProductLevel UpdateLevel
-------------             -------    ------------ -----------
ServerA                   13.0.5233  SP2          CU4
ServerB                   14.0.3045  RTM          CU12
```

In questo esempio, si farà un `dir` (alias di `Get-ChildItem`) per ottenere l'elenco di tutte le istanze di SQL Server sia incluso nel file server registrati e quindi usare il `Get-SqlDatabase` per ottenere un elenco di database per ognuna di tali istanze.

```powershell
dir 'SQLSERVER:\SQLRegistration\Database Engine Server Group' -Recurse |
WHERE { $_.Mode -ne 'd' } |
FOREACH {
    Get-SqlDatabase -ServerInstance $_.Name
}
```

Di seguito è riportato un esempio di come output sarà simile:

```
Name                 Status           Size     Space  Recovery Compat. Owner
                                            Available  Model     Level      
----                 ------           ---- ---------- -------- ------- -----
AdventureWorks2017   Normal      336.00 MB   57.01 MB Simple       140 sa   
master               Normal        6.00 MB  368.00 KB Simple       140 sa   
model                Normal       16.00 MB    5.53 MB Full         140 sa   
msdb                 Normal       48.44 MB    1.70 MB Simple       140 sa   
PBIRS                Normal      144.00 MB   55.95 MB Full         140 sa   
PBIRSTempDB          Normal       16.00 MB    4.20 MB Simple       140 sa   
SSISDB               Normal      325.06 MB   26.21 MB Full         140 sa   
tempdb               Normal       72.00 MB   61.25 MB Simple       140 sa   
WideWorldImporters   Normal         3.2 GB     2.6 GB Simple       130 sa   
```

Questo esempio Usa la `Get-SqlDatabase` cmdlet per recuperare un elenco di tutti i database nell'istanza ServerB, quindi presenta una griglia di tabella (utilizzando la `Out-GridView` cmdlet) per selezionare i database di eseguire il backup.  Una volta che l'utente fa clic sul pulsante "OK", solo i database evidenziati verranno sottoposti a backup.

```powershell
Get-SqlDatabase -ServerInstance ServerB |
Out-GridView -PassThru |
Backup-SqlDatabase -CompressionOption On
```

In questo esempio, anche in questo caso, ottiene un elenco di tutte le istanze di SQL Server sia incluso nel file server registrati, quindi chiama il `Get-SqlAgentJobHistory` quali report sono trascorsi dalla mezzanotte, per ogni istanza di SQL Server elencata ogni processo di SQL Agent non riuscito.

```powershell
dir 'SQLSERVER:\SQLRegistration\Database Engine Server Group' -Recurse |
WHERE {$_.Mode -ne 'd' } |
FOREACH {
    Get-SqlAgentJobHistory -ServerInstance  $_.Name -Since Midnight -OutcomesType Failed
}
```

## <a name="reporting-problems"></a>Segnalazione di problemi

Se si verificano problemi con l'estensione di PowerShell, vedere [la documentazione sulla risoluzione dei problemi](https://github.com/PowerShell/vscode-powershell/blob/master/docs/troubleshooting.md) per informazioni sulla diagnosi e segnalare eventuali problemi.

#### <a name="security-note"></a>Nota sulla sicurezza

Per eventuali problemi di sicurezza, vedere [qui](https://github.com/PowerShell/vscode-powershell/blob/master/docs/troubleshooting.md#note-on-security).

## <a name="contributing-to-the-code"></a>Aggiunta come contributo al codice

Consultare il [documentazione sullo sviluppo](https://github.com/PowerShell/vscode-powershell/blob/master/docs/development.md) per altri dettagli su come contribuire a questa estensione.

## <a name="maintainers"></a>Gestori

- [Keith Hill](https://github.com/rkeithhill) - [@r_keith_hill](http://twitter.com/r_keith_hill)
- [Tyler Leonhardt](https://github.com/tylerl0706) - [@TylerLeonhardt](http://twitter.com/tylerleonhardt)
- [Rob Holt](https://github.com/rjmholt)

## <a name="license"></a>Licenza

Questa estensione è [concesso in licenza in base alla licenza MIT](https://github.com/PowerShell/vscode-powershell/blob/master/LICENSE.txt). Per informazioni dettagliate sui binari di terze parti viene inclusa con le versioni di questo progetto, vedere la [comunicazioni di terze parti](https://github.com/PowerShell/vscode-powershell/blob/master/Third%20Party%20Notices.txt) file.

## <a name="code-of-conductconduct-md"></a>[Codice di condotta][conduct-md]

Questo progetto ha adottato il [Microsoft codice di comportamento Open Source][conduct-code].
Per altre informazioni, vedere la [codice di domande frequenti sul comportamento] [ conduct-FAQ] oppure contattare [ opencode@microsoft.com ] [ conduct-email] eventuali altre domande o commenti.

[conduct-code]: http://opensource.microsoft.com/codeofconduct/
[conduct-FAQ]: http://opensource.microsoft.com/codeofconduct/faq/
[conduct-email]: mailto:opencode@microsoft.com
[conduct-md]: https://github.com/PowerShell/vscode-powershell/blob/master/CODE_OF_CONDUCT.md
