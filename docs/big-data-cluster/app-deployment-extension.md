---
title: Estensione di distribuzione di App
titleSuffix: SQL Server big data clusters
description: Distribuire uno script Python o R come un'applicazione nel cluster di big data 2019 Server SQL (anteprima).
author: jeroenterheerdt
ms.author: jterh
ms.reviewer: jroth
manager: jroth
ms.date: 02/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 0b0d76db3813e0a399f1ece841d729711743cbd9
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66801913"
---
# <a name="how-to-use-vs-code-to-deploy-applications-to-sql-server-big-data-clusters"></a>Come usare Visual Studio Code per distribuire applicazioni in cluster di SQL Server i big Data

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Questo articolo descrive come distribuire le applicazioni a un cluster di big data di SQL Server usando Visual Studio Code con l'estensione di distribuzione dell'App. Questa funzionalità è stata introdotta nella versione CTP 2.3. 

## <a name="prerequisites"></a>Prerequisiti

- [Visual Studio Code](https://code.visualstudio.com/).
- [Cluster di big data di SQL Server](big-data-cluster-overview.md) CTP 2.3 o versioni successive.

## <a name="capabilities"></a>Capabilities

Questa estensione supporta le attività seguenti in Visual Studio Code:

- Eseguire l'autenticazione con il cluster di big data di SQL Server.
- Recuperare un modello di applicazione dal repository GitHub per la distribuzione dei runtime supportati.
- Gestire i modelli di applicazione attualmente aperti nell'area di lavoro dell'utente.
- Distribuire un'applicazione tramite una specifica del formato YAML.
- Gestire le app distribuite nel cluster di big data di SQL Server.
- Visualizzare tutte le app che è stata distribuita nella barra laterale con informazioni aggiuntive.
- Generare una specifica di esecuzione per utilizzare l'app o eliminare l'app dal cluster.
- Usare le app distribuite tramite una specifica esecuzione YAML.

Le sezioni seguenti seguire il processo di installazione e viene fornita una panoramica del funzionamento dell'estensione. 

### <a name="install"></a>Installazione

Prima di tutto installare l'estensione di distribuzione dell'App in Visual Studio Code:

1. Scaricare [distribuire l'estensione dell'App](https://aka.ms/app-deploy-vscode) per installare l'estensione come parte di Visual Studio Code.

1. Avviare Visual Studio Code e passare all'intestazione laterale estensioni.

1. Scegliere il `…` menu di scelta rapida nella parte superiore della barra laterale, selezionare `Install from vsix`.

   ![Installare VSIX](media/vs-extension/install_vsix.png)

1. Trovare il `sqlservbdc-app-deploy.vsix` file scaricato e scegliere di installare.

Dopo che l'app di cluster di SQL Server i big data distribuisce estensione è stata installata, viene richiesto di ricaricare Visual Studio Code. Esplora App di SQL Server di integrazione applicativa dei dati nella barra laterale di Visual Studio Code dovrebbe a questo punto.

### <a name="app-explorer"></a>Esplora App

Fare clic sull'estensione della barra laterale per caricare un pannello laterale con Esplora l'App. Lo screenshot di esempio seguente di Esplora App non mostra alcuna App o le specifiche di app disponibili:

<img src="media/vs-extension/app_explorer.png" width=350px></img>
<!--![App Explorer](media/vs-extension/app_explorer.png)-->

#### <a name="new-connection"></a>Nuova connessione

Per connettersi all'endpoint del cluster, usare uno dei metodi seguenti:

- Fare clic sulla barra di stato nella parte inferiore con la dicitura `SQL Server BDC Disconnected`.
- Oppure fare clic su di `New Connection` pulsante all'inizio con la freccia rivolta in incoraggiare.

   ![Nuova connessione](media/vs-extension/connect_to_cluster.png)

Visual Studio Code richiede l'endpoint appropriato, username e password. Se non specificato le credenziali corrette e l'endpoint dell'app, Visual Studio Code notifica che si è stati connessi al cluster e si visualizzeranno le app distribuite popolate nella barra laterale. Se ci si connette correttamente, l'endpoint e il nome utente verrà salvati `./sqldbc` come parte del profilo utente. Non verranno salvati mai alcuna password o i token. Quando si accede nuovamente, il prompt dei comandi verrà pre-compilare con il nome utente e l'host salvato ma richiedono sempre di immettere una password. Se si desidera connettersi a un endpoint di cluster diverso, fare semplicemente clic la `New Connection` nuovamente. La connessione verrà chiusa automaticamente se si chiude Visual Studio Code o se si apre un'altra area di lavoro e sarà necessario ristabilire la connessione.

### <a name="app-template"></a>Modello di App

Per distribuire una nuova app da uno dei modelli disponibili, fare clic sul `New App Template` pulsante di `App Specifications` riquadro, in cui verrà richiesto per il nome, il runtime e ciò che posizione si desidera posizionare la nuova app nel computer locale. È consigliabile che è inserirlo nell'area di lavoro corrente di Visual Studio Code in modo che è possibile usare la funzionalità completa dell'estensione, ma è possibile inserirlo in un punto qualsiasi nel file system locale.

![Nuovo modello di App](media/vs-extension/new_app_template.png)

Al termine, viene eseguito lo scaffolding di un nuovo modello di app per l'utente nel percorso specificato e la distribuzione `spec.yaml` viene aperto nell'area di lavoro. Se la directory selezionata nell'area di lavoro, è visualizzato anche nell'elenco visualizzato nei `App Specifications` riquadro:

![Caricamento modello di App](media/vs-extension/loading_app_template.png)

Il modello è un semplice `Hello World` app disposti come segue:

- **spec.yaml**
   - Indica il cluster come distribuire l'app
- **run-spec.yaml**
   - Indica il cluster come chiamare l'app
- **handler.py**
   - Si tratta di file del codice sorgente come specificato dalle `src` in `spec.yaml`
   - Ha una funzione denominata `handler` che viene considerato il `entrypoint` dell'app come illustrato nel `spec.yaml`. Accetta un input di stringa denominato `msg` e restituisce un output di tipo stringa denominato `out`. Tali opzioni vengono specificate `inputs` e `outputs` del `spec.yaml`.

Se non si desidera un modello sottoposto a scaffolding e si preferisce semplicemente una `spec.yaml` per la distribuzione di un'app è già stata compilata, fare clic sui `New Deploy Spec` accanto al `New App Template` pulsante e attraverso lo stesso processo, ma si riceveranno solo il `spec.yaml`, che è possibile modificare la modalità di installazione.

### <a name="deploy-app"></a>Distribuire App

Si potrebbe distribuire immediatamente l'App tramite la sezione di codice `Deploy App` nel `spec.yaml` oppure premere il pulsante cartella lightning accanto al `spec.yaml` file nel menu App specifiche. L'estensione verrà comprimere tutti i file nella directory in cui il `spec.yaml` Trova e distribuire l'app nel cluster. 

>[!NOTE]
>Verificare che tutti i file dell'app siano nella stessa directory di `spec.yaml`. Il `spec.yaml` deve essere al livello radice della directory di codice sorgente dell'app. 

![Distribuire App pulsante](media/vs-extension/deploy_app_lightning.png)

![Distribuire App CodeLens](media/vs-extension/deploy_app_codelens.png)

Si riceverà una notifica quando l'app è pronta per lo stato dell'app nella barra laterale in base al consumo:

![App distribuita](media/vs-extension/app_deploy.png)

![Barra laterale di App pronta](media/vs-extension/app_ready_side_bar.png)

![Notifica App pronte](media/vs-extension/app_ready_notification.png)

Dal riquadro sul lato, sarà in grado di vedere gli argomenti seguenti disponibili all'utente:

È possibile visualizzare tutte le app che è stata distribuita nella barra laterale con le informazioni seguenti:

- state
- version
- parametri di input
- Parametri di output
- collegamenti
  - swagger
  - dettagli

Se si sceglie `Links`, si noterà che è possibile accedere la `swagger.json` dell'app distribuita, in modo che sia possibile scrivere il proprio client che chiama l'app:

![swagger](media/vs-extension/swagger.png)

Visualizzare [utilizzo di applicazioni nei cluster di big data](big-data-cluster-consume-apps.md) per altre informazioni.

### <a name="app-run"></a>Esecuzione dell'App

Quando l'app è pronta, chiamare l'app con il `run-spec.yaml` che è stato specificato come parte del modello di app:

![Esecuzione specifica](media/vs-extension/run_spec.png)

Specificare qualsiasi stringa al posto di cui si vuole `hello` e quindi nuovamente eseguirlo tramite il collegamento al codice di sezione o il pulsante di fulmine nella barra laterale accanto al `run-spec.yaml`. Se non è una specifica di esecuzione per qualsiasi motivo, è possibile generarne uno da app distribuita nel cluster:

![Ottenere esecuzione specifica](media/vs-extension/get_run_spec.png)

Dopo avere uno e stato modificato correttamente, è necessario eseguirlo. Visual Studio Code restituisce la risposta appropriata al termine dell'esecuzione dell'app:

![Output di App](media/vs-extension/app_output.png)

Come può notare in precedenza, il risultato verrà restituito in una variabile temporanea `.json` file nell'area di lavoro. Se si desidera mantenere questo output, è possibile salvarla, in caso contrario, verranno eliminato in chiusura. Se l'app è privo di output per stampare un file, si otterrà solo il `Successful App Run` notifica nella parte inferiore. Se non è stato eseguito correttamente, si riceverà un messaggio di errore appropriato che consentirà di determinare qual è il problema.

Quando si esegue un'app, esistono diversi modi per passare i parametri:

È possibile specificare tutti gli input necessari tramite un `.json`, vale a dire:

- `inputs: ./example.json`

Quando si chiama un'app distribuita, se eventuali parametri di input sono innati per l'app o l'utente specificato e che specificato parametro di input è diverso da una primitiva, ad esempio una matrice, vettore, frame di dati, e così via, JSON complesso specifica il tipo di parametro direttamente nella riga quando chiamare l'app, vale a dire:

- vettore
    - `inputs:`
        - `x: [1, 2, 3]`
- Matrice
    - `inputs:`
        - `x: [[A,B,C],[1,2,3]]`
- Object
    - `inputs:`
        - `x: {A: 1, B: 2, C: 3}`

O fornire una stringa di un percorso file assoluto o relativo di una `.txt`, `.json`, o `.csv` che fornisce l'input necessario nel formato richieste dall'applicazione. L'analisi di file dipende `Node.js Path library`, in cui un percorso di file viene definito come un `string that contains a / or \ character`.

Se il parametro di input non viene specificato in base alle esigenze, un messaggio di errore appropriato verrà visualizzato con il percorso file non corretto se è stato specificato un percorso di file di stringhe o tale parametro non valido. La responsabilità viene assegnata all'autore dell'app per verificare che comprendono i parametri che si sta definendo.

Per eliminare un'app, fare semplicemente clic nel Cestino possibile pulsante accanto all'app nel `Deployed Apps` riquadro laterale.

## <a name="next-steps"></a>Passaggi successivi

Scopri come integrare le app distribuite nel cluster di big data nelle proprie applicazioni in SQL Server [utilizzo di applicazioni nei cluster di big data](big-data-cluster-consume-apps.md) per altre informazioni. È anche possibile fare riferimento agli esempi aggiuntivi nella [esempi di distribuire App](https://aka.ms/sql-app-deploy) provare con l'estensione.

Per altre informazioni sui cluster dei big data a SQL Server, vedere [quali sono i cluster di SQL Server 2019 dei big data?](big-data-cluster-overview.md).


Il nostro obiettivo è rendere questa estensione utile per te e per aver inviato commenti e suggerimenti. Per inviare [ [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] team](https://aka.ms/sqlfeedback).
