---
title: Installare SQL Server Machine Learning Services (R, Python, Java) in Linux | Microsoft Docs
description: Informazioni su come installare SQL Server Machine Learning Services (R, Python, Java) su Ubuntu e Red Hat.
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.date: 02/28/2019
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: machine-learning
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 833c6f2083d9532ecc4120e5f65be81a75a86d24
ms.sourcegitcommit: 8bc5d85bd157f9cfd52245d23062d150b76066ef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/07/2019
ms.locfileid: "57579526"
---
# <a name="install-sql-server-2019-machine-learning-services-r-python-java-on-linux"></a>Installare SQL Server 2019 Machine Learning Services (R, Python, Java) in Linux

[SQL Server Machine Learning Services](../advanced-analytics/what-is-sql-server-machine-learning.md) viene eseguito nei sistemi operativi Linux a partire da questa versione di anteprima di SQL Server 2019. Seguire i passaggi descritti in questo articolo per installare l'estensione di programmazione Java, o le estensioni di apprendimento per R e Python. 

Machine learning e le estensioni di programmazione è un componente aggiuntivo per il motore di database. Sebbene sia possibile [installare il motore di database e servizi di Machine Learning contemporaneamente](#install-all), è consigliabile installare e configurare il motore di database di SQL Server prima di tutto in modo da poter risolvere eventuali problemi prima di aggiungerne altri componenti. 

Percorso del pacchetto per le estensioni R, Python e Java sono nei repository di origine Linux di SQL Server. Se è già configurato repository del codice sorgente per l'installazione del motore di database, è possibile eseguire la **mssql-mlservices** i comandi di installazione usando la stessa registrazione del repository del pacchetto.

## <a name="uninstall-previous-ctp"></a>Versione CTP precedente di disinstallazione

L'elenco dei pacchetti è stato modificato nelle ultime versioni CTP diversi, generando un minor numero di pacchetti. È consigliabile disinstallare CTP 2.x in modo da rimuovere tutti i pacchetti precedenti prima dell'installazione di versioni da CTP 2.3. Installazione side-by-side di più versioni non è supportata.

### <a name="1-confirm-package-installation"></a>1. Confermare l'installazione del pacchetto

È possibile verificare l'esistenza di un'installazione precedente come primo passaggio. I file seguenti indicano un'installazione esistente: checkinstallextensibility.sh, exthost, launchpad.

```bash
ls /opt/microsoft/mssql/bin
```

### <a name="2-uninstall-ctp-20-or-21-packages"></a>2. Disinstallare 2.1 pacchetti o versioni da CTP 2.0

Disinstallare a livello di pacchetto più basso. Qualsiasi pacchetto upstream dipende da un pacchetto di livello inferiore viene automaticamente disinstallato.

  + Per l'integrazione di R, rimuovere **microsoft-r-open***
  + Per l'integrazione di Python, rimuovere **mssql-mlservices-python**
  + Per l'integrazione di Java, rimuovere **mssql-server-extensibility-java**

Comandi per la rimozione dei pacchetti vengono visualizzati nella tabella seguente.

| Piattaforma  | Comandi di rimozione pacchetto | 
|-----------|----------------------------|
| RHEL  | `sudo yum remove microsoft-r-open-mro-3.4.4`<br/>`sudo yum remove msssql-mlservices-python`<br/>`sudo yum remove msssql-server-extensibility-java` |
| SLES  | `sudo zypper remove microsoft-r-open-mro-3.4.4`<br/>`sudo zypper remove msssql-mlservices-python`<br/>`sudo zypper remove msssql-server-extensibility-java` |
| Ubuntu    | `sudo apt-get remove microsoft-r-open-mro-3.4.4`<br/>`sudo apt-get remove msssql-mlservices-python`<br/>`sudo apt-get remove msssql-server-extensibility-java`|

> [!Note]
> Microsoft R Open è composto da tre pacchetti. Se uno di questi pacchetti rimangono dopo aver rimosso microsoft-r-open-mro-3.4.4, è necessario rimuoverli singolarmente.
> ```
> microsoft-r-open-foreachiterators-3.4.4
> microsoft-r-open-mkl-3.4.4
> microsoft-r-open-mro-3.4.4
> ```

### <a name="3-proceed-with-ctp-23-install"></a>3. Procedere con l'installazione di versioni da CTP 2.3

Installare il massimo livello di pacchetto seguendo le istruzioni riportate in questo articolo per il sistema operativo.

Per ogni set di specifiche del sistema operativo di istruzioni di installazione *massimo livello di pacchetto* può essere **esempio 1: installazione completa** per il set completo di pacchetti, o **esempio 2 - installazione minima**  per il minor numero di pacchetti necessari per un'installazione valida.

1. Per l'integrazione di R, iniziare con [MRO](#mro) perché è un prerequisito. Integrazione di R non verrà installato senza di essa.

2. Eseguire i comandi di installazione usando la sintassi e i gestori di pacchetti per il sistema operativo: 

   + [RedHat](#RHEL)
   + [Ubuntu](#ubuntu)
   + [SUSE](#SUSE)

## <a name="prerequisites"></a>Prerequisiti

+ La versione di Linux deve essere [supportati da SQL Server](sql-server-linux-release-notes-2019.md#supported-platforms), ma non include il motore Docker. Le versioni supportate sono:

   + [Red Hat Enterprise Linux (RHEL)](quickstart-install-connect-red-hat.md)

   + [SUSE Enterprise Linux Server](quickstart-install-connect-suse.md)

   + [Ubuntu](quickstart-install-connect-ubuntu.md)

+ (Solo R) [Microsoft R Open](#mro) la distribuzione di R di base per la funzionalità di R in SQL Server

+ È necessario uno strumento per l'esecuzione di comandi T-SQL. Un editor di query è necessario per la convalida e configurazione di post-installazione. È consigliabile [Studio di Azure Data](https://docs.microsoft.com/sql/azure-data-studio/download?view=sql-server-2017#get-azure-data-studio-for-linux), un download gratuito che viene eseguito in Linux.

<a name="mro"></a>

### <a name="microsoft-r-open-mro-installation"></a>Installazione di Microsoft R Open (MRO)

Distribuzione di base di Microsoft di R è un prerequisito per l'uso di RevoScaleR, MicrosoftML e altri pacchetti R installati con i servizi di Machine Learning.

La versione richiesta è MRO 3.4.4.

Scegliere tra i due approcci seguenti per installare MRO:

+ Scaricare il file tarball MRO da MRAN, decomprimerlo ed eseguire lo script install.sh. È possibile seguire le [istruzioni di installazione su MRAN](https://mran.microsoft.com/releases/3.4.4) se si desidera che questo approccio.

+ In alternativa, registrare il **packages.microsoft.com** repository come descritto di seguito per installare i pacchetti di tre che comprendono la distribuzione MRO: microsoft-r-open-mro, microsoft-r-open-mkl, e Microsoft-r-open-foreachiterators. 

I comandi seguenti registrare il repository fornendo MRO. Post-registrazione, i comandi per installare altri pacchetti R, ad esempio mssql-mlservices-mml-r, includerà automaticamente MRO come una dipendenza del pacchetto.

#### <a name="mro-on-ubuntu"></a>MRO in Ubuntu

```bash
# Install as root
sudo su

# Optionally, if your system does not have the https apt transport option
apt-get install apt-transport-https

# Add the **azure-cli** repo to your apt sources list
AZ_REPO=$(lsb_release -cs)

echo "deb [arch=amd64] https://packages.microsoft.com/repos/azure-cli/ $AZ_REPO main" | sudo tee /etc/apt/sources.list.d/azure-cli.list

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

# Create local `azure-cli` repository
sudo sh -c 'echo -e "[azure-cli]\nname=Azure CLI\nbaseurl=https://packages.microsoft.com/yumrepos/azure-cli\nenabled=1\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" > /etc/yum.repos.d/azure-cli.repo'

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

## <a name="package-list"></a>Elenco dei pacchetti

In un dispositivo connesso a internet, i pacchetti vengono scaricati e installati indipendentemente dal motore di database mediante il programma di installazione del pacchetto per ogni sistema operativo. La tabella seguente descrive tutti i pacchetti disponibili, ma per R e Python, si specificano pacchetti che forniscono l'installazione completa di funzionalità o l'installazione della funzionalità minima.

| Nome pacchetto | Si applica a | Descrizione |
|--------------|----------|-------------|
|mssql-server-extensibility  | All | Framework di estendibilità utilizzato per eseguire codice R, Python o Java. |
|mssql-server-extensibility-java | Java | Estensione di Java per il caricamento di un ambiente di esecuzione di Java. Non esistono altre librerie o pacchetti per Java. |
| microsoft-openmpi  | Python, R | Interfaccia utilizzata dalle librerie Revo * per la parallelizzazione in Linux di passaggio dei messaggi. |
| mssql-mlservices-python | Python | Distribuzione di open source di Python e Anaconda. |
|mssql-mlservices-mlm-py  | Python | *Installazione completa*. Fornisce revoscalepy, microsoftml, pre-training di modelli per l'analisi del sentiment definizione delle funzionalità e il testo di immagine.| 
|mssql-mlservices-packages-py  | Python | *Installazione minima*. Fornisce microsoftml e revoscalepy. <br/>Esclude i modelli con training preliminare. | 
| [microsoft-r-open*](#mro) | R | Distribuzione open source di R, è costituito da tre pacchetti. |
|mssql-mlservices-mlm-r  | R | *Installazione completa*. Fornisce RevoScaleR, MicrosoftML, sqlRUtils, olapR, pre-training di modelli per l'analisi del sentiment definizione delle funzionalità e il testo di immagine.| 
|mssql-mlservices-packages-r  | R | *Installazione minima*. Provides RevoScaleR, sqlRUtils, MicrosoftML, olapR. <br/>Esclude i modelli con training preliminare. | 
|mssql-mlservices-mml-py  | Solo CTP 2.0, 2.1 | Obsoleto in CTP 2.2 a causa di un consolidamento del pacchetto di Python in mssql-mslservices-python. Fornisce revoscalepy. Esclude microsoftml e modelli con training preliminare.| 
|mssql-mlservices-mml-r  | Solo CTP 2.0, 2.1 | Obsoleto in CTP 2.2 a causa di consolidamento di pacchetti R in mssql-mslservices-python. Provides RevoScaleR, sqlRUtils, olapR. Esclude MicrosoftML e modelli con training preliminare.  |

<a name="RHEL"></a>

## <a name="rhel-commands"></a>Comandi RHEL

È possibile installare il supporto linguistico in qualsiasi combinazione desiderata (uno o più linguaggi). Per R e Python, sono disponibili due pacchetti tra cui scegliere. Uno fornisce tutte le funzionalità disponibili, caratterizzate come le *installazione completa*. La scelta alternativa esclude pre-addestrati modelli di machine learning e viene considerata il *installazione minima*.

> [!Tip]
> Se possibile, eseguire `yum clean all` per aggiornare i pacchetti nel sistema prima dell'installazione.

### <a name="example-1----full-installation"></a>Esempio 1: installazione completa 

Include open source R e Python, il framework di estendibilità, microsoft-openmpi, le estensioni (R, Python, Java), con librerie di machine learning e i modelli con training preliminare per R e Python. 

```bash
# Install as root or sudo
# Add everything (all R, Python, Java)
# Be sure to include -9.4.6* in mlsservices package names
sudo yum install mssql-mlservices-mlm-py-9.4.6*
sudo yum install mssql-mlservices-mlm-r-9.4.6* 
sudo yum install mssql-server-extensibility-java
```

### <a name="example-2---minimum-installation"></a>Esempio 2: installazione minima 

Include open source R e Python, il framework di estendibilità, microsoft-openmpi, Revo * librerie di core e librerie di machine learning per R e Python e Java extension. Esclude i modelli con training preliminare.

```bash
# Install as root or sudo
# Minimum install of R, Python, Java extensions
# Be sure to include -9.4.6* in mlsservices package names
sudo yum install mssql-mlservices-packages-py-9.4.6*
sudo yum install mssql-mlservices-packages-r-9.4.6*
sudo yum install mssql-server-extensibility-java
```

<a name="ubuntu"></a>

## <a name="ubuntu-commands"></a>Comandi di Ubuntu

È possibile installare il supporto linguistico in qualsiasi combinazione desiderata (uno o più linguaggi). Per R e Python, sono disponibili due pacchetti tra cui scegliere. Uno fornisce tutte le funzionalità disponibili, caratterizzate come le *installazione completa*. La scelta alternativa esclude pre-addestrati modelli di machine learning e viene considerata il *installazione minima*.

> [!Tip]
> Se possibile, eseguire `apt-get update` per aggiornare i pacchetti nel sistema prima dell'installazione. Inoltre, alcune immagini docker di Ubuntu potrebbero non avere l'opzione di apt trasporto https. Per installarlo, usare `apt-get install apt-transport-https`.

<!---
### Prerequisite for 18.04

Running mssql-mlservices R libraries on Ubuntu 18.04 requires **libpng12** from the Linux Kernel archives. This package is no longer included in the standard distribution and must be installed manually. To get this library, run the following commands:

```bash
wget https://mirrors.kernel.org/ubuntu/pool/main/libp/libpng/libpng12-0_1.2.54-1ubuntu1_amd64.deb
dpkg -i libpng12-0_1.2.54-1ubuntu1_amd64.deb
```--->

### <a name="example-1----full-installation"></a>Esempio 1: installazione completa 

Include open source R e Python, il framework di estendibilità, microsoft-openmpi, le estensioni (R, Python, Java), con librerie di machine learning e i modelli con training preliminare per R e Python. 

```bash
# Install as root or sudo
# Add everything (all R, Python, Java)
# There is no asterisk in this full install
sudo apt-get install mssql-mlservices-mlm-py 
sudo apt-get install mssql-mlservices-mlm-r 
sudo apt-get install mssql-server-extensibility-java
```

### <a name="example-2---minimum-installation"></a>Esempio 2: installazione minima 

Include open source R e Python, il framework di estendibilità, microsoft-openmpi, Revo * librerie di core e librerie di machine learning per R e Python e Java extension. Esclude i modelli con training preliminare. 

```bash
# Install as root or sudo
# Minimum install of R, Python, Java
# No aasterisk
sudo apt-get install mssql-mlservices-packages-py
sudo apt-get install mssql-mlservices-packages-r
sudo apt-get install mssql-server-extensibility-java
```

<a name="suse"></a>

## <a name="suse-commands"></a>Comandi SUSE

È possibile installare il supporto linguistico in qualsiasi combinazione desiderata (uno o più linguaggi). Per R e Python, sono disponibili due pacchetti tra cui scegliere. Uno fornisce tutte le funzionalità disponibili, caratterizzate come le *installazione completa*. La scelta alternativa esclude pre-addestrati modelli di machine learning e viene considerata il *installazione minima*.

### <a name="example-1----full-installation"></a>Esempio 1: installazione completa 

Include open source R e Python, il framework di estendibilità, microsoft-openmpi, le estensioni (R, Python, Java), con librerie di machine learning e i modelli con training preliminare per R e Python. 

```bash
# Install as root or sudo
# Add everything (all R, Python, Java)
# Be sure to include -9.4.6* in mlsservices package names
sudo zypper install mssql-mlservices-mlm-py-9.4.6*
sudo zypper install mssql-mlservices-mlm-r-9.4.6* 
sudo zypper install mssql-server-extensibility-java
```

### <a name="example-2---minimum-installation"></a>Esempio 2: installazione minima 

Include open source R e Python, il framework di estendibilità, microsoft-openmpi, Revo * librerie di core e librerie di machine learning per R e Python e Java extension. Esclude i modelli con training preliminare. 

```bash
# Install as root or sudo
# Minimum install of R, Python, Java extensions
# Be sure to include -9.4.6* in mlsservices package names
sudo zypper install mssql-mlservices-packages-py-9.4.6*
sudo zypper install mssql-mlservices-packages-r-9.4.6*
sudo zypper install mssql-server-extensibility-java
```

## <a name="post-install-config-required"></a>Configurazione di post-installazione (obbligatorio)

Configurazione aggiuntiva viene eseguito principalmente tramita il [lo strumento mssql-conf](sql-server-linux-configure-mssql-conf.md).


1. Aggiungere l'account utente mssql utilizzato per eseguire il servizio SQL Server. È obbligatorio se è stato ancora eseguito il programma di installazione in precedenza.

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

2. Accettare il contratto di licenza di R e Python open source. Esistono diversi modi per eseguire questa operazione. Se in precedenza accettati licenza di SQL Server e si siano aggiungendo a questo punto le estensioni R o Python, il comando seguente è il tuo consenso delle condizioni:

   ```bash
   # Run as SUDO or root
   # Use set + EULA 
   sudo /opt/mssql/bin/mssql-conf set EULA accepteulaml Y
   ```

   Un flusso di lavoro alternativo è che, se non si ha ancora accettato il motore di database di SQL Server contratto di licenza, il programma di installazione rileva mssql-mlservices pacchetti e istruzioni per l'accettazione delle condizioni di licenza quando `mssql-conf setup` viene eseguito. Per altre informazioni sui parametri di condizioni di licenza, vedere [configurare SQL Server con lo strumento mssql-conf](sql-server-linux-configure-mssql-conf.md#mlservices-eula).

3. Abilitare l'accesso alla rete in uscita. Accesso alla rete in uscita è disabilitata per impostazione predefinita. Per abilitare le richieste in uscita, impostare "outboundnetworkaccess" proprietà Boolean utilizzando lo strumento mssql-conf. Per altre informazioni, vedere [configurare SQL Server in Linux con mssql-conf](sql-server-linux-configure-mssql-conf.md#mlservices-outbound-access).

   ```bash
   # Run as SUDO or root
   # Enable outbound requests over the network
   sudo /opt/mssql/bin/mssql-conf set extensibility outboundnetworkaccess 1
   ```

4. Per R di funzionalità di integrazione solo, imposta il **MKL_CBWR** variabile di ambiente [garantire coerenti con l'output](https://software.intel.com/articles/introduction-to-the-conditional-numerical-reproducibility-cnr) dai calcoli Intel Math Kernel Library (MKL).

   + Modificare o creare un file denominato **file con estensione bash_profile** nella home directory utente, aggiungendo la riga `export MKL_CBWR="AUTO"` al file.

   + Eseguire questo file digitando `source .bash_profile` un prompt dei comandi bash.

5. Riavviare il servizio Launchpad di SQL Server e l'istanza del motore di database per leggere i valori aggiornati dal file INI. Ricorda di un messaggio di riavvio ogni volta che viene modificata un'impostazione di estendibilità.  

   ```bash
   systemctl restart mssql-launchpadd

   systemctl restart mssql-server.service
   ```

6. Abilitare l'esecuzione dello script esterno usando Azure Data Studio o un altro strumento come SQL Server Management Studio (solo Windows) che esegue Transact-SQL. 

   ```bash
   EXEC sp_configure 'external scripts enabled', 1 
   RECONFIGURE WITH OVERRIDE 
   ```

7. Riavviare il servizio Launchpad di nuovo.

## <a name="verify-installation"></a>Verificare l'installazione

Librerie di R (MicrosoftML, RevoScaleR e ad altri utenti) sono reperibile in `/opt/mssql/mlservices/libraries/RServer`.

Le librerie Python (microsoftml e revoscalepy) sono reperibile in `/opt/mssql/mlservices/libraries/PythonServer`.

Integrazione delle funzionalità Java non include le librerie, ma è possibile eseguire `grep -r JAVA_HOME /etc` per confermare la creazione della variabile di ambiente JAVA_HOME.

Per convalidare l'installazione, eseguire uno script T-SQL che esegue una stored procedure di sistema il richiamo di R o Python. È necessario uno strumento di query per questa attività. Azure Data Studio è una scelta ottimale. Altri utilizzati di frequente strumenti come SQL Server Management Studio o PowerShell sono solo Windows. Se si dispone di un computer Windows con questi strumenti, usarlo per connettersi all'installazione di Linux del motore di database.

Eseguire il comando SQL seguente per testare l'esecuzione di R in SQL Server. Se non viene eseguito lo script, provare a riavviare il servizio, `sudo systemctl restart mssql-server.service`.

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

## <a name="chained-combo-install"></a>Installa concatenata "combinata"

È possibile installare e configurare il motore di database e servizi di Machine Learning in una procedura mediante l'aggiunta di pacchetti R, Python o Java e i parametri in un comando che installa il motore di database. 

1. Per l'integrazione di R, installare [Microsoft R Open](#mro) come prerequisito. Se non si installa la funzionalità R, ignorare questo passaggio.

2. Fornire una riga di comando che include il motore di database, oltre a funzionalità di estensione del linguaggio.

  È possibile aggiungere una singola funzione, ad esempio Java installare integrazione, per un motore di database.

  ```bash
  sudo yum install -y mssql-server mssql-server-extensibility-java 
  ```

  In alternativa, aggiungere tutte le estensioni (Java, R, Python).

  ```bash
  sudo yum install -y mssql-server mssql-server-extensibility-java mssql-mlservices-packages-r-9.4.6* mssql-mlservices-packages-py-9.4.6*
  ```

3. Accettare i contratti di licenza e completare la configurazione di post-installazione. Usare la **mssql-conf** dello strumento per questa attività.

  ```bash
  sudo /opt/mssql/bin/mssql-conf setup
  ```

  Verrà richiesto di accettare il contratto di licenza per il motore di database, scegliere un'edizione e impostare la password dell'amministratore. Inoltre richiesto di accettare il contratto di licenza per i servizi di Machine Learning.

4. Riavviare il servizio, se viene richiesto di farlo.

  ```bash
  sudo systemctl restart mssql-server.service
  ```

## <a name="unattended-installation"></a>Installazione automatica

Usando il [installazione automatica](https://docs.microsoft.com/sql/linux/sql-server-linux-setup?view=sql-server-2017#unattended) per il motore di Database, aggiungere i pacchetti per mssql-mlservices ed EULA.

È importante ricordare che il programma di installazione o lo strumento mssql-conf richiesta per l'accettazione di contratto di licenza. Se è già configurato il motore di database di SQL Server e accettato le condizioni di licenza, usare uno dei parametri mlservices specifiche condizioni di licenza per le distribuzioni di R e Python open source:

```bash
sudo /opt/mssql/bin/mssql-conf setup accept-eula-ml
```

Tutte le possibili permutazioni di accettazione del contratto sono documentate in [configurare SQL Server in Linux con lo strumento mssql-conf](sql-server-linux-configure-mssql-conf.md#mlservices-eula).

## <a name="offline-installation"></a>Installazione offline

Seguire le [installazione Offline](sql-server-linux-setup.md#offline) istruzioni per la procedura di installazione dei pacchetti. Trovare il sito di download e quindi scaricare pacchetti specifici usando l'elenco dei pacchetti riportato di seguito.

> [!Tip]
> Molti degli strumenti di gestione pacchetti forniscono comandi utili per determinano le dipendenze dei pacchetti. Per yum, usare `sudo yum deplist [package]`. Per Ubuntu, utilizzare `sudo apt-get install --reinstall --download-only [package name]` seguita da `dpkg -I [package name].deb`.


#### <a name="download-site"></a>Sito di download

È possibile scaricare i pacchetti da [ https://packages.microsoft.com/ ](https://packages.microsoft.com/). Tutti i pacchetti mlservices per R, Python e Java sono collocati insieme ai pacchetti di motore di database. Versione di base per i pacchetti mlservices è 9.4.5 (per CTP 2.0) 9.4.6 (per CTP 2.1 e versioni successive). Tenere presente che i pacchetti r-microsoft-open si trovano in un [diversi repository](#mro).

#### <a name="rhel7-paths"></a>Percorsi RHEL/7

|||
|--|----|
| MSSQL/mlservices pacchetti | [https://packages.microsoft.com/rhel/7/mssql-server-preview/](https://packages.microsoft.com/rhel/7/mssql-server-preview/) |
| pacchetti r-Microsoft-open | [https://packages.microsoft.com/rhel/7/prod/](https://packages.microsoft.com/rhel/7/prod/) | 


#### <a name="ubuntu1604-paths"></a>Percorsi/Ubuntu 16.04

|||
|--|----|
| MSSQL/mlservices pacchetti | [https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/) |
| pacchetti r-Microsoft-open | [https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/](https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/) | 

#### <a name="sles12-paths"></a>Percorsi SLES 12

|||
|--|----|
| MSSQL/mlservices pacchetti | [https://packages.microsoft.com/sles/12/mssql-server-preview/](https://packages.microsoft.com/sles/12/mssql-server-preview/) |
| pacchetti r-Microsoft-open | [https://packages.microsoft.com/sles/12/prod/](https://packages.microsoft.com/sles/12/prod/) | 

#### <a name="package-list"></a>Elenco dei pacchetti

A seconda le estensioni che si desidera utilizzare, scaricare i pacchetti necessari per una lingua specifica. I nomi file esatti includono informazioni sulla piattaforma nel suffisso, ma i nomi di file riportato di seguito devono essere sufficientemente vicine per determinare i file da ottenere.

```
# Core packages 
mssql-server-15.0.1000
mssql-server-extensibility-15.0.1000

# Java
mssql-server-extensibility-java-15.0.1000

# R
microsoft-openmpi-3.0.0
microsoft-r-open-foreachiterators-3.4.4
microsoft-r-open-mkl-3.4.4
microsoft-r-open-mro-3.4.4
mssql-mlservices-packages-r-9.4.6.523
mssql-mlservices-mlm-r-9.4.6.523
mssql-mlservices-mml-r-9.4.6.523

# Python
microsoft-openmpi-3.0.0
mssql-mlservices-python-9.4.6.523
mssql-mlservices-packages-py-9.4.6.523
mssql-mlservices-mlm-py-9.4.6.523
mssql-mlservices-mml-py-9.4.6.523
```

#### <a name="package-list-for-original-ctp-20-and-21"></a>Elenco dei pacchetti originali versioni da CTP 2.0 e 2.1

CTP 2.2 Rimuove **mssql-mlservices-mlm-py** e **mssql-mlservices-mlm-r** attraverso il consolidamento di pacchetto in **mssql-mlservices-package-py** e**mssql-mlservices pacchetti r**, rispettivamente.

Se sono necessarie in modo specifico l'originale di versioni da CTP 2.0 o 2.1 pacchetti, scaricare i pacchetti seguenti:

* Per versioni da CTP 2.0, scaricare le versioni dei pacchetti 9.4.5

* Per la versione CTP 2.1, scaricare le versioni dei pacchetti 9.4.6.237


## <a name="add-more-rpython-packages"></a>Aggiunta di altri pacchetti R o Python 
 
È possibile installare altri pacchetti R e Python e utilizzarli nello script che esegue SQL Server 2019.

### <a name="r-packages"></a>Pacchetti R 
 
1. Avviare una sessione R.

   ```r
   # sudo /opt/mssql/mlservices/bin/R/R 
   ```

2. Installare un pacchetto R chiamato [glue](https://mran.microsoft.com/package/glue) per testare l'installazione del pacchetto.

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
 
1. Installare un pacchetto di Python denominato [httpie](https://httpie.org/) tramite pip. 

   ```python
   # sudo /opt/mssql/mlservices/bin/python/python -m pip install httpie 
   ``` 

2. Importare il pacchetto di Python nelle [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).
 
   ```python
   EXEC sp_execute_external_script  
   @language = N'Python',  
   @script = N'import httpie' 
   ```

## <a name="limitations-in-ctp-releases"></a>Limitazioni nelle versioni CTP

Integrazione di R, Python e Java in Linux è ancora in fase di sviluppo. Le funzionalità seguenti non sono ancora abilitate nella versione di anteprima.

+ L'autenticazione implicita non è attualmente disponibile in servizi di Machine Learning in Linux a questo punto, il che significa che non è possibile connettersi al server da uno script in corso di R o Python per accedere a dati o altre risorse. 

+ [CREATE EXTERNAL LIBRARY](../t-sql/statements/create-external-library-transact-sql.md) (per l'archiviazione dei pacchetti R nel database) non è attualmente disponibile in Linux e non supporta Python.  

### <a name="resource-governance"></a>Governance delle risorse

È disponibile la parità tra Linux e Windows per [governance delle risorse](../t-sql/statements/create-external-resource-pool-transact-sql.md) per il pool di risorse esterne, ma le statistiche per [sys.dm_resource_governor_external_resource_pools](../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pools.md) dispone attualmente unità di misura diversa in Linux. Le unità vengono allineati in una versione CTP successiva.
 
| Nome colonna   | Descrizione | Valore in Linux | 
|---------------|--------------|---------------|
|peak_memory_kb | La quantità massima di memoria utilizzata per il pool di risorse. | In Linux, questa statistica è originata dal sottosistema di memoria Cgroup, dove il valore è memory.max_usage_in_bytes |
|write_io_count | Totale scrittura generati dalla reimpostazione delle statistiche di Resource Governor. | In Linux, questa statistica è originata dal sottosistema di blkio Cgroup, dove il valore della riga di scrittura è blkio.throttle.io_serviced | 
|read_io_count | Il totale di lettura generati dalla reimpostazione delle statistiche di Resource Governor. | In Linux, questa statistica è originata dal sottosistema di blkio Cgroup, in cui valore della riga di lettura è blkio.throttle.io_serviced | 
|total_cpu_kernel_ms | CPU utente kernel tempo totale espresso in millisecondi, reimpostazione delle statistiche di Resource Governor. | In Linux, questa statistica è originata dal sottosistema di cpuacct Cgroup, dove il valore nella riga dell'utente è cpuacct.stat |  
|total_cpu_user_ms | Tempo cumulativo della CPU di un utente espresso in millisecondi, reimpostazione delle statistiche di Resource Governor.| In Linux, questa statistica è originata dal sottosistema di cpuacct Cgroup, dove il valore per il valore di riga del sistema è cpuacct.stat | 
|active_processes_count | Il numero di processi esterni in esecuzione al momento della richiesta.| In Linux, questa statistica è originata dal sottosistema dei PID GGroups, dove il valore è pids.current | 

## <a name="next-steps"></a>Passaggi successivi

Gli sviluppatori di R possono iniziare a usare alcuni semplici esempi e informazioni di base del funzionamento di R con SQL Server. Per il passaggio successivo, vedere i collegamenti seguenti:

+ [Esercitazione: Eseguire R in T-SQL](../advanced-analytics/tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)
+ [Esercitazione: Analitica nel database per gli sviluppatori di R](../advanced-analytics/tutorials/sqldev-in-database-r-for-sql-developers.md)

Gli sviluppatori di Python è possono imparare a usare Python con SQL Server seguendo queste esercitazioni:

+ [Esercitazione: Eseguire Python in T-SQL](../advanced-analytics/tutorials/run-python-using-t-sql.md)
+ [Esercitazione: Analitica nel database per sviluppatori Python](../advanced-analytics/tutorials/sqldev-in-database-python-for-sql-developers.md)

Per visualizzare esempi di machine learning basate su scenari reali, vedere [di Machine learning esercitazioni](../advanced-analytics/tutorials/machine-learning-services-tutorials.md).
