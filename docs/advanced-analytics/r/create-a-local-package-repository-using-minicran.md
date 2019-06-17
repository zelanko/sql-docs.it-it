---
title: Creare un repository di pacchetti R locale usando miniCRAN - servizi di SQL Server Machine Learning
description: Usare miniCran per rilevare, assemblare e installare le dipendenze dei pacchetti R in un unico pacchetto consolidato.
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 83d73bb9d075825472cda96a7dcd54e25549de5e
ms.sourcegitcommit: a91c3f4fe2587d474cd4d470bda93239ba2693bb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/14/2019
ms.locfileid: "67140625"
---
# <a name="create-a-local-r-package-repository-using-minicran"></a>Creare un repository di pacchetti R locale usando miniCRAN
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

[miniCRAN](https://cran.r-project.org/web/packages/miniCRAN/index.html) pacchetto, creato da [Andre de Vries](https://blog.revolutionanalytics.com/2016/05/minicran-sql-server.html), identifica e scarica i pacchetti e dipendenze in un'unica cartella, è possibile copiare in altri computer per l'installazione offline di pacchetti R.

Come input, specificare uno o più pacchetti. **miniCRAN** legge l'albero delle dipendenze per i pacchetti in modo ricorsivo e Scarica solo i pacchetti elencati e le relative dipendenze da CRAN o repository simile.

Come output, **miniCRAN** crea un repository internamente coerenza costituiti da pacchetti selezionati e tutte le dipendenze necessarie. È quindi possibile spostare il repository locale al server e continuare per installare i pacchetti senza una connessione internet.

> [!NOTE]
> Gli utenti R esperti cercano spesso per un elenco di pacchetti dipendenti nel file di descrizione per il pacchetto scaricato. Tuttavia, i pacchetti elencati nel **importazioni** potrebbe avere dipendenze di secondo livello. Per questo motivo, è consigliabile **miniCRAN** per l'assemblaggio della raccolta completa dei pacchetti necessari.

## <a name="why-create-a-local-repository"></a>Il motivo per cui creare un repository locale

L'obiettivo di creare un repository di pacchetti locale è fornire un'unica posizione che un amministratore del server o ad altri utenti nell'organizzazione possono usare per installare nuovi pacchetti R in un server, specialmente uno che non dispone dell'accesso a internet. Dopo aver creato il repository, è possibile modificarlo mediante l'aggiunta di nuovi pacchetti o aggiornando la versione dei pacchetti esistenti.

I repository dei pacchetti sono utili in questi scenari:

- **Sicurezza**: Molti utenti di R sono abituati a scaricare e installare nuovi pacchetti R in base alle esigenze, da CRAN o uno dei relativi siti mirror. Tuttavia, per motivi di sicurezza, i server di produzione in esecuzione [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] in genere non dispongono di connettività internet.

- **Semplice installazione offline**: Per installare il pacchetto server non in linea richiede che è anche scaricare tutte le dipendenze di pacchetto, miniCRAN Using rende più semplice ottenere tutte le dipendenze nel formato corretto.

    Usando miniCRAN, è possibile evitare errori di dipendenza del pacchetto quando si prepara i pacchetti da installare con il [CREATE EXTERNAL LIBRARY](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql) istruzione.

- **Migliorata la gestione delle versioni**: In un ambiente multiutente, esistono buone ragioni per evitare l'installazione senza restrizioni di più versioni dei pacchetti nel server. Usare un repository locale per fornire un set coerente di pacchetti per l'uso dagli analisti dei. 

> [!TIP]
> È anche possibile usare miniCRAN per preparare i pacchetti per l'uso in Azure Machine Learning. Per altre informazioni, vedere questo blog: [Usando miniCRAN in Azure Machine Learning, da Michele Usuelli](https://www.r-bloggers.com/using-minicran-in-azure-ml/) 

## <a name="install-minicran"></a>Installare miniCRAN

Il **miniCRAN** pacchetto stesso è dipendente da 18 altri pacchetti CRAN, tra cui è la **RCurl** pacchetto, che presenta una dipendenza di sistema sul **curl-sviluppo per sistemi operativi** pacchetto. Analogamente, creare un pacchetto **XML** presenta una dipendenza **libxml2 svil**. Per risolvere le dipendenze, è consigliabile compilare inizialmente il repository locale in un computer con accesso completo a internet. 

Eseguire i comandi seguenti in un computer con una base R, R tools e connessione a internet. Si presuppone che si tratta *non* computer SQL Server. I seguenti comandi installano il **miniCRAN** pacchetto e le richieste **igraph** pacchetto. In questo esempio controlla se il pacchetto è già installato, ma è possibile ignorare il se le istruzioni e installare i pacchetti direttamente.

```R
if(!require("miniCRAN")) install.packages("miniCRAN") 
if(!require("igraph")) install.packages("igraph") 
library("miniCRAN")
```

## <a name="set-the-cran-mirror-and-mran-snapshot"></a>Impostare il mirror CRAN e snapshot MRAN

Specificare un sito mirror da utilizzare nel recupero dei pacchetti. Ad esempio, è possibile usare il sito MRAN o qualsiasi altro sito nella propria area che contiene i pacchetti che necessari. Se il download ha esito negativo, provare un altro sito mirror.

```R
CRAN_mirror <- c(CRAN = "https://mran.microsoft.com")
CRAN_mirror <- c(CRAN = "https://cran.cnr.berkeley.edu")
```

## <a name="create-a-local-folder"></a>Creare una cartella locale

Creare una cartella locale, ad esempio `C:\mylocalrepo` in cui archiviare i pacchetti raccolti. Se si ripete questo spesso, è probabilmente necessario usare un nome più descrittivo, ad esempio "miniCRANZooPackages" o "miniCRANMyRPackagev2".

Specificare la cartella del repository locale. Sintassi di R Usa una barra rovesciata per nomi di percorso, che è opposta dalle convenzioni Windows.

```R
local_repo <- "C:/mylocalrepo"
```

## <a name="add-packages-to-the-local-repo"></a>Aggiungere pacchetti al repository locale

Dopo aver **miniCRAN** sia installato e caricato, crea un elenco che specifica i pacchetti aggiuntivi che si desidera scaricare.

Effettuare **non** aggiungere dipendenze a questo elenco iniziale. Il **igraph** pacchetto usato dal **miniCRAN** genera l'elenco delle dipendenze per l'utente. Per altre informazioni su come usare il grafico di dipendenze generato, vedere [usando miniCRAN per identificare le dipendenze dei pacchetti](https://cran.r-project.org/web/packages/miniCRAN/vignettes/miniCRAN-dependency-graph.html).

1. Aggiungere i pacchetti di destinazione, "in zoo" e "previsti" a una variabile.

    ```R
    pkgs_needed <- c("zoo", "forecast")
    ```

2. Facoltativamente, tracciare il grafico delle dipendenze, ma potrebbe risultare informativo.
    
    ```R
    plot(makeDepGraph(pkgs_needed))
    ```

3. Creare il repository locale. Assicurarsi di modificare la versione di R, se necessario per la versione installata nell'istanza di SQL Server. Versione 3.2.2 è SQL Server 2016, versione 3.3 è SQL Server 2017. Se è stato eseguito un aggiornamento del componente, la versione può essere più recente. Per altre informazioni, vedere [Python e R di ottenere informazioni sul pacchetto](../package-management/installed-package-information.md).

    ```R
    pkgs_expanded <- pkgDep(pkgs_needed, repos = CRAN_mirror);
    makeRepo(pkgs_expanded, path = local_repo, repos = CRAN_mirror, type = "win.binary", Rversion = "3.3");
    ```

   Da queste informazioni, il pacchetto miniCRAN crea la struttura di cartelle che è necessario copiare i pacchetti di [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] in un secondo momento.

A questo punto è necessario disporre una cartella che contiene i pacchetti necessari e tutti i pacchetti aggiuntivi che erano necessari. Il percorso dovrebbe essere simile a questo esempio: C:\mylocalrepo\bin\windows\contrib\3.3 e pertanto deve contenere una raccolta di pacchetti compressi. Non decomprimere i pacchetti o rinominare i file.

Facoltativamente, eseguire il codice seguente per elencare i pacchetti contenuti nel repository miniCRAN locale.

```R
pdb <- as.data.frame(pkgAvail(local_repo, type = "win.binary", Rversion = "3.3"), stringsAsFactors = FALSE);
head(pdb);
pdb$Package;
pdb[, c("Package", "Version", "License")]
```

## <a name="add-packages-to-the-instance-library"></a>Aggiungere i pacchetti nella libreria di istanza

Dopo aver creato un repository locale con i pacchetti che necessari, spostare il repository dei pacchetti nel computer di SQL Server. La procedura seguente viene descritto come installare i pacchetti tramite gli strumenti R.

1. Copiare la cartella che contiene il repository miniCRAN, nella sua interezza, al server in cui si prevede di installare i pacchetti. La cartella contiene in genere questa struttura: miniCRAN radice > bin > windows > contrib > versione > tutti i pacchetti. Negli esempi seguenti, si presuppone una cartella disattivata l'unità radice: 

2. Aprire uno strumento di R associato all'istanza (ad esempio, si potrebbe utilizzare Rgui.exe). Fare doppio clic su **Esegui come amministratore** per consentire allo strumento di apportare aggiornamenti al sistema.

    - Per SQL Server 2017 è il percorso del file per RGUI `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\bin\x64`.

    - Per SQL Server 2016, percorso file he RGUI è `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\bin\x64`.

3. Ottenere il percorso per la libreria di istanza e aggiungerlo all'elenco di percorsi di libreria. In SQL Server 2017, il percorso è simile all'esempio seguente.

    ```R
    outputlib <- "C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER/R_SERVICES/library"
    ```

4. Specificare il nuovo percorso nel server in cui è stato copiato il **miniCRAN** repository, come `server_repo`.

    In questo esempio si presuppone che copiata nel repository in una cartella temporanea sul server.

    ```R
    inputlib <- "C:/temp/mylocalrepo"
    ```

5. Poiché si lavora in una nuova area di lavoro R nel server, fornire anche l'elenco dei pacchetti da installare.

    ```R
    mypackages <- c("zoo", "forecast")
    ```

6. Installare i pacchetti, che fornisce il percorso della copia locale del repository miniCRAN.

    ```R
    install.packages(mypackages, repos = file.path("file://", normalizePath(inputlib, winslash = "/")), lib = outputlib, type = "win.binary", dependencies = TRUE);
    ```

7. Dalla raccolta di istanza, è possibile visualizzare i pacchetti installati usando un comando simile al seguente:

    ```R
    installed.packages()
    ```

## <a name="see-also"></a>Vedere anche

+ [Ottenere informazioni sui pacchetti](../package-management/installed-package-information.md)
+ [Esercitazioni di R](../tutorials/sql-server-r-tutorials.md)
