---
title: Installare SQL Server Machine Learning Services (R, Python) in Linux
description: Informazioni su come installare SQL Server Machine Learning Services (R, Python) in Red Hat, Ubuntu e SUSE.
author: dphansen
ms.author: davidph
ms.reviewer: vanto
manager: cgronlun
ms.date: 05/22/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: machine-learning
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: f578ae9dbc60b255959de406999feb8b68171389
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/25/2019
ms.locfileid: "68476194"
---
# <a name="install-sql-server-2019-machine-learning-services-r-python-on-linux"></a>Installare SQL Server 2019 Machine Learning Services (R, Python) in Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

[SQL Server Machine Learning Services](../advanced-analytics/index.yml) viene eseguito nei sistemi operativi Linux a partire da questa versione di anteprima di SQL Server 2019. Eseguire la procedura descritta in questo articolo per installare le estensioni di Machine Learning per R e Python.

Le estensioni di Machine Learning e di programmazione sono un componente aggiuntivo del motore di database. Anche se è possibile [installare il motore di database e Machine Learning Services simultaneamente](#install-all), è consigliabile installare e configurare prima il motore di database di SQL Server per poter risolvere eventuali problemi prima di aggiungere altri componenti. 

Il percorso del pacchetto per le estensioni R e Python si trova nei repository di origine di Linux per SQL Server. Se i repository di origine per l'installazione del motore di database sono già stati configurati, è possibile eseguire i comandi di installazione del pacchetto **mssql-mlservices** usando la stessa registrazione dei repository.

Machine Learning Services è supportato anche nei contenitori Linux. Non vengono forniti contenitori predefiniti con Machine Learning Services, ma è possibile crearne uno dai contenitori di SQL Server usando [un modello di esempio disponibile in GitHub](https://github.com/Microsoft/mssql-docker/tree/master/linux/preview/examples/mssql-mlservices).

## <a name="uninstall-previous-ctp"></a>Disinstallare la versione CTP precedente

L'elenco dei pacchetti è stato modificato nelle ultime versioni di CTP, creando un numero minore di pacchetti. Si consiglia di disinstallare CTP 2.x per rimuovere tutti i pacchetti precedenti prima di installare CTP 3.2. L'installazione side-by-side di più versioni non è supportata.

### <a name="1-confirm-package-installation"></a>1. Verificare l'installazione dei pacchetti

Come primo passaggio, potrebbe essere necessario verificare se esiste un'installazione precedente. I file seguenti indicano un'installazione esistente: checkinstallextensibility.sh, exthost, launchpad.

```bash
ls /opt/microsoft/mssql/bin
```

### <a name="2-uninstall-previous-ctp-2x-packages"></a>2. Disinstallare i pacchetti CTP 2.x precedenti

Disinstallare il pacchetto di livello più basso. Qualsiasi pacchetto upstream dipendente da un pacchetto di livello inferiore viene disinstallato automaticamente.

  + Per l'integrazione di R, rimuovere **microsoft-r-open***
  + Per l'integrazione di Python, rimuovere **mssql-mlservices-python**

I comandi per la rimozione dei pacchetti sono elencati nella tabella seguente.

| Piattaforma  | Comandi di rimozione dei pacchetti | 
|-----------|----------------------------|
| RHEL  | `sudo yum remove microsoft-r-open-mro-3.4.4`<br/>`sudo yum remove msssql-mlservices-python` |
| SLES  | `sudo zypper remove microsoft-r-open-mro-3.4.4`<br/>`sudo zypper remove msssql-mlservices-python` |
| Ubuntu    | `sudo apt-get remove microsoft-r-open-mro-3.4.4`<br/>`sudo apt-get remove msssql-mlservices-python`|

> [!Note]
> Microsoft R Open 3.4.4 è costituito da due o tre pacchetti, a seconda della versione CTP installata in precedenza. Il pacchetto foreachiterators è stato combinato nel pacchetto mro principale della versione CTP 2.2. Se uno di questi pacchetti è ancora presente dopo aver rimosso microsoft-r-open-mro-3.4.4, è necessario rimuoverli singolarmente.
> ```
> microsoft-r-open-foreachiterators-3.4.4
> microsoft-r-open-mkl-3.4.4
> microsoft-r-open-mro-3.4.4
> ```

### <a name="3-proceed-with-ctp-32-install"></a>3. Procedere con l'installazione di CTP 3.2

Installare il pacchetto di livello più alto seguendo le istruzioni riportate in questo articolo per il sistema operativo.

Per ogni set di istruzioni di installazione specifico del sistema operativo, il *pacchetto di livello più alto* corrisponde a **Esempio 1 - Installazione completa** per il set di pacchetti completo oppure a **Esempio 2 - Installazione minima** per il numero minimo di pacchetti necessari per un'installazione valida.

1. Per l'integrazione di R, iniziare con [MRO](#mro) perché è un prerequisito, senza il quale l'integrazione di R non verrà installata.

2. Eseguire i comandi di installazione usando le utilità di gestione pacchetti e la sintassi per il sistema operativo in uso: 

   + [RedHat](#RHEL)
   + [Ubuntu](#ubuntu)
   + [SUSE](#suse)

## <a name="prerequisites"></a>Prerequisites

+ La versione di Linux deve essere [supportata da SQL Server](sql-server-linux-release-notes-2019.md#supported-platforms), ma non include il motore Docker. Le versioni supportate includono:

   + [Red Hat Enterprise Linux (RHEL)](quickstart-install-connect-red-hat.md)

   + [SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)

   + [Ubuntu](quickstart-install-connect-ubuntu.md)

+ (Solo R) [Microsoft R Open](#mro) fornisce la distribuzione di R di base per la funzionalità R in SQL Server

+ È necessario avere uno strumento per eseguire i comandi T-SQL. Un editor di query è necessario per la configurazione e la convalida successiva all'installazione. È consigliabile usare [Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/download?view=sql-server-2017#get-azure-data-studio-for-linux), scaricabile gratuitamente, che viene eseguito in Linux.

<a name="mro"></a>

### <a name="microsoft-r-open-mro-installation"></a>Installazione di Microsoft R Open (MRO)

La distribuzione di base di Microsoft di R è un prerequisito per l'uso di RevoScaleR, MicrosoftML e altri pacchetti R installati con Machine Learning Services.

La versione richiesta è MRO 3.5.2.

Per installare MRO, scegliere uno dei due approcci seguenti:

+ Scaricare il file tarball di MRO da MRAN, decomprimerlo ed eseguire lo script install.sh. Se si sceglie questo approccio, è possibile seguire le [istruzioni di installazione nella pagina di MRAN](https://mran.microsoft.com/releases/3.5.2).

+ In alternativa, registrare il repository **packages.microsoft.com**, come descritto sotto, per installare i due pacchetti comprendenti la distribuzione di MRO: microsoft-r-open-mro e microsoft-r-open-mkl. 

I comandi seguenti registrano il repository che fornisce MRO. Dopo la registrazione, i comandi per l'installazione di altri pacchetti R, ad esempio mssql-mlservices-mml-r, includeranno automaticamente MRO come dipendenza del pacchetto.

#### <a name="mro-on-ubuntu"></a>MRO in Ubuntu

```bash
# Install as root
sudo su

# Optionally, if your system does not have the https apt transport option
apt-get install apt-transport-https

# Set the location of the package repo the "prod" directory containing the distribution.
# This example specifies 16.04. Replace with 14.04 if you want that version
wget https://packages.microsoft.com/config/ubuntu/16.04/packages-microsoft-prod.deb

# Register the repo
dpkg -i packages-microsoft-prod.deb

# Update packages on your system (required), including MRO installation
sudo apt-get update
```

#### <a name="mro-on-rhel"></a>MRO in RHEL

```bash
# Import the Microsoft repository key
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc


# Set the location of the package repo at the "prod" directory
# The following command is for version 7.x
# For 6.x, replace 7 with 6 to get that version
rpm -Uvh https://packages.microsoft.com/config/rhel/7/packages-microsoft-prod.rpm

# Update packages on your system (optional)
yum update
```
#### <a name="mro-on-suse"></a>MRO in SUSE

```bash
# Install as root
sudo su

# Set the location of the package repo at the "prod" directory containing the distribution
# This example is for SLES12, the only supported version of SUSE in Machine Learning Server
zypper ar -f https://packages.microsoft.com/sles/12/prod packages-microsoft-com

# Update packages on your system (optional)
zypper update
```

## <a name="package-list"></a>Elenco di pacchetti

In un dispositivo connesso a Internet i pacchetti vengono scaricati e installati in modo indipendente dal motore di database usando il programma di installazione del pacchetto per ogni sistema operativo. La tabella seguente descrive tutti i pacchetti disponibili, ma per R e Python si specificano pacchetti che forniscono l'installazione completa delle funzionalità o l'installazione minima delle funzionalità.

| Nome pacchetto | Applicabile a | Descrizione |
|--------------|----------|-------------|
|mssql-server-extensibility  | All | Framework di estendibilità usato per eseguire il codice R e Python. |
| microsoft-openmpi  | Python, R | Interfaccia per la trasmissione di messaggi usata dalle librerie Revo* per la parallelizzazione in Linux. |
| mssql-mlservices-python | Python | Distribuzione open source di Anaconda e Python. |
|mssql-mlservices-mlm-py  | Python | *Installazione completa*. Fornisce revoscalepy, microsoftml, modelli con training preliminare per la definizione di un immagine e l'analisi del sentiment del testo.| 
|mssql-mlservices-packages-py  | Python | *Installazione minima*. Fornisce revoscalepy e microsoftml. <br/>Esclude i modelli con training preliminare. | 
| [microsoft-r-open*](#mro) | R | Distribuzione open source di R, costituita da tre pacchetti. |
|mssql-mlservices-mlm-r  | R | *Installazione completa*. Fornisce RevoScaleR, MicrosoftML, sqlRUtils, olapR, modelli con training preliminare per la definizione di un immagine e l'analisi del sentiment del testo.| 
|mssql-mlservices-packages-r  | R | *Installazione minima*. Fornisce RevoScaleR, sqlRUtils, MicrosoftML, olapR. <br/>Esclude i modelli con training preliminare. | 
|mssql-mlservices-mml-py  | Solo CTP 2.0-2.1 | Obsoleto nella versione CTP 2.2 a causa del consolidamento del pacchetto Python in mssql-mslservices-python. Fornisce revoscalepy. Esclude i modelli con training preliminare e microsoftml.| 
|mssql-mlservices-mml-r  | Solo CTP 2.0-2.1 | Obsoleto nella versione CTP 2.2 a causa del consolidamento del pacchetto R in mssql-mslservices-python. Fornisce RevoScaleR, sqlRUtils, olapR. Esclude i modelli con training preliminare e MicrosoftML.  |

<a name="RHEL"></a>

## <a name="redhat-commands"></a>Comandi di RedHat

È possibile installare il supporto per la lingua in qualsiasi combinazione necessaria (una o più lingue). Per R e Python, è possibile scegliere tra due pacchetti. Uno fornisce tutte le funzionalità disponibili, caratterizzate dall'*installazione completa*. La scelta alternativa esclude i modelli di Machine Learning con training preliminare ed è considerata l'*installazione minima*.

> [!Tip]
> Se possibile, eseguire `yum clean all` per aggiornare i pacchetti nel sistema prima dell'installazione.

### <a name="example-1----full-installation"></a>Esempio 1: Installazione completa 

Include R e Python open source, framework di estendibilità, microsoft-openmpi, estensioni (R, Python), con librerie di Machine Learning e modelli con training preliminare per R e Python. 

```bash
# Install as root or sudo
# Add everything (all R, Python)
# Be sure to include -9.4.7* in mlsservices package names
sudo yum install mssql-mlservices-mlm-py-9.4.7*
sudo yum install mssql-mlservices-mlm-r-9.4.7* 
```

### <a name="example-2---minimum-installation"></a>Esempio 2: Installazione minima 

Include R e Python open source, framework di estendibilità, microsoft-openmpi, librerie principali di Revo* e librerie di Machine Learning per R e Python. Esclude i modelli con training preliminare.

```bash
# Install as root or sudo
# Minimum install of R, Python extensions
# Be sure to include -9.4.6* in mlsservices package names
sudo yum install mssql-mlservices-packages-py-9.4.7*
sudo yum install mssql-mlservices-packages-r-9.4.7*
```

<a name="ubuntu"></a>

## <a name="ubuntu-commands"></a>Comandi di Ubuntu

È possibile installare il supporto per la lingua in qualsiasi combinazione necessaria (una o più lingue). Per R e Python, è possibile scegliere tra due pacchetti. Uno fornisce tutte le funzionalità disponibili, caratterizzate dall'*installazione completa*. La scelta alternativa esclude i modelli di Machine Learning con training preliminare ed è considerata l'*installazione minima*.

> [!Tip]
> Se possibile, eseguire `apt-get update` per aggiornare i pacchetti nel sistema prima dell'installazione. Inoltre, alcune immagini Docker di Ubuntu potrebbero non avere l'opzione di trasporto apt HTTPS. Per installarla, usare `apt-get install apt-transport-https`.

### <a name="example-1----full-installation"></a>Esempio 1: Installazione completa 

Include R e Python open source, framework di estendibilità, microsoft-openmpi, estensioni (R, Python), con librerie di Machine Learning e modelli con training preliminare per R e Python. 

```bash
# Install as root or sudo
# Add everything (all R, Python)
# There is no asterisk in this full install
sudo apt-get install mssql-mlservices-mlm-py 
sudo apt-get install mssql-mlservices-mlm-r 
```

### <a name="example-2---minimum-installation"></a>Esempio 2: Installazione minima 

Include R e Python open source, framework di estendibilità, microsoft-openmpi, librerie principali di Revo* e librerie di Machine Learning per R e Python. Esclude i modelli con training preliminare. 

```bash
# Install as root or sudo
# Minimum install of R, Python
# No aasterisk
sudo apt-get install mssql-mlservices-packages-py
sudo apt-get install mssql-mlservices-packages-r
```

<a name="suse"></a>

## <a name="suse-commands"></a>Comandi di SUSE

È possibile installare il supporto per la lingua in qualsiasi combinazione necessaria (una o più lingue). Per R e Python, è possibile scegliere tra due pacchetti. Uno fornisce tutte le funzionalità disponibili, caratterizzate dall'*installazione completa*. La scelta alternativa esclude i modelli di Machine Learning con training preliminare ed è considerata l'*installazione minima*.

### <a name="example-1----full-installation"></a>Esempio 1: Installazione completa 

Include R e Python open source, framework di estendibilità, microsoft-openmpi, estensioni (R, Python), con librerie di Machine Learning e modelli con training preliminare per R e Python. 

```bash
# Install as root or sudo
# Add everything (all R, Python)
# Be sure to include -9.4.7* in mlsservices package names
sudo zypper install mssql-mlservices-mlm-py-9.4.7*
sudo zypper install mssql-mlservices-mlm-r-9.4.7* 
```

### <a name="example-2---minimum-installation"></a>Esempio 2: Installazione minima 

Include R e Python open source, framework di estendibilità, microsoft-openmpi, librerie principali di Revo* e librerie di Machine Learning per R e Python. Esclude i modelli con training preliminare. 

```bash
# Install as root or sudo
# Minimum install of R, Python extensions
# Be sure to include -9.4.6* in mlsservices package names
sudo zypper install mssql-mlservices-packages-py-9.4.7*
sudo zypper install mssql-mlservices-packages-r-9.4.7*
```

## <a name="post-install-config-required"></a>Configurazione successiva all'installazione (obbligatoria)

La configurazione aggiuntiva viene eseguita principalmente tramite lo [strumento mssql-conf](sql-server-linux-configure-mssql-conf.md).


1. Aggiungere l'account utente mssql usato per eseguire il servizio SQL Server. Questa operazione è necessaria se la configurazione non è stata eseguita in precedenza.

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

2. Accettare i contratti di licenza per R e Python open source. Questa operazione può essere eseguita in più modi. Se in precedenza è stata accettata la licenza di SQL Server e ora si aggiungono le estensioni R o Python, il comando seguente è il consenso alle condizioni:

   ```bash
   # Run as SUDO or root
   # Use set + EULA 
   sudo /opt/mssql/bin/mssql-conf set EULA accepteulaml Y
   ```

   Un flusso di lavoro alternativo prevede che, se il contratto di licenza per il motore di database di SQL Server non è ancora stato accettato, il programma di installazione rilevi i pacchetti mssql-mlservices e chieda l'accettazione delle condizioni di licenza quando viene eseguito `mssql-conf setup`. Per altre informazioni sui parametri delle condizioni di licenza, vedere [Configurare SQL Server con lo strumento mssql conf](sql-server-linux-configure-mssql-conf.md#mlservices-eula).

3. Abilitare l'accesso alla rete in uscita. L'accesso alla rete in uscita è disabilitato per impostazione predefinita. Per abilitare le richieste in uscita, impostare la proprietà booleana "outboundnetworkaccess" usando lo strumento mssql-conf. Per altre informazioni, vedere [Configurare SQL Server in Linux con mssql conf](sql-server-linux-configure-mssql-conf.md#mlservices-outbound-access).

   ```bash
   # Run as SUDO or root
   # Enable outbound requests over the network
   sudo /opt/mssql/bin/mssql-conf set extensibility outboundnetworkaccess 1
   ```

4. Per integrare solo le funzionalità di R, impostare la variabile di ambiente **MKL_CBWR** in modo da [garantire un output coerente](https://software.intel.com/articles/introduction-to-the-conditional-numerical-reproducibility-cnr) dai calcoli di Intel Math Kernel Library (MKL).

   + Modificare o creare un file denominato **.bash_profile** nella home directory dell'utente, aggiungendo la riga `export MKL_CBWR="AUTO"` al file.

   + Eseguire questo file digitando `source .bash_profile` al prompt dei comandi di Bash.

5. Riavviare il servizio Launchpad di SQL Server e l'istanza del motore di database per leggere i valori aggiornati dal file INI. Un messaggio di riavvio avverte ogni volta che viene modificata un'impostazione relativa all'estendibilità.  

   ```bash
   systemctl restart mssql-launchpadd

   systemctl restart mssql-server.service
   ```

6. Abilitare l'esecuzione di script esterni usando Azure Data Studio o un altro strumento come SQL Server Management Studio (solo Windows) che esegue Transact-SQL. 

   ```bash
   EXEC sp_configure 'external scripts enabled', 1 
   RECONFIGURE WITH OVERRIDE 
   ```

7. Riavviare nuovamente il servizio Launchpad.

## <a name="verify-installation"></a>Verificare l'installazione

Le librerie R (MicrosoftML, RevoScaleR e altre) sono disponibili in `/opt/mssql/mlservices/libraries/RServer`.

Le librerie Python (microsoftml e revoscalepy) sono disponibili in `/opt/mssql/mlservices/libraries/PythonServer`.

Per convalidare l'installazione, eseguire uno script T-SQL che esegue una stored procedure di sistema richiamando R o Python. Per questa attività sarà necessario uno strumento di query. Azure Data Studio è una scelta ottimale. Altri strumenti di uso comune, ad esempio SQL Server Management Studio o PowerShell, sono solo per Windows. Se si ha un computer Windows con questi strumenti, usarlo per connettersi all'installazione Linux del motore di database.

Eseguire il comando SQL seguente per testare l'esecuzione di R in SQL Server. Se lo script non viene eseguito, provare a riavviare il servizio con il comando `sudo systemctl restart mssql-server.service`.

```r
EXEC sp_execute_external_script   
@language =N'R', 
@script=N' 
OutputDataSet <- InputDataSet', 
@input_data_1 =N'SELECT 1 AS hello' 
WITH RESULT SETS (([hello] int not null)); 
GO 
```
 
Eseguire il comando SQL seguente per testare l'esecuzione di Python in SQL Server. 
 
```python
EXEC sp_execute_external_script  
@language =N'Python', 
@script=N' 
OutputDataSet = InputDataSet; 
', 
@input_data_1 =N'SELECT 1 AS hello' 
WITH RESULT SETS (([hello] int not null)); 
GO 
```

<a name="install-all"></a>

## <a name="chained-combo-install"></a>Installazione "combinata" concatenata

È possibile installare e configurare il motore di database e Machine Learning Services in una sola procedura aggiungendo i pacchetti e i parametri R o Python in un comando che installa il motore di database. 

1. Per l'integrazione di R, installare [Microsoft R Open](#mro) come prerequisito. Ignorare questo passaggio se non si sta installando la funzionalità R.

2. Specificare una riga di comando che includa il motore di database, oltre alle funzionalità delle estensioni del linguaggio.

  È possibile aggiungere un'unica funzionalità, ad esempio l'integrazione di Python, a un'installazione del motore di database.

  ```bash
  sudo yum install -y mssql-server mssql-mlservices-packages-r-9.4.7* 
  ```

  In alternativa, aggiungere entrambe le estensioni (R, Python).

  ```bash
  sudo yum install -y mssql-server mssql-mlservices-packages-r-9.4.7* mssql-mlservices-packages-py-9.4.7*
  ```

3. Accettare i contratti di licenza e completare la configurazione successiva all'installazione. Per questa attività usare lo strumento **mssql-conf**.

  ```bash
  sudo /opt/mssql/bin/mssql-conf setup
  ```

  Verrà richiesto di accettare il contratto di licenza per il motore di database, scegliere un'edizione e impostare la password dell'amministratore. Viene anche richiesto di accettare il contratto di licenza per Machine Learning Services.

4. Se richiesto, riavviare il servizio.

  ```bash
  sudo systemctl restart mssql-server.service
  ```

## <a name="unattended-installation"></a>Installazione automatica

Usando l'[installazione automatica](https://docs.microsoft.com/sql/linux/sql-server-linux-setup?view=sql-server-2017#unattended) per il motore di database, aggiungere i pacchetti per mssql-mlservices e le condizioni di licenza.

Si ricordi che il programma di installazione o lo strumento mssql-conf richiede l'accettazione del contratto di licenza. Se il motore di database di SQL Server è già stato configurato e le condizioni di licenza sono già state accettate, usare uno dei parametri delle condizioni di licenza specifici di mlservices per le distribuzioni di R e Python open source:

```bash
sudo /opt/mssql/bin/mssql-conf setup accept-eula-ml
```

Tutte le possibili permutazioni dell'accettazione delle condizioni di licenza sono documentate in [Configurare SQL Server in Linux con lo strumento mssql-conf](sql-server-linux-configure-mssql-conf.md#mlservices-eula).

## <a name="offline-installation"></a>Installazione offline

Per la procedura di installazione dei pacchetti, seguire le istruzioni contenute in [Installazione offline](sql-server-linux-setup.md#offline). Trovare il sito di download e quindi scaricare i pacchetti specifici usando l'elenco di pacchetti riportato di seguito.

> [!Tip]
> Molti degli strumenti di gestione dei pacchetti forniscono comandi che consentono di determinare le dipendenze dei pacchetti. Per yum, usare `sudo yum deplist [package]`. Per Ubuntu, usare `sudo apt-get install --reinstall --download-only [package name]` seguito da `dpkg -I [package name].deb`.


#### <a name="download-site"></a>Sito di download

È possibile scaricare i pacchetti da [https://packages.microsoft.com/](https://packages.microsoft.com/). Tutti i pacchetti mlservices per R e Python hanno un percorso condiviso con il pacchetto del motore di database. La versione di base per i pacchetti mlservices è la 9.4.5 (per CTP 2.0) 9.4.6 (per CTP 2.1 e versioni successive). Si ricordi che i pacchetti microsoft-r-open si trovano in un [repository diverso](#mro).

#### <a name="rhel7-paths"></a>Percorsi RHEL/7

|||
|--|----|
| Pacchetti mssql/mlservices | [https://packages.microsoft.com/rhel/7/mssql-server-preview/](https://packages.microsoft.com/rhel/7/mssql-server-preview/) |
| Pacchetti microsoft-r-open | [https://packages.microsoft.com/rhel/7/prod/](https://packages.microsoft.com/rhel/7/prod/) | 


#### <a name="ubuntu1604-paths"></a>Percorsi Ubuntu/16.04

|||
|--|----|
| Pacchetti mssql/mlservices | [https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/) |
| Pacchetti microsoft-r-open | [https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/](https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/) | 

#### <a name="sles12-paths"></a>Percorsi SLES/12

|||
|--|----|
| Pacchetti mssql/mlservices | [https://packages.microsoft.com/sles/12/mssql-server-preview/](https://packages.microsoft.com/sles/12/mssql-server-preview/) |
| Pacchetti microsoft-r-open | [https://packages.microsoft.com/sles/12/prod/](https://packages.microsoft.com/sles/12/prod/) | 

#### <a name="package-list"></a>Elenco di pacchetti

A seconda delle estensioni che si vogliono usare, scaricare i pacchetti necessari per una linguaggio specifico. I nomi dei file esatti includono le informazioni sulla piattaforma nel suffisso, ma i nomi dei file riportati di seguito dovrebbero essere sufficienti per determinare quali file ottenere.

```
# Core packages 
mssql-server-15.0.1000
mssql-server-extensibility-15.0.1000

# R
microsoft-openmpi-3.0.0
microsoft-r-open-mkl-3.5.2
microsoft-r-open-mro-3.5.2
mssql-mlservices-packages-r-9.4.7.64
mssql-mlservices-mlm-r-9.4.7.64


# Python
microsoft-openmpi-3.0.0
mssql-mlservices-python-9.4.7.64
mssql-mlservices-packages-py-9.4.7.64
mssql-mlservices-mlm-py-9.4.7.64
```

## <a name="add-more-rpython-packages"></a>Aggiungere altri pacchetti R/Python 
 
È possibile installare altri pacchetti R e Python e usarli nello script eseguito in SQL Server 2019.

### <a name="r-packages"></a>Pacchetti R 
 
1. Avviare una sessione di R.

   ```r
   # sudo /opt/mssql/mlservices/bin/R/R 
   ```

2. Installare un pacchetto R denominato [glue](https://mran.microsoft.com/package/glue) per testare l'installazione del pacchetto.

   ```r
   # install.packages("glue",lib="/opt/mssql/mlservices/libraries/RServer") 
   ```
   In alternativa, è possibile installare un pacchetto R dalla riga di comando 

   ```r
   # sudo /opt/mssql/mlservices/bin/R/R CMD INSTALL -l /opt/mssql/mlservices/libraries/RServer glue_1.1.1.tar.gz 
   ```

3. Importare il pacchetto R in [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).

   ```r
   EXEC sp_execute_external_script  
   @language = N'R', 
   @script = N'library(glue)' 
   ```

### <a name="python-packages"></a>Pacchetti Python 
 
1. Installare un pacchetto Python denominato [httpie](https://httpie.org/) usando pip. 

   ```python
   # sudo /opt/mssql/mlservices/bin/python/python -m pip install httpie 
   ``` 

2. Importare il pacchetto Python in [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).
 
   ```python
   EXEC sp_execute_external_script  
   @language = N'Python',  
   @script = N'import httpie' 
   ```

## <a name="limitations-in-ctp-releases"></a>Limitazioni nelle versioni di CTP

L'integrazione di R e Python in Linux è ancora in fase di sviluppo attivo. Le funzionalità seguenti non sono ancora abilitate nella versione di anteprima.

+ L'autenticazione implicita attualmente non è disponibile in Machine Learning Services. Ciò significa che non è possibile connettersi al server da uno script R o Python in esecuzione per accedere ai dati o ad altre risorse. 

### <a name="resource-governance"></a>Governance delle risorse

Esiste parità tra Linux e Windows per la [governance delle risorse](../t-sql/statements/create-external-resource-pool-transact-sql.md) per i pool di risorse esterni, ma le statistiche per [sys.dm_resource_governor_external_resource_pools](../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pools.md) hanno attualmente unità diverse in Linux. Le unità saranno allineate in una versione CTP futura.
 
| Nome colonna   | Descrizione | Valore in Linux | 
|---------------|--------------|---------------|
|peak_memory_kb | Quantità massima di memoria usata per il pool di risorse. | In Linux questa statistica è originata dal sottosistema di memoria CGroups, dove il valore è memory.max_usage_in_bytes |
|write_io_count | Il totale degli I/O di scrittura generati dalla reimpostazione delle statistiche di Resource Governor. | In Linux questa statistica è originata dal sottosistema blkio di CGroups, dove il valore nella riga di scrittura è blkio.throttle.io_serviced | 
|read_io_count | Il totale degli I/O di lettura generati dalla reimpostazione delle statistiche di Resource Governor. | In Linux questa statistica è originata dal sottosistema blkio di CGroups, dove il valore nella riga di lettura è blkio.throttle.io_serviced | 
|total_cpu_kernel_ms | Tempo del kernel dell'utente della CPU cumulativo, espresso in millisecondi, dalla reimpostazione delle statistiche di Resource Governor. | In Linux questa statistica è originata dal sottosistema cpuacct di CGroups, dove il valore nella riga dell'utente è cpuacct.stat |  
|total_cpu_user_ms | Tempo dell'utente della CPU cumulativo, espresso in millisecondi, dalla reimpostazione delle statistiche di Resource Governor.| In Linux questa statistica è originata dal sottosistema cpuacct di CGroups, dove il valore nella riga di sistema è cpuacct.stat | 
|active_processes_count | Numero di processi esterni in esecuzione al momento della richiesta.| In Linux questa statistica è originata dal sottosistema pids GGroups, dove il valore è pids.current | 

## <a name="next-steps"></a>Passaggi successivi

Gli sviluppatori R possono iniziare alcuni semplici esempi e con le nozioni di base sul funzionamento di R con SQL Server. Per il passaggio successivo, vedere i collegamenti seguenti:

+ [Esercitazione: Eseguire R in T-SQL](../advanced-analytics/tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)
+ [Esercitazione: Analisi nel database per sviluppatori R](../advanced-analytics/tutorials/sqldev-in-database-r-for-sql-developers.md)

Gli sviluppatori Python possono apprendere come usare Python con SQL Server seguendo queste esercitazioni:

+ [Esercitazione: Eseguire Python in T-SQL](../advanced-analytics/tutorials/run-python-using-t-sql.md)
+ [Esercitazione: Analisi nel database per sviluppatori Python](../advanced-analytics/tutorials/sqldev-in-database-python-for-sql-developers.md)

Per esempi di Machine Learning basati su scenari reali, vedere [Esercitazioni su Machine Learning](../advanced-analytics/tutorials/machine-learning-services-tutorials.md).
