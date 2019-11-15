---
title: Ottenere informazioni sui pacchetti R
description: Istruzioni su come ottenere informazioni sui pacchetti R installati in Machine Learning Services per SQL Server e R Services per SQL Server.
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
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2019
ms.locfileid: "69641158"
---
# <a name="get-r-package-information"></a>Ottenere informazioni sui pacchetti R

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Questo articolo descrive come ottenere informazioni sui pacchetti R installati in Machine Learning Services per SQL Server e R Services per SQL Server. Gli script R di esempio mostrano come elencare le informazioni sui pacchetti, ad esempio il percorso di installazione e la versione.

## <a name="default-r-library-location"></a>Percorso della libreria R predefinita

Quando si installa Machine Learning con SQL Server, viene creata una singola libreria di pacchetti a livello di istanza per ogni linguaggio installato. In Windows la libreria dell'istanza è una cartella protetta registrata con SQL Server.

Qualsiasi script eseguito nel database in SQL Server deve caricare le funzioni dalla libreria dell'istanza. SQL Server non può accedere ai pacchetti installati in altre librerie. Questo vale anche per i client remoti. Qualsiasi script R in esecuzione nel contesto di calcolo del server può usare solo i pacchetti installati nella libreria dell'istanza.
Per assicurare la protezione delle risorse del server, la libreria dell'istanza predefinita può essere modificata solo da un amministratore del computer.

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
Il percorso predefinito dei file binari per R è il seguente:

`C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library`
::: moniker-end

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
Il percorso predefinito dei file binari per R è il seguente:

`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library`
::: moniker-end

::: moniker range=">sql-server-2017||=sqlallproducts-allversions"
Il percorso predefinito dei file binari per R è il seguente:

`C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\R_SERVICES\library`
::: moniker-end

In questo esempio si presuppone che venga usata l'istanza di SQL predefinita, ovvero MSSQLSERVER. Se SQL Server è installato come istanza definita dall'utente, in alternativa viene usato il nome specificato.

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

L'istruzione seguente usa [rxSqlLibPaths](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqllibpaths) per restituire il percorso della libreria dell'istanza e la versione di RevoScaleR usata da SQL Server:

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

Con R Services per SQL Server vengono installati i pacchetti R seguenti.

|Pacchetti | Versione | Descrizione |
|---------|---------|-------------|
| [RevoScaleR](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler)  | 8.0.3 | Usato per contesti di calcolo remoti, streaming, esecuzione parallela di funzioni rx per l'importazione e la trasformazione dei dati, modellazione, visualizzazione e analisi. |
| [sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils) | 8.0.3 | Usato per includere script R nelle stored procedure. |

::: moniker-end

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"

Quando si seleziona la funzionalità R durante l'installazione di Machine Learning Services per SQL Server, vengono installati i pacchetti R seguenti.

