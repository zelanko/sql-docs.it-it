---
title: Installare SQL Server Machine Learning Services (Python, R) in Linux
description: 'Informazioni su come installare SQL Server Machine Learning Services (Python e R) in Linux: Red Hat, Ubuntu e SUSE.'
author: cawrites
ms.author: chadam
ms.reviewer: vanto
manager: cgronlun
ms.date: 03/05/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: machine-learning
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: bf474ff8a7587c916591e6d7ba4dc82052b516f7
ms.sourcegitcommit: fc99fdd586eabc2d60f33056123398f263d5913d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/09/2020
ms.locfileid: "78937657"
---
# <a name="install-sql-server-machine-learning-services-python-and-r-on-linux"></a>Installare SQL Server Machine Learning Services (Python e R) in Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Questo articolo illustra l'installazione di [SQL Server Machine Learning Services](../advanced-analytics/index.yml) in Linux. Gli script Python e R possono essere eseguiti nel database usando Machine Learning Services.

[!NOTE]
> Machine Learning Services viene installato per impostazione predefinita nei cluster Big Data di SQL Server. Per altre informazioni, vedere [Usare Machine Learning Services (Python e R) in cluster Big Data](../big-data-cluster/machine-learning-services.md)

## <a name="what-are-machine-learning-services"></a>Che cos'è Machine Learning Services

Machine Learning Services è un componente aggiuntivo per le funzionalità per il motore di database.

Installare e configurare prima di tutto il motore di database di SQL Server in modo da poter risolvere eventuali problemi prima di aggiungere altri componenti.

## <a name="pre-install-checklist"></a>Elenco di controllo preliminare all'installazione

