---
title: Ottenere le informazioni sul pacchetto R
description: Informazioni su come ottenere informazioni sui pacchetti R installati in SQL Server Machine Learning Services e R Services per SQL Server.
ms.custom: ''
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/15/2019
ms.topic: conceptual
author: garyericson
ms.author: garye
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 8c3cf3c1debc03c169c585521b8b46dd8b1365c5
ms.sourcegitcommit: 632ff55084339f054d5934a81c63c77a93ede4ce
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2019
ms.locfileid: "69641158"
---
# <a name="get-r-package-information"></a>Ottenere le informazioni sul pacchetto R

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Questo articolo descrive come ottenere informazioni sui pacchetti R installati in SQL Server Machine Learning Services e R Services per SQL Server. Gli script R di esempio illustrano come elencare le informazioni del pacchetto, ad esempio il percorso di installazione e la versione.

## <a name="default-r-library-location"></a>Percorso predefinito della libreria R

Quando si installa Machine Learning con SQL Server, viene creata una singola libreria di pacchetti a livello di istanza per ogni lingua installata. In Windows la libreria di istanze è una cartella protetta registrata con SQL Server.

Tutti gli script eseguiti nel database in SQL Server devono caricare le funzioni dalla libreria di istanze. SQL Server non è in grado di accedere ai pacchetti installati in altre librerie. Questo vale anche per i client remoti: qualsiasi script R in esecuzione nel contesto di calcolo del server può usare solo i pacchetti installati nella libreria di istanze.
Per proteggere le risorse del server, la libreria di istanze predefinita può essere modificata solo da un amministratore del computer.

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
Il percorso predefinito dei file binari per R è:

`C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library`
::: moniker-end

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
Il percorso predefinito dei file binari per R è:

`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library`
::: moniker-end

::: moniker range=">sql-server-2017||=sqlallproducts-allversions"
Il percorso predefinito dei file binari per R è:

`C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\R_SERVICES\library`
::: moniker-end

Si presuppone che l'istanza di SQL predefinita, MSSQLSERVER. Se SQL Server viene installato come un'istanza denominata definita dall'utente, viene invece utilizzato il nome specificato.

<!-- I don't think this note is necessary. If you have these other products installed, you'd already know about them.
> [!NOTE]
> If you find other folders having similar subfolder names and files, you probably have a standalone installation of  Microsoft R Server or Machine Learning Server. These server products have different installers and paths: C:\Program Files\Microsoft\R Server\R_SERVER or C:\Program Files\Microsoft\ML SERVER\R_SERVER. For more information, see [Install R Server 9.1 for Windows](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows) or [Install Machine Learning Server for Windows](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install).
-->

Eseguire l'istruzione seguente per verificare la libreria di pacchetti R predefinita per l'istanza corrente:

```sql
EXECUTE sp_execute_external_script  
  @language = N'R',
  @script = N'OutputDataSet <- data.frame(.libPaths());'
WITH RESULT SETS (([DefaultLibraryName] VARCHAR(MAX) NOT NULL));
GO
```

Nell'istruzione seguente viene utilizzato [rxSqlLibPaths](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqllibpaths) per restituire il percorso della libreria di istanze e la versione di RevoScaleR utilizzata da SQL Server:

```sql
EXECUTE sp_execute_external_script
  @language =N'R',
  @script=N'
  sql_r_path <- rxSqlLibPaths("local")
  print(sql_r_path)
  version_info <-packageVersion("RevoScaleR")
  print(version_info)'
```

> [!NOTE]
> La funzione [rxSqlLibPaths](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqllibpaths) può essere eseguita solo sul computer locale. La funzione non può restituire percorsi di libreria per le connessioni remote.

## <a name="default-r-packages"></a>Pacchetti R predefiniti

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"

I pacchetti R seguenti vengono installati con R Services per SQL Server.

|Pacchetti | Versione | Descrizione |
|---------|---------|-------------|
| [RevoScaleR](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler)  | 8.0.3 | Usato per contesti di calcolo remoti, streaming, esecuzione parallela di funzioni RX per l'importazione e la trasformazione dei dati, la modellazione, la visualizzazione e l'analisi. |
| [sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils) | 8.0.3 | Usato per includere script R nelle stored procedure. |

::: moniker-end

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"

I pacchetti R seguenti vengono installati con SQL Server Machine Learning Services quando si seleziona la funzionalità R durante l'installazione.