|Pacchetti | Versione | Descrizione |
|---------|---------|-------------|
| [RevoScaleR](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler)  | 9.2 | Usato per contesti di calcolo remoti, streaming, esecuzione parallela di funzioni rx per l'importazione e la trasformazione dei dati, modellazione, visualizzazione e analisi. |
| [sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils) | 9.2 | Usato per includere script R nelle stored procedure. |
| [MicrosoftML](https://docs.microsoft.com/r-server/r-reference/microsoftml/microsoftml-package)| 9.2 | Aggiunge algoritmi di Machine Learning in R. | 
| [olapR](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) | 9.2 | Usato per la scrittura di istruzioni MDX in R. |

::: moniker-end

### <a name="component-upgrades"></a>Aggiornamenti dei componenti

Per impostazione predefinita, i pacchetti R vengono aggiornati tramite i Service Pack e gli aggiornamenti cumulativi. I pacchetti aggiuntivi e gli aggiornamenti completi della versione dei componenti di base di R sono possibili solo tramite aggiornamenti del prodotto oppure tramite il binding del supporto R con Microsoft Machine Learning Server.

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
È inoltre possibile aggiungere pacchetti MicrosoftML e olapR a un'istanza di SQL Server tramite un aggiornamento dei componenti.
::: moniker-end

Per altre informazioni, vedere [Aggiornare i componenti R e Python in SQL Server](../install/upgrade-r-and-python.md).

## <a name="default-open-source-r-packages"></a>Pacchetti R open source predefiniti

Il supporto per R include la distribuzione di R open source. In questo modo è possibile chiamare le funzioni R di base e installare altri pacchetti open source e di terze parti. Il supporto per il linguaggio R include le funzionalità di base, ad esempio **base**, **stats**, **utils** e altre ancora. Un'installazione di base di R include anche numerosi set di dati di esempio e strumenti R standard come **RGui** (un editor interattivo leggero) e **RTerm** (un prompt dei comandi R).

La distribuzione di R open source inclusa nell'installazione è [Microsoft R Open (MRO)](https://mran.microsoft.com/open). MRO aggiunge valore alle funzioni R di base includendo pacchetti open source aggiuntivi come [Intel Math Kernel Library](https://en.wikipedia.org/wiki/Math_Kernel_Library).

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
La versione di R fornita da MRO tramite l'installazione di R Services per SQL Server è la 3.2.2.
::: moniker-end

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
La versione di R fornita da MRO tramite l'installazione di Machine Learning Services per SQL Server è la 3.3.3.
::: moniker-end

> [!IMPORTANT]
> Non si dovrebbe mai sovrascrivere manualmente la versione di R installata dal programma di installazione di SQL Server con le versioni più recenti sul Web. I pacchetti Microsoft per R sono basati su versioni specifiche di R. La modifica dell'installazione può rendere instabile questa distribuzione.

## <a name="list-all-installed-r-packages"></a>Elenco di tutti i pacchetti R installati

L'esempio seguente usa la funzione R `installed.packages()` in una stored procedure di [!INCLUDE[tsql](../../includes/tsql-md.md)] per visualizzare un elenco dei pacchetti R installati nella libreria R_SERVICES per l'istanza SQL corrente. Questo script restituisce i campi relativi al nome e alla versione del pacchetto nel file DESCRIPTION.

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

Per altre informazioni sui campi facoltativi e predefiniti per il file DESCRIPTION del pacchetto R, vedere [https://cran.r-project.org](https://cran.r-project.org/doc/manuals/R-exts.html#The-DESCRIPTION-file).

## <a name="find-a-single-r-package"></a>Trovare un singolo pacchetto R

Se è stato installato un pacchetto R e si vuole verificare che il pacchetto sia disponibile per una determinata istanza di SQL Server, è possibile eseguire una stored procedure per caricare il pacchetto e restituire messaggi.

L'istruzione seguente, ad esempio, esegue la ricerca del pacchetto [glue](https://cran.r-project.org/web/packages/glue/) e lo carica, se disponibile.
Se il pacchetto non viene trovato o non può essere caricato, viene restituito un errore per segnalare che non è presente alcun pacchetto con il nome "glue".

```sql
EXECUTE sp_execute_external_script  
  @language =N'R',
  @script=N'require("glue")'
GO
```

Per altre informazioni sul pacchetto, vedere la funzione `packageDescription`.
L'istruzione seguente restituisce informazioni per il pacchetto **glue**.

```sql
EXECUTE sp_execute_external_script
  @language = N'R',
  @script = N'
print(packageDescription("glue"))
  '
```

## <a name="next-steps"></a>Passaggi successivi

+ [Installare nuovi pacchetti R](../r/install-additional-r-packages-on-sql-server.md)
+ [Ottenere informazioni sui pacchetti Python](python-package-information.md)
+ [Installare nuovi pacchetti Python](../python/install-additional-python-packages-on-sql-server.md)
+ [Esercitazioni di R e Python](../tutorials/machine-learning-services-tutorials.md)
