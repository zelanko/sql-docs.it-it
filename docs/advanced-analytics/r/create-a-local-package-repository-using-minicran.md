---
title: Creare un repository di pacchetti R locale usando miniCRAN
description: Usare miniCran per rilevare, assemblare e installare le dipendenze dei pacchetti R in un unico pacchetto consolidato.
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: a2324ad662cad2c91bc6e002fd652fed73d8ab3d
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715767"
---
# <a name="create-a-local-r-package-repository-using-minicran"></a>Creare un repository di pacchetti R locale usando miniCRAN
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

il pacchetto [miniCRAN](https://cran.r-project.org/web/packages/miniCRAN/index.html) , creato da [Andre de Vries](https://blog.revolutionanalytics.com/2016/05/minicran-sql-server.html), identifica e Scarica i pacchetti e le dipendenze in un'unica cartella, che è possibile copiare in altri computer per l'installazione di pacchetti R offline.

Come input, specificare uno o più pacchetti. **miniCRAN** legge in modo ricorsivo l'albero delle dipendenze per questi pacchetti e Scarica solo i pacchetti elencati e le relative dipendenze da Cran o da repository simili.

Come output, **miniCRAN** crea un repository coerente internamente costituito dai pacchetti selezionati e da tutte le dipendenze necessarie. È quindi possibile spostare il repository locale nel server e procedere con l'installazione dei pacchetti senza una connessione Internet.

> [!NOTE]
> Gli utenti esperti di R cercano spesso l'elenco dei pacchetti dipendenti nel file di descrizione per il pacchetto scaricato. Tuttavia, i pacchetti elencati nelle importazioni potrebbero avere dipendenze di secondo livello. Per questo motivo, è consigliabile **miniCRAN** per l'assemblaggio della raccolta completa dei pacchetti necessari.

## <a name="why-create-a-local-repository"></a>Perché creare un repository locale

L'obiettivo della creazione di un repository di pacchetti locale è fornire un'unica posizione che può essere usata da un amministratore del server o da altri utenti dell'organizzazione per installare nuovi pacchetti R in un server, in particolare uno che non dispone di accesso a Internet. Dopo aver creato il repository, è possibile modificarlo aggiungendo nuovi pacchetti o aggiornando la versione dei pacchetti esistenti.

I repository dei pacchetti sono utili in questi scenari:

- **Sicurezza**: Molti utenti R sono abituati a scaricare e installare nuovi pacchetti R a partire da CRAN o da uno dei siti mirror. Per motivi di sicurezza, tuttavia, i server [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] di produzione in esecuzione in genere non dispongono di connettività Internet.

- **Installazione offline più semplice**: Per installare il pacchetto in un server offline, è necessario scaricare anche tutte le dipendenze del pacchetto. l'uso di miniCRAN rende più semplice ottenere tutte le dipendenze nel formato corretto.

    Utilizzando miniCRAN, è possibile evitare errori di dipendenza del pacchetto quando si preparano i pacchetti per l'installazione con l'istruzione [Create external Library](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql) .

- **Gestione delle versioni migliorata**: In un ambiente multiutente sono validi i motivi per evitare l'installazione senza restrizioni di più versioni del pacchetto nel server. Usare un repository locale per fornire un set coerente di pacchetti utilizzabili dagli analisti. 

> [!TIP]
> È anche possibile usare miniCRAN per preparare i pacchetti da usare in Azure Machine Learning. Per ulteriori informazioni, vedere questo Blog: [Uso di miniCRAN in Azure ML, di Michele Usuelli](https://www.r-bloggers.com/using-minicran-in-azure-ml/) 

## <a name="install-minicran"></a>Installare miniCRAN

Il pacchetto **miniCRAN** dipende da 18 altri pacchetti Cran, tra cui il pacchetto **RCurl** , che ha una dipendenza di sistema dal pacchetto **curl-devel** . Analogamente, il **file XML** del pacchetto presenta una dipendenza da **libxml2-devel**. Per risolvere le dipendenze, è consigliabile compilare inizialmente il repository locale in un computer con accesso a Internet completo. 

Eseguire i comandi seguenti in un computer con una connessione di base R, R Tools e Internet. Si presuppone che *non* si tratti del computer SQL Server. I comandi seguenti installano il pacchetto **miniCRAN** e il pacchetto **igraph** obbligatorio. Questo esempio controlla se il pacchetto è già installato, ma è possibile ignorare le istruzioni If e installare direttamente i pacchetti.

```R
if(!require("miniCRAN")) install.packages("miniCRAN") 
if(!require("igraph")) install.packages("igraph") 
library("miniCRAN")
```

## <a name="set-the-cran-mirror-and-mran-snapshot"></a>Impostare il mirror CRAN e lo snapshot MRAN

Specificare un sito mirror da usare per ottenere i pacchetti. Ad esempio, è possibile usare il sito di MRAN o qualsiasi altro sito nella propria area che contiene i pacchetti necessari. Se il download non riesce, provare con un altro sito mirror.

```R
CRAN_mirror <- c(CRAN = "https://mran.microsoft.com")
CRAN_mirror <- c(CRAN = "https://cran.cnr.berkeley.edu")
```

## <a name="create-a-local-folder"></a>Creare una cartella locale

Creare una cartella locale, ad esempio `C:\mylocalrepo` in cui archiviare i pacchetti raccolti. Se si ripete spesso questo problema, è consigliabile usare un nome più descrittivo, ad esempio "miniCRANZooPackages" o "miniCRANMyRPackagev2".

Specificare la cartella come repository locale. La sintassi R usa una barra per i nomi di percorso, che è opposta rispetto alle convenzioni di Windows.

```R
local_repo <- "C:/mylocalrepo"
```

## <a name="add-packages-to-the-local-repo"></a>Aggiungere pacchetti al repository locale

Dopo l'installazione e il caricamento di **miniCRAN** , creare un elenco che specifichi i pacchetti aggiuntivi che si desidera scaricare.

**Non** aggiungere dipendenze a questo elenco iniziale. Il pacchetto **igraph** usato da **miniCRAN** genera automaticamente l'elenco di dipendenze. Per ulteriori informazioni sull'utilizzo del grafico dipendenze generato, vedere [utilizzo di miniCRAN per identificare](https://cran.r-project.org/web/packages/miniCRAN/vignettes/miniCRAN-dependency-graph.html)le dipendenze dei pacchetti.

1. Aggiungere i pacchetti di destinazione, "Zoo" e "Forecast" a una variabile.

    ```R
    pkgs_needed <- c("zoo", "forecast")
    ```

2. Facoltativamente, tracciare il grafico delle dipendenze, ma può essere informativo.
    
    ```R
    plot(makeDepGraph(pkgs_needed))
    ```

3. Creare il repository locale. Assicurarsi di modificare la versione di R se necessario per la versione installata nell'istanza di SQL Server. La versione 3.2.2 è la SQL Server 2016, la versione 3,3 è SQL Server 2017. Se è stato eseguito l'aggiornamento di un componente, la versione potrebbe essere più recente. Per altre informazioni, vedere [ottenere R e informazioni sul pacchetto python](../package-management/installed-package-information.md).

    ```R
    pkgs_expanded <- pkgDep(pkgs_needed, repos = CRAN_mirror);
    makeRepo(pkgs_expanded, path = local_repo, repos = CRAN_mirror, type = "win.binary", Rversion = "3.3");
    ```

   Da queste informazioni, il pacchetto miniCRAN crea la struttura di cartelle in cui è necessario copiare i pacchetti in [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] un secondo momento.

A questo punto è necessario disporre di una cartella contenente i pacchetti necessari e di eventuali pacchetti aggiuntivi richiesti. Il percorso dovrebbe essere simile all'esempio seguente: C:\mylocalrepo\bin\windows\contrib\3.3 e deve contenere una raccolta di pacchetti compressi. Non decomprimere i pacchetti né rinominare i file.

Facoltativamente, eseguire il codice seguente per elencare i pacchetti contenuti nel repository miniCRAN locale.

```R
pdb <- as.data.frame(pkgAvail(local_repo, type = "win.binary", Rversion = "3.3"), stringsAsFactors = FALSE);
head(pdb);
pdb$Package;
pdb[, c("Package", "Version", "License")]
```

## <a name="add-packages-to-the-instance-library"></a>Aggiungere pacchetti alla libreria di istanze

Quando si dispone di un repository locale con i pacchetti necessari, spostare il repository del pacchetto nel computer SQL Server. La procedura seguente descrive come installare i pacchetti usando R Tools.

1. Copiare l'intera cartella contenente il repository miniCRAN nel server in cui si prevede di installare i pacchetti. La cartella ha in genere questa struttura: miniCRAN radice > bin > Windows > contrib > versione > tutti i pacchetti. Negli esempi seguenti si presuppone una cartella all'esterno dell'unità radice: 

2. Aprire uno strumento R associato all'istanza. ad esempio, è possibile usare Rgui. exe. Fare clic con il pulsante destro del mouse su **Esegui come amministratore** per consentire allo strumento di eseguire aggiornamenti al sistema.

    - Per SQL Server 2017, il percorso del file per RGUI `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\bin\x64`è.

    - Per SQL Server 2016, il percorso del file per RGUI `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\bin\x64`è.

3. Ottenere il percorso della libreria di istanze e aggiungerlo all'elenco dei percorsi di libreria. In SQL Server 2017 il percorso è simile all'esempio seguente.

    ```R
    outputlib <- "C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER/R_SERVICES/library"
    ```

4. Specificare il nuovo percorso nel server in cui è stato copiato il repository **miniCRAN** , `server_repo`come.

    In questo esempio si presuppone che il repository sia stato copiato in una cartella temporanea nel server.

    ```R
    inputlib <- "C:/temp/mylocalrepo"
    ```

5. Poiché si sta lavorando in una nuova area di lavoro di R sul server, è necessario fornire anche l'elenco dei pacchetti da installare.

    ```R
    mypackages <- c("zoo", "forecast")
    ```

6. Installare i pacchetti, specificando il percorso della copia locale del repository miniCRAN.

    ```R
    install.packages(mypackages, repos = file.path("file://", normalizePath(inputlib, winslash = "/")), lib = outputlib, type = "win.binary", dependencies = TRUE);
    ```

7. Dalla libreria di istanze è possibile visualizzare i pacchetti installati usando un comando simile al seguente:

    ```R
    installed.packages()
    ```

## <a name="see-also"></a>Vedere anche

+ [Ottenere informazioni sui pacchetti](../package-management/installed-package-information.md)
+ [Esercitazioni di R](../tutorials/sql-server-r-tutorials.md)
