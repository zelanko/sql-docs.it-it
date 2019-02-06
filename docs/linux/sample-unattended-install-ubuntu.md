---
title: Installazione automatica per SQL Server in Ubuntu
titleSuffix: SQL Server
description: Esempio di Script SQL Server - installazione automatica su Ubuntu
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/02/2017
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux, seodec18
ms.technology: linux
ms.openlocfilehash: c6327ae25e9e0b22310e810cd33f7176ecc1349d
ms.sourcegitcommit: 5ef24b3229b4659ede891b0af2125ef22bd94b96
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/06/2019
ms.locfileid: "55760054"
---
# <a name="sample-unattended-sql-server-installation-script-for-ubuntu"></a>Esempio: Script di installazione di SQL Server automatico per Ubuntu

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Questo script Bash di esempio consente di installare SQL Server 2017 su Ubuntu 16.04 senza input interattivo. Fornisce esempi di installazione del motore di database, strumenti da riga di comando di SQL Server, SQL Server Agent e vengono eseguiti i passaggi di post-installazione. È facoltativamente possibile installare la ricerca full-text e creare un utente amministratore.

> [!TIP]
> Se non è necessario uno script di installazione automatica, il modo più rapido per installare SQL Server consiste nel seguire il [Guida introduttiva per Ubuntu](quickstart-install-connect-ubuntu.md). Per altre informazioni sul programma di installazione, vedere [informazioni aggiuntive sull'installazione per SQL Server in Linux](sql-server-linux-setup.md).

## <a name="prerequisites"></a>Prerequisiti

- È necessario almeno 2 GB di memoria per l'esecuzione di SQL Server in Linux.
- Il file system deve essere **XFS** oppure **EXT4**. Altri file System, ad esempio **BTRFS**, non sono supportati.
- Per altri requisiti di sistema, vedere [requisiti di sistema per SQL Server in Linux](sql-server-linux-setup.md#system).

## <a name="sample-script"></a>Script di esempio

```bash
#!/bin/bash -e

# Use the following variables to control your install:

# Password for the SA user (required)
MSSQL_SA_PASSWORD='<YourStrong!Passw0rd>'

# Product ID of the version of SQL server you're installing
# Must be evaluation, developer, express, web, standard, enterprise, or your 25 digit product key
# Defaults to developer
MSSQL_PID='evaluation'

# Install SQL Server Agent (recommended)
SQL_INSTALL_AGENT='y'

# Install SQL Server Full Text Search (optional)
# SQL_INSTALL_FULLTEXT='y'

# Create an additional user with sysadmin privileges (optional)
# SQL_INSTALL_USER='<Username>'
# SQL_INSTALL_USER_PASSWORD='<YourStrong!Passw0rd>'

if [ -z $MSSQL_SA_PASSWORD ]
then
  echo Environment variable MSSQL_SA_PASSWORD must be set for unattended install
  exit 1
fi

echo Adding Microsoft repositories...
sudo curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
repoargs="$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017.list)"
sudo add-apt-repository "${repoargs}"
repoargs="$(curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list)"
sudo add-apt-repository "${repoargs}"

echo Running apt-get update -y...
sudo apt-get update -y

echo Installing SQL Server...
sudo apt-get install -y mssql-server

echo Running mssql-conf setup...
sudo MSSQL_SA_PASSWORD=$MSSQL_SA_PASSWORD \
     MSSQL_PID=$MSSQL_PID \
     /opt/mssql/bin/mssql-conf -n setup accept-eula

echo Installing mssql-tools and unixODBC developer...
sudo ACCEPT_EULA=Y apt-get install -y mssql-tools unixodbc-dev

# Add SQL Server tools to the path by default:
echo Adding SQL Server tools to your path...
echo PATH="$PATH:/opt/mssql-tools/bin" >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc

# Optional SQL Server Agent installation:
if [ ! -z $SQL_INSTALL_AGENT ]
then
  echo Installing SQL Server Agent...
  sudo apt-get install -y mssql-server-agent
fi

# Optional SQL Server Full Text Search installation:
if [ ! -z $SQL_INSTALL_FULLTEXT ]
then
    echo Installing SQL Server Full-Text Search...
    sudo apt-get install -y mssql-server-fts
fi

# Configure firewall to allow TCP port 1433:
echo Configuring UFW to allow traffic on port 1433...
sudo ufw allow 1433/tcp
sudo ufw reload

# Optional example of post-installation configuration.
# Trace flags 1204 and 1222 are for deadlock tracing.
# echo Setting trace flags...
# sudo /opt/mssql/bin/mssql-conf traceflag 1204 1222 on

# Restart SQL Server after installing:
echo Restarting SQL Server...
sudo systemctl restart mssql-server

# Connect to server and get the version:
counter=1
errstatus=1
while [ $counter -le 5 ] && [ $errstatus = 1 ]
do
  echo Waiting for SQL Server to start...
  sleep 3s
  /opt/mssql-tools/bin/sqlcmd \
    -S localhost \
    -U SA \
    -P $MSSQL_SA_PASSWORD \
    -Q "SELECT @@VERSION" 2>/dev/null
  errstatus=$?
  ((counter++))
done

# Display error if connection failed:
if [ $errstatus = 1 ]
then
  echo Cannot connect to SQL Server, installation aborted
  exit $errstatus
fi

# Optional new user creation:
if [ ! -z $SQL_INSTALL_USER ] && [ ! -z $SQL_INSTALL_USER_PASSWORD ]
then
  echo Creating user $SQL_INSTALL_USER
  /opt/mssql-tools/bin/sqlcmd \
    -S localhost \
    -U SA \
    -P $MSSQL_SA_PASSWORD \
    -Q "CREATE LOGIN [$SQL_INSTALL_USER] WITH PASSWORD=N'$SQL_INSTALL_USER_PASSWORD', DEFAULT_DATABASE=[master], CHECK_EXPIRATION=ON, CHECK_POLICY=ON; ALTER SERVER ROLE [sysadmin] ADD MEMBER [$SQL_INSTALL_USER]"
fi

echo Done!
```

### <a name="running-the-script"></a>Esecuzione dello script

Per eseguire lo script

1. Incollare il codice di esempio in un editor di testo e salvarlo con un nome facile da ricordare, ad esempio `install_sql.sh`.

1. Personalizzare `MSSQL_SA_PASSWORD`, `MSSQL_PID`e in tutte le altre variabili che si desidera modificare.

1. Contrassegnare lo script come eseguibile

   ```bash
   chmod +x install_sql.sh
   ```

1. Eseguire lo script

   ```bash
   ./install_sql.sh
   ```

### <a name="understanding-the-script"></a>Informazioni sullo script di
La prima operazione che esegue lo script Bash è impostare alcune variabili. Può trattarsi di variabili di scripting, come nell'esempio, o le variabili di ambiente. La variabile ``` MSSQL_SA_PASSWORD ``` viene **obbligatorio** dall'installazione di SQL Server, gli altri sono variabili personalizzate create per lo script. Lo script di esempio esegue i passaggi seguenti:

1. Importare le chiavi pubbliche GPG Microsoft.

1. Registrare il repository di Microsoft per SQL Server e gli strumenti da riga di comando.

1. Aggiornare il repository locale

1. Installare SQL Server

1. Configurare SQL Server con il ```MSSQL_SA_PASSWORD``` e accettare automaticamente il contratto di licenza dell'utente finale.

1. Accettare il contratto di licenza dell'utente finale per gli strumenti da riga di comando di SQL Server, installarli e installare il pacchetto unixodbc-dev automaticamente.

1. Aggiungere gli strumenti da riga di comando di SQL Server per il percorso per una maggiore facilità d'uso.

1. Installare SQL Server Agent, se la variabile di scripting ```SQL_INSTALL_AGENT``` , via per impostazione predefinita.

1. Se lo si desidera installare la ricerca Full-Text di SQL Server, se la variabile ```SQL_INSTALL_FULLTEXT``` è impostata.

1. Sblocca la porta 1433 per il protocollo TCP nel firewall del sistema, necessarie per connettersi a SQL Server da un altro sistema.

1. Facoltativamente, impostare i flag di traccia per la traccia di deadlock. (richiede rimosso le righe)

1. È ora installato SQL Server, per rendere operativa, riavviare il processo.

1. Verificare che SQL Server sia installato correttamente, nascondendo però eventuali messaggi di errore.

1. Creare un nuovo utente amministratore server, se ```SQL_INSTALL_USER``` e ```SQL_INSTALL_USER_PASSWORD``` sono entrambe impostate.

## <a name="next-steps"></a>Passaggi successivi

Semplificano più installazioni automatiche e creare uno script Bash autonomo che consente di impostare le variabili di ambiente appropriate. È possibile rimuovere una delle variabili dello script di esempio viene utilizzato e inserirle nel proprio script Bash.

```bash
#!/bin/bash
export MSSQL_SA_PASSWORD='<YourStrong!Passw0rd>'
export MSSQL_PID='evaluation'
export SQL_INSTALL_AGENT='y'
export SQL_INSTALL_USER='<Username>'
export SQL_INSTALL_USER_PASSWORD='<YourStrong!Passw0rd>'
export SQL_INSTALL_AGENT='y'
```

Quindi eseguire lo script Bash nel modo seguente:
```bash
. ./my_script_name.sh
```

Per altre informazioni su SQL Server in Linux, vedere [SQL Server in Linux Panoramica](sql-server-linux-overview.md).