[Installare SQL Server in Linux](https://docs.microsoft.com/sql/linux/sql-server-linux-setup) e verificare l'installazione.

* Controllare i repository di SQL Server Linux per le estensioni Python e R. 
* Se i repository di origine per l'installazione del motore di database sono già stati configurati, è possibile eseguire i comandi di installazione del pacchetto **mssql-mlservices** usando la stessa registrazione dei repository.

* [Microsoft R Open](#mro) fornisce la distribuzione di R di base per la funzionalità R in SQL Server

* È necessario avere uno strumento per eseguire i comandi T-SQL. 
* Un editor di query è necessario per la configurazione e la convalida successiva all'installazione. 
* È consigliabile usare [Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/download?view=sql-server-2017#get-azure-data-studio-for-linux), scaricabile gratuitamente, che viene eseguito in Linux.


<a name="mro"></a>

### <a name="microsoft-r-open-mro-installation"></a>Installazione di Microsoft R Open (MRO)

La distribuzione di base di Microsoft di R è un prerequisito per l'uso di RevoScaleR, MicrosoftML e altri pacchetti R installati con Machine Learning Services.

La versione richiesta è MRO 3.5.2.

Per installare MRO, scegliere uno dei due approcci seguenti:

+ Scaricare il file tarball di MRO da MRAN, decomprimerlo ed eseguire lo script install.sh. Se si sceglie questo approccio, è possibile seguire le [istruzioni di installazione nella pagina di MRAN](https://mran.microsoft.com/releases/3.5.2).

+ Registrare il repository **packages.microsoft.com**, come descritto di seguito per installare la distribuzione di MRO: microsoft-r-open-mro e microsoft-r-open-mkl. 

<a name="RHEL"></a>

## <a name="install-on-redhat"></a>Installare in RedHat

### <a name="install-mro-on-red-hat"></a>Installare (MRO) in Red Hat

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

Opzioni di installazione per Python e R:

*  Installare il supporto della lingua in base ai propri requisiti (una o più lingue).
*  L'*installazione completa* include tutte le funzionalità disponibili, inclusi i modelli di Machine Learning con training preliminare.
*  L'*installazione minima* esclude i modelli ma include comunque tutte le funzionalità.

> [!Tip]
> Se possibile, eseguire `yum clean all` per aggiornare i pacchetti nel sistema prima dell'installazione.

### <a name="example-1----full-installation"></a>Esempio 1: Installazione completa

Include:
*  Python open source
*  R open source
*  Framework di estendibilità
*  microsoft-openmpi
*  Estensioni (Python, R)
*  Librerie di Machine Learning
*  Modelli con training preliminare per Python e R

```bash
# Install as root or sudo
# Add everything (all R, Python)
# Be sure to include -9.4.7* in mlsservices package names
sudo yum install mssql-mlservices-mlm-py-9.4.7*
sudo yum install mssql-mlservices-mlm-r-9.4.7*
```

### <a name="example-2---minimum-installation"></a>Esempio 2: Installazione minima

Include:
*  Python open source
*  R open source
*  Framework di estendibilità
*  microsoft-openmpi
*  Librerie Revo * principali
*  Librerie di Machine Learning

```bash
# Install as root or sudo
# Minimum install of R, Python extensions
# Be sure to include -9.4.6* in mlsservices package names
sudo yum install mssql-mlservices-packages-py-9.4.7*
sudo yum install mssql-mlservices-packages-r-9.4.7*
```
<a name="ubuntu"></a>

## <a name="install-on-ubuntu"></a>Installare in Ubuntu

### <a name="install-mro-on-ubuntu"></a>Installare (MRO) in Ubuntu

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

Opzioni di installazione per Python e R:

*  Installare il supporto della lingua in base ai propri requisiti (una o più lingue).
*  L'*installazione completa* include tutte le funzionalità disponibili, inclusi i modelli di Machine Learning con training preliminare.
*  L'*installazione minima* esclude i modelli ma include comunque tutte le funzionalità.

> [!Tip]
> Se possibile, eseguire `apt-get update` per aggiornare i pacchetti nel sistema prima dell'installazione. 

### <a name="example-1----full-installation"></a>Esempio 1: Installazione completa 

Include:
*  Python open source
*  R open source
*  Framework di estendibilità
*  microsoft-openmpi
*  Estensioni Python
*  Estensioni R
*  Librerie di Machine Learning
*  Modelli con training preliminare per Python e R

```bash
# Install as root or sudo
# Add everything (all R, Python)
# There is no asterisk in this full install
sudo apt-get install mssql-mlservices-mlm-py 
sudo apt-get install mssql-mlservices-mlm-r 
```

### <a name="example-2---minimum-installation"></a>Esempio 2: Installazione minima 

Include:
*  Python open source
*  R open source
*  Framework di estendibilità
*  microsoft-openmpi
*  Librerie Revo * principali
*  Librerie di Machine Learning

```bash
# Install as root or sudo
# Minimum install of R, Python
# No asterisk
sudo apt-get install mssql-mlservices-packages-py
sudo apt-get install mssql-mlservices-packages-r
```

<a name="SLES"></a>

## <a name="install-on-suse"></a>Installare in SUSE

### <a name="install-mro-on-susesles"></a>Installare (MRO) in SUSE (SLES)

```bash
# Install as root
sudo su

# Set the location of the package repo at the "prod" directory containing the distribution
# This example is for SLES12, the only supported version of SUSE in Machine Learning Server
zypper ar -f https://packages.microsoft.com/sles/12/prod packages-microsoft-com

# Update packages on your system (optional)
zypper update
```

Opzioni di installazione per Python e R:

*  Installare il supporto della lingua in base ai propri requisiti (una o più lingue).
*  L'*installazione completa* include tutte le funzionalità disponibili, inclusi i modelli di Machine Learning con training preliminare.
*  L'*installazione minima* esclude i modelli ma include comunque tutte le funzionalità.

### <a name="example-1----full-installation"></a>Esempio 1: Installazione completa 

Include:
*  Python open source
*  R open source
*  Framework di estendibilità
*  microsoft-openmpi
*  Estensioni per Python e R
*  Librerie di Machine Learning
*  Modelli con training preliminare per Python e R

```bash
# Install as root or sudo
# Add everything (all R, Python)
# Be sure to include -9.4.7* in mlsservices package names
sudo zypper install mssql-mlservices-mlm-py-9.4.7*
sudo zypper install mssql-mlservices-mlm-r-9.4.7* 
```

### <a name="example-2---minimum-installation"></a>Esempio 2: Installazione minima 

Include:
*  Python open source
*  R open source
*  Framework di estendibilità
*  microsoft-openmpi
*  Librerie Revo * principali
*  Librerie di Machine Learning 

```bash
# Install as root or sudo
# Minimum install of R, Python extensions
# Be sure to include -9.4.6* in mlsservices package names
sudo zypper install mssql-mlservices-packages-py-9.4.7*
sudo zypper install mssql-mlservices-packages-r-9.4.7*
```

## <a name="post-install-config-required"></a>Configurazione successiva all'installazione (obbligatoria)

La configurazione aggiuntiva viene eseguita principalmente tramite lo [strumento mssql-conf](sql-server-linux-configure-mssql-conf.md).


1. Aggiungere l'account utente mssql usato per eseguire il servizio SQL Server.

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

2. Accettare i contratti di licenza per le estensioni R e Python open source. Usare il comando seguente:

   ```bash
   # Run as SUDO or root
   # Use set + EULA 
   sudo /opt/mssql/bin/mssql-conf set EULA accepteulaml Y
   ```
3. Il programma di installazione rileva i pacchetti mssql-mlservices e richiede l'accettazione del contratto di licenza con l'utente finale (se non è stato precedentemente accettato) quando si esegue `mssql-conf setup`. Per altre informazioni sui parametri delle condizioni di licenza, vedere [Configurare SQL Server con lo strumento mssql conf](sql-server-linux-configure-mssql-conf.md#mlservices-eula).

4. Abilitare l'accesso alla rete in uscita. L'accesso alla rete in uscita è disabilitato per impostazione predefinita. Per abilitare le richieste in uscita, impostare la proprietà booleana "outboundnetworkaccess" usando lo strumento mssql-conf. Per altre informazioni, vedere [Configurare SQL Server in Linux con mssql conf](sql-server-linux-configure-mssql-conf.md#mlservices-outbound-access).

   ```bash
   # Run as SUDO or root
   # Enable outbound requests over the network
   sudo /opt/mssql/bin/mssql-conf set extensibility outboundnetworkaccess 1
   ```

5. Per integrare solo le funzionalità di R, impostare la variabile di ambiente **MKL_CBWR** in modo da [garantire un output coerente](https://software.intel.com/articles/introduction-to-the-conditional-numerical-reproducibility-cnr) dai calcoli di Intel Math Kernel Library (MKL).

   + Modificare o creare un file `named.bash_profile` nella home directory dell'utente, aggiungendo la riga `export MKL_CBWR="AUTO"` al file.

   + Eseguire questo file digitando `source.bash_profile` al prompt dei comandi di Bash.

6. Riavviare il servizio Launchpad di SQL Server e l'istanza del motore di database per leggere i valori aggiornati dal file INI. Quando viene modificata un'impostazione relativa all'estendibilità, viene visualizzato un messaggio di notifica.  

   ```bash
   systemctl restart mssql-launchpadd

   systemctl restart mssql-server.service
   ```

7. Abilitare l'esecuzione di script esterni usando Azure Data Studio o un altro strumento come SQL Server Management Studio (solo Windows) che esegue Transact-SQL. 

   ```bash
   EXEC sp_configure 'external scripts enabled', 1 
   RECONFIGURE WITH OVERRIDE 
   ```

7. Riavviare nuovamente il servizio Launchpad.

## <a name="verify-installation"></a>Verificare l'installazione

Le librerie R (MicrosoftML, RevoScaleR e altre) sono disponibili in `/opt/mssql/mlservices/libraries/RServer`.

Le librerie Python (microsoftml e revoscalepy) sono disponibili in `/opt/mssql/mlservices/libraries/PythonServer`.

Per convalidare l'installazione:

- Eseguire uno script T-SQL che esegue un stored procedure di sistema richiamando Python o R con uno strumento di query. 

Per Windows: 
*  Azure Data Studio
*  SQL Server Management Studio o PowerShell

Se si ha un computer Windows con questi strumenti, usarlo per connettersi all'installazione Linux del motore di database.

Eseguire il comando SQL seguente per testare l'esecuzione di R in SQL Server. Errori? Provare a riavviare il servizio, `sudo systemctl restart mssql-server.service`.

```
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

## <a name="unattended-installation"></a>Installazione automatica

Usando l'[installazione automatica](https://docs.microsoft.com/sql/linux/sql-server-linux-setup?view=sql-server-2017#unattended) per il motore di database, aggiungere i pacchetti per mssql-mlservices e le condizioni di licenza.

 Usare uno dei parametri EULA specifici di mlservices per le distribuzioni R e Python open source:

```bash
sudo /opt/mssql/bin/mssql-conf setup accept-eula-ml
```

Il contratto di licenza con l'utente finale completo è documentato in [Configurare SQL Server in Linux con lo strumento mssql conf](sql-server-linux-configure-mssql-conf.md#mlservices-eula).

## <a name="offline-installation"></a>Installazione offline

Per la procedura di installazione dei pacchetti, seguire le istruzioni contenute in [Installazione offline](sql-server-linux-setup.md#offline). Scaricare pacchetti specifici usando l'elenco di pacchetti riportato di seguito.

> [!Tip]
> Molti degli strumenti di gestione dei pacchetti forniscono comandi che consentono di determinare le dipendenze dei pacchetti. Per yum, usare `sudo yum deplist [package]`. Per Ubuntu, usare `sudo apt-get install --reinstall --download-only [package name]` seguito da `dpkg -I [package name].deb`.


#### <a name="download-site"></a>Sito di download

Scaricare i pacchetti da [https://packages.microsoft.com/](https://packages.microsoft.com/). Tutti i pacchetti mlservices per Python e R hanno un percorso condiviso con il pacchetto del motore di database. La versione di base per i pacchetti mlservices è la 9.4.6. Si ricordi che i pacchetti microsoft-r-open si trovano in un [repository diverso](#mro).

#### <a name="rhel7-paths"></a>Percorsi RHEL/7

|||
|--|----|
| Pacchetti mssql/mlservices | [https://packages.microsoft.com/rhel/7/mssql-server-2019/](https://packages.microsoft.com/rhel/7/mssql-server-2019/) |
| Pacchetti microsoft-r-open | [https://packages.microsoft.com/rhel/7/prod/](https://packages.microsoft.com/rhel/7/prod/) | 


#### <a name="ubuntu1604-paths"></a>Percorsi Ubuntu/16.04

|||
|--|----|
| Pacchetti mssql/mlservices | [https://packages.microsoft.com/ubuntu/16.04/mssql-server-2019/pool/main/m/](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2019/pool/main/m/) |
| Pacchetti microsoft-r-open | [https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/](https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/) | 

#### <a name="sles12-paths"></a>Percorsi SLES/12

|||
|--|----|
| Pacchetti mssql/mlservices | [https://packages.microsoft.com/sles/12/mssql-server-preview/](https://packages.microsoft.com/sles/12/mssql-server-preview/) |
| Pacchetti microsoft-r-open | [https://packages.microsoft.com/sles/12/prod/](https://packages.microsoft.com/sles/12/prod/) |

## <a name="package-list"></a>Elenco di pacchetti

Pacchetti di installazione disponibili:

| Nome del pacchetto | Applicabile a | Descrizione |
|--------------|----------|-------------|
|mssql-server-extensibility  | Tutti | Framework di estendibilità usato per eseguire Python e R. |
| microsoft-openmpi  | Python, R | Interfaccia per la trasmissione di messaggi usata dalle librerie Rev* per la parallelizzazione in Linux. |
| mssql-mlservices-python | Python | Distribuzione open source di Anaconda e Python. |
|mssql-mlservices-mlm-py  | Python | *Installazione completa*. Fornisce revoscalepy, microsoftml, modelli con training preliminare per la definizione di un immagine e l'analisi del sentiment del testo.| 
|mssql-mlservices-packages-py  | Python | *Installazione minima*. Fornisce revoscalepy e microsoftml. <br/>Esclude i modelli con training preliminare. | 
| [microsoft-r-open*](#mro) | R | Distribuzione open source di R, costituita da tre pacchetti. |
|mssql-mlservices-mlm-r  | R | *Installazione completa*. Fornisce: RevoScaleR, MicrosoftML, sqlRUtils, olapR, modelli con training preliminare per la definizione di un immagine e l'analisi del sentiment del testo.| 
|mssql-mlservices-packages-r  | R | *Installazione minima*. Fornisce RevoScaleR, sqlRUtils, MicrosoftML, olapR. <br/>Esclude i modelli con training preliminare. |

Selezionare le estensioni che si vogliono usare, scaricare i pacchetti necessari per una linguaggio specifico. I nomi dei file includono le informazioni sulla piattaforma nel suffisso.

Elenco di file:

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

## <a name="next-steps"></a>Passaggi successivi

Gli sviluppatori R possono iniziare alcuni semplici esempi e con le nozioni di base sul funzionamento di R con SQL Server. Per il passaggio successivo, vedere i collegamenti seguenti:

+ [Esercitazione: Eseguire R in T-SQL](../advanced-analytics/tutorials/quickstart-r-create-script.md)
+ [Esercitazione: Analisi nel database per sviluppatori R](../advanced-analytics/tutorials/sqldev-in-database-r-for-sql-developers.md)

Gli sviluppatori Python possono apprendere come usare Python con SQL Server seguendo queste esercitazioni:

+ [Esercitazione: Eseguire Python in T-SQL](../advanced-analytics/tutorials/run-python-using-t-sql.md)
+ [Esercitazione: Analisi nel database per sviluppatori Python](../advanced-analytics/tutorials/sqldev-in-database-python-for-sql-developers.md)

Per esempi di Machine Learning basati su scenari reali, vedere [Esercitazioni su Machine Learning](../advanced-analytics/tutorials/machine-learning-services-tutorials.md).