|Pacchetti | Versione | Descrizione |
|---------|---------|-------------|
| [RevoScaleR](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler)  | 9,2 | Usato per contesti di calcolo remoti, streaming, esecuzione parallela di funzioni RX per l'importazione e la trasformazione dei dati, la modellazione, la visualizzazione e l'analisi. |
| [sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils) | 9,2 | Usato per includere script R nelle stored procedure. |
| [MicrosoftML](https://docs.microsoft.com/r-server/r-reference/microsoftml/microsoftml-package)| 9,2 | Aggiunge gli algoritmi di Machine Learning in R. | 
| [olapR](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) | 9,2 | Usato per la scrittura di istruzioni MDX in R. |

::: moniker-end

### <a name="component-upgrades"></a>Aggiornamenti componenti

Per impostazione predefinita, i pacchetti R vengono aggiornati tramite i Service Pack e gli aggiornamenti cumulativi. Pacchetti aggiuntivi e aggiornamenti completi della versione dei componenti di base di R sono possibili solo tramite aggiornamenti del prodotto o mediante l'associazione del supporto R a Microsoft Machine Learning Server.

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
Inoltre, è possibile aggiungere pacchetti MicrosoftML e olapr a un'istanza di SQL Server tramite un aggiornamento del componente.
::: moniker-end

Per altre informazioni, vedere [aggiornare i componenti R e Python in SQL Server](../install/upgrade-r-and-python.md).

## <a name="default-open-source-r-packages"></a>Pacchetti R Open Source predefiniti

Il supporto r include Open Source per poter chiamare le funzioni R di base e installare altri pacchetti open source e di terze parti. Il supporto del linguaggio R include funzionalità principali, ad esempio **base**, **statistiche**, **utils**e altre. Un'installazione di base di R include anche numerosi set di impostazioni di esempio e strumenti R standard come **RGui** (un editor interattivo leggero) e **RTerm** (un prompt dei comandi di r).

La distribuzione di R open source inclusa nell'installazione è [Microsoft R Open (riparazione)](https://mran.microsoft.com/open). Con l'aggiunta di un valore a R di base è possibile includere pacchetti open source aggiuntivi, ad esempio la [libreria del kernel matematico di Intel](https://en.wikipedia.org/wiki/Math_Kernel_Library).

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
La versione di R fornita da riparazione tramite R Services per SQL Server configurazione è 3.2.2.
::: moniker-end

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
La versione di R fornita da riparazione tramite SQL Server Machine Learning Services configurazione è 3.3.3.
::: moniker-end

> [!IMPORTANT]
> Non è mai necessario sovrascrivere manualmente la versione di R installata dal programma di installazione di SQL Server con le versioni più recenti sul Web. I pacchetti Microsoft R sono basati su versioni specifiche di R. la modifica dell'installazione potrebbe destabilizzarla.

## <a name="list-all-installed-r-packages"></a>Elenca tutti i pacchetti R installati

Nell'esempio seguente viene usata la funzione `installed.packages()` R in [!INCLUDE[tsql](../../includes/tsql-md.md)] una stored procedure per visualizzare un elenco di pacchetti R installati nella libreria R_SERVICES per l'istanza di SQL corrente. Questo script restituisce i campi relativi al nome e alla versione del pacchetto nel file di descrizione.

```sql
EXECUTE sp_execute_external_script
  @language=N'R',
@script = N'str(OutputDataSet);
packagematrix <- installed.packages();
Name <- packagematrix[,1];
Version <- packagematrix[,3];
OutputDataSet <- data.frame(Name, Version);',
@input_data_1 = N'
  '
WITH RESULT SETS ((PackageName nvarchar(250), PackageVersion nvarchar(max) ))
```

Per ulteriori informazioni sui campi facoltativi e predefiniti per il campo Descrizione pacchetto R, vedere [https://cran.r-project.org](https://cran.r-project.org/doc/manuals/R-exts.html#The-DESCRIPTION-file).

## <a name="find-a-single-r-package"></a>Trovare un singolo pacchetto R

Se è stato installato un pacchetto R e si desidera assicurarsi che sia disponibile per una particolare istanza di SQL Server, è possibile eseguire una stored procedure per caricare il pacchetto e restituire messaggi.

Ad esempio, l'istruzione seguente cerca e carica il pacchetto [Glue](https://cran.r-project.org/web/packages/glue/) , se disponibile.
Se non è possibile trovare o caricare il pacchetto, si verifica un errore contenente il testo "non è presente alcun pacchetto denominato ' glue '".

```sql
EXECUTE sp_execute_external_script  
  @language =N'R',
  @script=N'require("glue")'
GO
```

Per visualizzare ulteriori informazioni sul pacchetto, visualizzare `packageDescription`.
L'istruzione seguente restituisce informazioni per il pacchetto **Glue** .

```sql
EXECUTE sp_execute_external_script
  @language = N'R',
  @script = N'
print(packageDescription("glue"))
  '
```

## <a name="next-steps"></a>Passaggi successivi

+ [Installare nuovi pacchetti R](../r/install-additional-r-packages-on-sql-server.md)
+ [Ottenere informazioni sul pacchetto python](python-package-information.md)
+ [Installare nuovi pacchetti Python](../python/install-additional-python-packages-on-sql-server.md)
+ [Esercitazioni su R e Python](../tutorials/machine-learning-services-tutorials.md)
