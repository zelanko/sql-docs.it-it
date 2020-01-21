---
title: Panoramica di SQL Server Integration Services DevOps | Microsoft Docs
description: Informazioni su come compilare il processo CI/CD di SSIS con SSIS DevOps Tools.
ms.date: 12/06/2019
ms.topic: conceptual
ms.prod: sql
ms.prod_service: integration-services
ms.custom: ''
ms.technology: integration-services
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 4cf79aade8e74277ef7b5cbaa6e1bd3ae612e94b
ms.sourcegitcommit: 909b69dd1f918f00b9013bb43ea66e76a690400a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/14/2020
ms.locfileid: "75924925"
---
# <a name="sql-server-integration-services-ssis-devops-tools-preview"></a>SQL Server Integration Services (SSIS) DevOps Tools (anteprima)

L'estensione [SSIS DevOps Tools](https://marketplace.visualstudio.com/items?itemName=SSIS.ssis-devops-tools) è disponibile nel Marketplace di **Azure DevOps**.

Se non si dispone di un'organizzazione **Azure DevOps**, per prima cosa iscriversi ad [Azure Pipelines](https://docs.microsoft.com/azure/devops/pipelines/get-started/pipelines-sign-up?view=azure-devops) e quindi aggiungere l'estensione **SSIS DevOps Tools** seguendo [questa procedura](https://docs.microsoft.com/azure/devops/marketplace/overview?view=azure-devops&tabs=browser#add-an-extension).

**SSIS DevOps Tools** include l'attività **SSIS Build** (Compilazione SSIS) e l'attività di rilascio **SSIS Deploy** (Distribuzione SSIS).

- L'attività **SSIS Build** (Compilazione SSIS) supporta la compilazione di con estensione dtproj nel modello di distribuzione del progetto o nel modello di distribuzione del pacchetto.

- L'attività **SSIS Deploy** (Distribuzione SSIS) supporta la distribuzione di uno o più file con estensione ispac nel catalogo SSIS locale e in Azure-SSIS IR o di file SSISDeploymentManifest e relativi file associati in una condivisione file locale o di Azure.

## <a name="ssis-build-task"></a>Attività SSIS Build (Compilazione SSIS)

![attività di compilazione](media/ssis-build-task.png)

### <a name="properties"></a>Proprietà

#### <a name="project-path"></a>Percorso progetto

Percorso della cartella o del file di progetto da compilare. Se viene specificato un percorso di cartella, l'attività di compilazione SSIS cercherà in modo ricorsivo tutti i file dtproj in questa cartella e li compilerà tutti.

#### <a name="project-configuration"></a>Configurazione del progetto

Nome della configurazione di progetto da usare per la compilazione. Se non viene specificata, per impostazione predefinita viene assegnata la prima configurazione di progetto definita in ogni file dtproj.

#### <a name="output-path"></a>Percorso di output

Percorso di una cartella separata in cui salvare i risultati della compilazione, che può essere pubblicata come artefatto di compilazione tramite l'attività [Pubblica artefatti della compilazione](https://docs.microsoft.com/azure/devops/pipelines/tasks/utility/publish-build-artifacts?view=azure-devops).

### <a name="limitations-and-known-issues"></a>Limitazioni e problemi noti

- L'attività di compilazione SSIS si basa su Visual Studio e Progettazione SSIS, obbligatoria negli agenti di compilazione. Per eseguire l'attività di compilazione SSIS nella pipeline, quindi, è necessario scegliere **vs2017-win2016** per gli agenti ospitati da Microsoft oppure installare Visual Studio e Progettazione SSIS (VS2017 + SSDT2017 o VS2019 + estensione Progetti SSIS) negli agenti self-hosted.

- Per compilare progetti SSIS usando i componenti predefiniti (incluso SSIS Azure Feature Pack e altri componenti di terze parti), i componenti predefiniti devono essere installati nel computer in cui è in esecuzione l'agente pipeline.  Per l'agente ospitato da Microsoft, l'utente può aggiungere un'[attività di script di PowerShell](https://docs.microsoft.com/azure/devops/pipelines/tasks/utility/powershell?view=azure-devops) o un'[attività script da riga di comando](https://docs.microsoft.com/azure/devops/pipelines/tasks/utility/command-line?view=azure-devops) per scaricare e installare i componenti prima dell'esecuzione dell'attività di compilazione SSIS.

- Nell'attività di compilazione SSIS non sono supportati i livelli di protezione **EncryptSensitiveWithPassword** e **EncryptAllWithPassword**. Verificare che nessuno dei progetti SSIS presenti nella codebase usi questi due livelli di protezione. In caso contrario, l'attività di compilazione SSIS si blocca e viene generato un errore di timeout durante l'esecuzione.

## <a name="ssis-deploy-task"></a>Attività SSIS Deploy (Distribuzione SSIS)

![attività di distribuzione](media/ssis-deploy-task.png)

### <a name="properties"></a>Proprietà

#### <a name="source-path"></a>Percorso di origine

Percorso dei file di origine ISPAC o SSISDeploymentManifest da distribuire. Questo percorso può essere un percorso di cartella o un percorso di file.

#### <a name="destination-type"></a>Tipo destinazione

Tipo della destinazione. L'attività di distribuzione SSIS supporta attualmente due tipi di destinazione:

- *File System*: Distribuire i file SSISDeploymentManifest e i file associati in un file system specificato. Sono supportate sia la condivisione file locale che quella di Azure.
- *SSISDB*: Distribuire i file ISPAC in un catalogo SSIS specificato, che può essere ospitato in un database SQL Server locale o in Azure-SSIS Integration Runtime.

#### <a name="destination-server"></a>Server di destinazione

Nome del server SQL di destinazione. Può corrispondere al nome di un database SQL Server locale, di un database SQL di Azure o di un'istanza gestita di database SQL di Azure. Questa proprietà è visibile solo se il tipo di destinazione è SSISDB.

#### <a name="destination-path"></a>Percorso di destinazione

Percorso della cartella di destinazione in cui verrà distribuito il file di origine. Ad esempio:

- /SSISDB/\<folderName\>
- \\\\\<machineName\>\\\<shareFolderName\>\\\<optionalSubfolderName\>

L'attività di distribuzione SSIS creerà la cartella e la sottocartella, se non esistono già.

#### <a name="authentication-type"></a>Tipo di autenticazione

Tipo di autenticazione per accedere al server di destinazione specificato. Questa proprietà è visibile solo se il tipo di destinazione è SSISDB. L'attività di distribuzione SSIS supporta in genere quattro tipi di autenticazione:

- Autenticazione di Windows
- Autenticazione di SQL Server
- Active Directory - Password
- Active Directory - Integrata

Il supporto di un determinato tipo di autenticazione dipende tuttavia dal tipo di server di destinazione e dal tipo di agente. Per una matrice di supporto dettagliata, vedere la tabella seguente.

| |Pool ospitato da Microsoft|Agente self-hosted|
|---------|---------|---------|
|SQL Server in locale o macchina virtuale |N/D|Autenticazione di Windows|
|SQL di Azure|Autenticazione di SQL Server <br> Active Directory - Password|Autenticazione di SQL Server <br> Active Directory - Password <br> Active Directory - Integrata|

#### <a name="domain-name"></a>Nome di dominio

Nome di dominio per accedere al file system specificato. Questa proprietà è visibile solo se il tipo di destinazione è File System.
È possibile lasciarla vuota se all'account utente che esegue l'agente self-hosted è stato concesso l'accesso in lettura/scrittura al percorso di destinazione specificato.

#### <a name="username"></a>Username

Nome utente per accedere al file system o al database SSISDB specificato. Questa proprietà è visibile se il tipo di destinazione è File System o il tipo di autenticazione è Autenticazione SQL Server o Active Directory - Password.
È possibile lasciarla vuota se il tipo di destinazione è File System e se all'account utente che esegue l'agente self-hosted è stato concesso l'accesso in lettura/scrittura al percorso di destinazione specificato.

#### <a name="password"></a>Password

Password per accedere al file system o al database SSISDB specificato. Questa proprietà è visibile se il tipo di destinazione è File System o il tipo di autenticazione è Autenticazione SQL Server o Active Directory - Password.
È possibile lasciarla vuota se il tipo di destinazione è File System e se all'account utente che esegue l'agente self-hosted è stato concesso l'accesso in lettura/scrittura al percorso di destinazione specificato.

#### <a name="overwrite-existing-projects-or-ssisdeploymentmanifest-files-of-the-same-names"></a>Overwrite existing projects or SSISDeploymentManifest files of the same names (Sovrascrivi progetti esistenti o file SSISDeploymentManifest con lo stesso nome)

Consente di specificare se sovrascrivere progetti esistenti o file SSISDeploymentManifest con gli stessi nomi. Se 'No', l'attività di distribuzione SSIS ignorerà la distribuzione di questi file o progetti.

#### <a name="continue-deployment-when-error-occurs"></a>Continue deployment when error occurs (Continua la distribuzione in caso di errore)

Consente di specificare se TP deve continuare la distribuzione dei progetti o dei file rimanenti in caso di errore. Se 'No', l'attività di distribuzione SSIS si interromperà immediatamente in caso di errore.

### <a name="limitations-and-known-issues"></a>Limitazioni e problemi noti

L'attività di distribuzione SSIS non supporta attualmente gli scenari seguenti:

- Configurare l'ambiente nel catalogo SSIS.
- Distribuire ispac in Azure SQL Server o in un'istanza gestita di SQL di Azure che consente solo l'autenticazione a più fattori.
- Distribuire i pacchetti in MSDB o nell'archivio pacchetti SSIS.

## <a name="release-notes"></a>Note sulla versione

### <a name="version-012-preview"></a>Versione 0.1.2 - Anteprima

Data di rilascio: 13 gennaio 2020

- Aggiunte informazioni più dettagliate sull'eccezione nel log dell'attività di distribuzione SSIS quando il tipo di destinazione è SSISDB.
- Corretto il percorso di destinazione di esempio nel testo della Guida relativo al percorso di destinazione della proprietà dell'attività di distribuzione SSIS.

### <a name="version-011-preview"></a>Version 0.1.1 (anteprima)

Data di rilascio: 6 gennaio 2020

- Aggiunta la limitazione del requisito di versione minima dell'agente. Attualmente la versione minima dell'agente di questo prodotto è 2.144.0.
- Corretto testo errato visualizzato per l'attività di distribuzione SSIS.
- Perfezionati alcuni messaggi di errore.

### <a name="version-010-preview"></a>Version 0.1.0 (anteprima)

Data di rilascio: 5 dicembre 2019

Versione iniziale di SSIS DevOps Tools. Si tratta di una versione di anteprima.

## <a name="next-steps"></a>Passaggi successivi

- Ottenere [Estensione SSIS DevOps](https://marketplace.visualstudio.com/items?itemName=SSIS.ssis-devops-tools)
