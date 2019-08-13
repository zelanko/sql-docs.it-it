---
title: Estensione per la distribuzione di app
titleSuffix: SQL Server big data clusters
description: Distribuire uno script Python o R come applicazione in un cluster Big Data di SQL Server 2019 (anteprima).
author: jeroenterheerdt
ms.author: jterh
ms.reviewer: mikeray
ms.date: 02/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 1e5ab6364437432c803a364abd50ef5b1af4f8f6
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/25/2019
ms.locfileid: "67958918"
---
# <a name="how-to-use-vs-code-to-deploy-applications-to-sql-server-big-data-clusters"></a>Come usare VS Code per distribuire applicazioni in cluster Big Data di SQL Server

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Questo articolo descrive come distribuire applicazioni in un cluster Big Data di SQL Server usando Visual Studio Code con l'estensione per la distribuzione di app. Questa funzionalità è stata introdotta in CTP 2.3. 

## <a name="prerequisites"></a>Prerequisites

- [Visual Studio Code](https://code.visualstudio.com/).
- [Cluster Big Data di SQL Server](big-data-cluster-overview.md) CTP 2.3 o versioni successive.

## <a name="capabilities"></a>Funzionalità

Questa estensione supporta le attività seguenti in Visual Studio Code:

- Eseguire l'autenticazione con il cluster Big Data di SQL Server.
- Recuperare un modello di applicazione dal repository GitHub per la distribuzione dei runtime supportati.
- Gestire modelli di applicazione attualmente aperti nell'area di lavoro dell'utente.
- Distribuire un'applicazione tramite una specifica in formato YAML.
- Gestire le app distribuite nel cluster Big Data di SQL Server.
- Visualizzare tutte le app distribuite nella barra laterale con informazioni aggiuntive.
- Generare una specifica di esecuzione per utilizzare l'app o eliminarla dal cluster.
- Utilizzare le app distribuite tramite una specifica di esecuzione YAML.

Nelle sezioni seguenti viene descritto il processo di installazione e viene fornita una panoramica del funzionamento dell'estensione. 

### <a name="install"></a>Installazione

Installare prima di tutto l'estensione per la distribuzione di app in VS Code:

1. Scaricare l'[estensione per la distribuzione di app](https://aka.ms/app-deploy-vscode) per installarla come parte di VS Code.

1. Avviare VS Code e passare alla barra laterale Estensioni.

1. Fare clic sul menu di scelta rapida `Install from vsix` nella parte superiore della barra laterale e selezionare `…`.

   ![Installare VSIX](media/vs-extension/install_vsix.png)

1. Individuare il file `sqlservbdc-app-deploy.vsix` scaricato e selezionarlo per installarlo.

Al termine dell'installazione dell'estensione per la distribuzione di app per cluster Big Data di SQL Server, verrà chiesto di ricaricare VS Code. A questo punto, verrà visualizzato lo strumento di esplorazione delle app BDC per SQL Server nella barra laterale di VS Code.

### <a name="app-explorer"></a>Strumento di esplorazione delle app

Fare clic sull'estensione nella barra laterale per caricare un pannello laterale che mostra lo strumento di esplorazione delle app. Lo screenshot di esempio seguente dello strumento di esplorazione delle app non mostra alcuna app o specifica disponibile:

<img src="media/vs-extension/app_explorer.png" width=350px></img>
<!--![App Explorer](media/vs-extension/app_explorer.png)-->

#### <a name="new-connection"></a>Nuova connessione

Per connettersi all'endpoint del cluster, usare uno dei metodi seguenti:

- Fare clic sulla barra di stato nella parte inferiore che indica `SQL Server BDC Disconnected`.
- In alternativa, fare clic sul pulsante `New Connection` nella parte superiore che raffigura una freccia che punta a una porta.

   ![Nuova connessione](media/vs-extension/connect_to_cluster.png)

VS Code chiede l'endpoint, il nome utente e la password appropriati. Se vengono forniti le credenziali e l'endpoint dell'app corretti, VS Code segnala che è stata stabilita la connessione al cluster e nella barra laterale è possibile visualizzare tutte le app distribuite. Se la connessione riesce, l'endpoint e il nome utente vengono salvati in `./sqldbc` come parte del profilo utente. Password e token non vengono mai salvati. Quando si esegue di nuovo l'accesso, il prompt viene precompilato con l'host e il nome utente salvati, ma è sempre necessario immettere una password. Se si vuole connettersi a un endpoint del cluster diverso, fare semplicemente clic di nuovo su `New Connection`. La connessione viene automaticamente chiusa se si chiude VS Code o se si apre un'area di lavoro diversa ed è necessario riconnettersi.

### <a name="app-template"></a>Modello di app

Per distribuire una nuova app da uno dei modelli, fare clic sul pulsante `New App Template` nel riquadro `App Specifications`, in cui viene chiesto di immettere il nome, il runtime e il percorso in cui si vuole inserire la nuova app nel computer locale. È consigliabile inserirla nell'area di lavoro corrente di VS Code per poter usare la funzionalità completa dell'estensione, ma è possibile posizionarla in qualsiasi punto del file system locale.

![Nuovo modello di app](media/vs-extension/new_app_template.png)

Al termine, viene eseguito lo scaffolding automatico di un nuovo modello di app nel percorso specificato e il file `spec.yaml` di distribuzione viene aperto nell'area di lavoro. Se la directory selezionata si trova nell'area di lavoro, il file viene visualizzato anche nel riquadro `App Specifications`:

![Modello di app caricato](media/vs-extension/loading_app_template.png)

Il modello è una semplice app `Hello World` che viene definita nel modo seguente:

- **spec.yaml**
   - Indica al cluster come distribuire l'app
- **run-spec.yaml**
   - Indica al cluster come chiamare l'app
- **handler.py**
   - Questo è il file del codice sorgente in base a quanto specificato da `src` in `spec.yaml`
   - Include una funzione denominata `handler` che viene considerata `entrypoint` dell'app, come mostrato in `spec.yaml`. Accetta un input stringa denominato `msg` e restituisce un output stringa denominato `out`. Questi vengono specificati in `inputs` e `outputs` del file `spec.yaml`.

Se non si vuole che venga eseguito lo scaffolding del modello e si preferisce semplicemente un file `spec.yaml` per la distribuzione di un'app già compilata, fare clic sul pulsante `New Deploy Spec` accanto al pulsante `New App Template` ed eseguire lo stesso processo, ma in questo caso si riceverà semplicemente il file `spec.yaml`, che può essere modificato nel modo scelto.

### <a name="deploy-app"></a>Distribuire l'app

L'app può essere distribuita immediatamente tramite il CodeLens `Deploy App` in `spec.yaml` o premendo il pulsante che raffigura una cartella con un razzo accanto al file `spec.yaml` nel menu delle specifiche dell'app. L'estensione comprimerà tutti i file nella directory in cui si trova `spec.yaml` e distribuirà l'app nel cluster. 

>[!NOTE]
>Assicurarsi che tutti i file dell'app si trovino nella stessa directory di `spec.yaml`. `spec.yaml` deve trovarsi al livello radice della directory del codice sorgente dell'app. 

![Pulsante per la distribuzione dell'app](media/vs-extension/deploy_app_lightning.png)

![Distribuire il CodeLens dell'app](media/vs-extension/deploy_app_codelens.png)

Si riceverà una notifica quando l'app è pronta per l'uso in base allo stato dell'app nella barra laterale:

![App distribuita](media/vs-extension/app_deploy.png)

![App indicata come pronta nella barra laterale](media/vs-extension/app_ready_side_bar.png)

![Notifica di app pronta](media/vs-extension/app_ready_notification.png)

Nel riquadro laterale saranno disponibili gli elementi seguenti:

È possibile visualizzare tutte le app distribuite nella barra laterale con le informazioni seguenti:

- state
- version
- parametri di input
- parametri di output
- collegamenti
  - swagger
  - dettagli

Se si fa clic su `Links`, si noterà che è possibile accedere al file `swagger.json` dell'app distribuita, in modo da poter scrivere i propri client che chiamano l'app:

![Swagger](media/vs-extension/swagger.png)

Per altre informazioni, vedere [Utilizzare applicazioni in cluster Big Data](big-data-cluster-consume-apps.md).

### <a name="app-run"></a>Esecuzione dell'app

Quando l'app è pronta, è possibile chiamarla con `run-spec.yaml`, che è stato fornito come parte del modello di app:

![Specifica di esecuzione](media/vs-extension/run_spec.png)

Specificare qualsiasi stringa desiderata al posto di `hello` e quindi eseguire di nuovo l'app tramite il collegamento del CodeLens o il pulsante che raffigura un razzo nella barra laterale, accanto a `run-spec.yaml`. Se per qualunque motivo non è presente alcuna specifica di esecuzione, generarne una dall'app distribuita nel cluster:

![Ottenere la specifica di esecuzione](media/vs-extension/get_run_spec.png)

Dopo aver ottenuto la specifica e averla modificata in base alle esigenze, eseguire l'app. VS Code restituisce il feedback appropriato al termine dell'esecuzione dell'app:

![Output dell'app](media/vs-extension/app_output.png)

Come si può notare sopra, l'output viene fornito in un file `.json` temporaneo nell'area di lavoro. Se si vuole conservare questo output, è possibile salvarlo. In caso contrario, verrà eliminato alla chiusura. Se l'app non ha output da stampare in un file, si otterrà solo la notifica `Successful App Run` nella parte inferiore. Se l'esecuzione non è riuscita, si riceverà un messaggio di errore appropriato che aiuterà a determinare il problema.

Quando si esegue un'app, è possibile passare parametri in diversi modi:

È possibile specificare tutti gli input necessari tramite un file `.json`, ovvero:

- `inputs: ./example.json`

Quando si chiama un'app distribuita, se uno o più dei parametri di input sono innati nell'app o specificati dall'utente e il parametro di input specifico è diverso da una primitiva, ad esempio una matrice, un vettore, un dataframe, un file JSON complesso e così via, specificare il tipo di parametro direttamente nella riga durante la chiamata dell'app, ovvero:

- Vettore
    - `inputs:`
        - `x: [1, 2, 3]`
- Matrice
    - `inputs:`
        - `x: [[A,B,C],[1,2,3]]`
- Object
    - `inputs:`
        - `x: {A: 1, B: 2, C: 3}`

In alternativa, assegnare a una stringa un percorso di file relativo o assoluto a un file `.txt`, `.json` o `.csv` che fornisce l'input richiesto nel formato necessario per l'app. L'analisi dei file è basata su `Node.js Path library`, in cui un percorso è definito come `string that contains a / or \ character`.

Se in base alle esigenze il parametro di input non viene specificato, verrà visualizzato un messaggio di errore appropriato con il percorso del file errato se è stato specificato un percorso di file stringa o se il parametro non è valido. La responsabilità viene attribuita all'autore dell'app per garantire che questi conosca i parametri che definisce.

Per eliminare un'app, è sufficiente fare clic sul pulsante del cestino accanto all'app nel riquadro laterale `Deployed Apps`.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni su come integrare app distribuite in cluster Big Data di SQL Server nelle proprie applicazioni, vedere [Utilizzare applicazioni in cluster Big Data](big-data-cluster-consume-apps.md). È anche possibile fare riferimento agli esempi aggiuntivi disponibili in [Esempi di distribuzione di app](https://aka.ms/sql-app-deploy) per provare l'estensione.

Per altre informazioni sui cluster Big Data di SQL Server, vedere [Che cosa sono i cluster Big Data di SQL Server 2019?](big-data-cluster-overview.md).


L'obiettivo è rendere utile questa estensione e qualunque commento o suggerimento sarà bene accetto. Inviarli al [team di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]](https://aka.ms/sqlfeedback).
