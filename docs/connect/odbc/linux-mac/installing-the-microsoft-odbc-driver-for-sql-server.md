---
title: Installazione di Microsoft ODBC Driver for SQL Server in Linux e macOS | Microsoft Docs
ms.custom: ''
ms.date: 12/04/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- driver, installing
ms.assetid: f78b81ed-5214-43ec-a600-9bfe51c5745a
author: MightyPen
ms.author: v-jizho2
manager: kenvh
ms.openlocfilehash: 5f9392d0ba5b07a489caffdd2e496051e842b1c8
ms.sourcegitcommit: 38076f423663bdbb42f325e3d0624264e05beda1
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 12/06/2018
ms.locfileid: "52984062"
---
# <a name="installing-the-microsoft-odbc-driver-for-sql-server-on-linux-and-macos"></a>Installazione di Microsoft ODBC Driver for SQL Server in Linux e macOS
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

Questo articolo illustra come installare il [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in Linux e macOS, nonché gli strumenti da riga di comando facoltativa per SQL Server (`bcp` e `sqlcmd`) e di sviluppo intestazioni unixODBC.

## <a name="microsoft-odbc-driver-17-for-sql-server"></a>Microsoft ODBC Driver 17 per SQL Server 

> [!IMPORTANT]
> Se è stato installato il v17 `msodbcsql` pacchetto brevemente disponibile, è necessario rimuoverlo prima di installare il `msodbcsql17` pacchetto. Evitare i conflitti. Il `msodbcsql17` pacchetto può essere installato in modalità affiancata con il `msodbcsql` v13 pacchetto.

### <a name="debian-8-and-9"></a>Debian 8 e 9
```
sudo su 
curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -

#Download appropriate package for the OS version
#Choose only ONE of the following, corresponding to your OS version

#Debian 8
curl https://packages.microsoft.com/config/debian/8/prod.list > /etc/apt/sources.list.d/mssql-release.list

#Debian 9
curl https://packages.microsoft.com/config/debian/9/prod.list > /etc/apt/sources.list.d/mssql-release.list

exit
sudo apt-get update
sudo ACCEPT_EULA=Y apt-get install msodbcsql17
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y apt-get install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo apt-get install unixodbc-dev
```

### <a name="redhat-enterprise-server-6-and-7"></a>Server Red Hat Enterprise 6 e 7
```
sudo su

#Download appropriate package for the OS version
#Choose only ONE of the following, corresponding to your OS version

#RedHat Enterprise Server 6
curl https://packages.microsoft.com/config/rhel/6/prod.repo > /etc/yum.repos.d/mssql-release.repo

#RedHat Enterprise Server 7
curl https://packages.microsoft.com/config/rhel/7/prod.repo > /etc/yum.repos.d/mssql-release.repo

exit
sudo yum remove unixODBC-utf16 unixODBC-utf16-devel #to avoid conflicts
sudo ACCEPT_EULA=Y yum install msodbcsql17
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y yum install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo yum install unixODBC-devel
```

### <a name="suse-linux-enterprise-server-11sp4-and-12"></a>SUSE Linux Enterprise Server 11SP4 e 12

```
sudo su

#Download appropriate package for the OS version
#Choose only ONE of the following, corresponding to your OS version

#SUSE Linux Enterprise Server 11 SP4
zypper ar https://packages.microsoft.com/config/sles/11/prod.repo

#SUSE Linux Enterprise Server 12
zypper ar https://packages.microsoft.com/config/sles/12/prod.repo

exit
sudo ACCEPT_EULA=Y zypper install msodbcsql17
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y zypper install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo zypper install unixODBC-devel
``` 

### <a name="ubuntu-1404-1604-1710-and-1804"></a>Ubuntu 14.04, 16.04, 17.10 e 18.04
```
sudo su 
curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -

#Download appropriate package for the OS version
#Choose only ONE of the following, corresponding to your OS version

#Ubuntu 14.04
curl https://packages.microsoft.com/config/ubuntu/14.04/prod.list > /etc/apt/sources.list.d/mssql-release.list

#Ubuntu 16.04
curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list > /etc/apt/sources.list.d/mssql-release.list

#Ubuntu 17.10
curl https://packages.microsoft.com/config/ubuntu/17.10/prod.list > /etc/apt/sources.list.d/mssql-release.list

#Ubuntu 18.04
curl https://packages.microsoft.com/config/ubuntu/18.04/prod.list > /etc/apt/sources.list.d/mssql-release.list

exit
sudo apt-get update
sudo ACCEPT_EULA=Y apt-get install msodbcsql17
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y apt-get install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo apt-get install unixodbc-dev
```
> [!NOTE]
> - È necessaria per il supporto di Ubuntu 18.04 driver versione 17.2 o successiva.
> - Il pacchetto di sviluppo unixodbc 2.3.1 non è disponibile in Ubuntu 14.04.   

### <a name="os-x-1011-el-capitan-macos-1012-sierra-and-macos-1013-high-sierra"></a>OS X 10.11 (El Capitan) macOS 10.12 (Sierra) e macOS 10.13 (High Sierra)

```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
brew tap microsoft/mssql-release https://github.com/Microsoft/homebrew-mssql-release
brew update
brew install --no-sandbox msodbcsql17 mssql-tools
```

## <a name="microsoft-odbc-driver-131-for-sql-server"></a>Microsoft ODBC Driver 13.1 per SQL Server 

### <a name="debian-8"></a>Debian 8
```
sudo su 
curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
curl https://packages.microsoft.com/config/debian/8/prod.list > /etc/apt/sources.list.d/mssql-release.list
exit
sudo apt-get update
sudo ACCEPT_EULA=Y apt-get install msodbcsql
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y apt-get install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo apt-get install unixodbc-dev
```

### <a name="redhat-enterprise-server-6"></a>Server Red Hat Enterprise 6
```
sudo su
curl https://packages.microsoft.com/config/rhel/6/prod.repo > /etc/yum.repos.d/mssql-release.repo
exit
sudo yum remove unixODBC-utf16 unixODBC-utf16-devel #to avoid conflicts
sudo ACCEPT_EULA=Y yum install msodbcsql
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y yum install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo yum install unixODBC-devel
```

### <a name="redhat-enterprise-server-7"></a>Red Hat Enterprise Server 7
```
sudo su
curl https://packages.microsoft.com/config/rhel/7/prod.repo > /etc/yum.repos.d/mssql-release.repo
exit
sudo yum remove unixODBC-utf16 unixODBC-utf16-devel #to avoid conflicts
sudo ACCEPT_EULA=Y yum install msodbcsql
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y yum install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo yum install unixODBC-devel
```

### <a name="suse-linux-enterprise-server-11"></a>SUSE Linux Enterprise Server 11

```
sudo su
zypper ar https://packages.microsoft.com/config/sles/11/prod.repo
exit
sudo ACCEPT_EULA=Y zypper install msodbcsql
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y zypper install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo zypper install unixODBC-devel
``` 

### <a name="suse-linux-enterprise-server-12"></a>SUSE Linux Enterprise Server 12

```
sudo su
zypper ar https://packages.microsoft.com/config/sles/12/prod.repo
exit
sudo ACCEPT_EULA=Y zypper install msodbcsql
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y zypper install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo zypper install unixODBC-devel
``` 

### <a name="ubuntu-1510"></a>Ubuntu 15.10
```
sudo su 
curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
curl https://packages.microsoft.com/config/ubuntu/15.10/prod.list > /etc/apt/sources.list.d/mssql-release.list
exit
sudo apt-get update
sudo ACCEPT_EULA=Y apt-get install msodbcsql
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y apt-get install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo apt-get install unixodbc-dev
```

### <a name="ubuntu-1604"></a>Ubuntu 16.04
```
sudo su 
curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list > /etc/apt/sources.list.d/mssql-release.list
exit
sudo apt-get update
sudo ACCEPT_EULA=Y apt-get install msodbcsql
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y apt-get install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo apt-get install unixodbc-dev
```

### <a name="ubuntu-1610"></a>Ubuntu 16.10
```
sudo su 
curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
curl https://packages.microsoft.com/config/ubuntu/16.10/prod.list > /etc/apt/sources.list.d/mssql-release.list
exit
sudo apt-get update
sudo ACCEPT_EULA=Y apt-get install msodbcsql
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y apt-get install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo apt-get install unixodbc-dev
```

### <a name="os-x-1011-el-capitan-and-macos-1012-sierra"></a>OS X 10.11 (El Capitan) e macOS 10.12 (Sierra)

```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
brew tap microsoft/mssql-release https://github.com/Microsoft/homebrew-mssql-release
brew update
brew install --no-sandbox msodbcsql@13.1.9.2 mssql-tools@14.0.6.0
```

## <a name="microsoft-odbc-driver-13-for-sql-server"></a>Microsoft ODBC Driver 13 for SQL Server

### <a name="redhat-enterprise-server-6"></a>Server Red Hat Enterprise 6
```
sudo su
curl https://packages.microsoft.com/config/rhel/6/prod.repo > /etc/yum.repos.d/mssql-release.repo
exit
sudo yum update
sudo yum remove unixODBC #to avoid conflicts
sudo ACCEPT_EULA=Y yum install msodbcsql-13.0.1.0-1 mssql-tools-14.0.2.0-1
sudo yum install unixODBC-utf16-devel #this step is optional but recommended*
#Create symlinks for tools
ln -sfn /opt/mssql-tools/bin/sqlcmd-13.0.1.0 /usr/bin/sqlcmd 
ln -sfn /opt/mssql-tools/bin/bcp-13.0.1.0 /usr/bin/bcp
```

### <a name="redhat-enterprise-server-7"></a>Red Hat Enterprise Server 7
```
sudo su
curl https://packages.microsoft.com/config/rhel/7/prod.repo > /etc/yum.repos.d/mssql-release.repo
exit
sudo yum update
sudo yum remove unixODBC #to avoid conflicts
sudo ACCEPT_EULA=Y yum install msodbcsql-13.0.1.0-1 mssql-tools-14.0.2.0-1
sudo yum install unixODBC-utf16-devel #this step is optional but recommended*
#Create symlinks for tools
ln -sfn /opt/mssql-tools/bin/sqlcmd-13.0.1.0 /usr/bin/sqlcmd 
ln -sfn /opt/mssql-tools/bin/bcp-13.0.1.0 /usr/bin/bcp
```

### <a name="ubuntu-1510"></a>Ubuntu 15.10
```
sudo su 
curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
curl https://packages.microsoft.com/config/ubuntu/15.10/prod.list > /etc/apt/sources.list.d/mssql-release.list
exit
sudo apt-get update
sudo ACCEPT_EULA=Y apt-get install msodbcsql=13.0.1.0-1 mssql-tools=14.0.2.0-1
sudo apt-get install unixodbc-dev-utf16 #this step is optional but recommended*
#Create symlinks for tools
ln -sfn /opt/mssql-tools/bin/sqlcmd-13.0.1.0 /usr/bin/sqlcmd 
ln -sfn /opt/mssql-tools/bin/bcp-13.0.1.0 /usr/bin/bcp
```

### <a name="ubuntu-1604"></a>Ubuntu 16.04
```
sudo su 
curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list > /etc/apt/sources.list.d/mssql-release.list
exit
sudo apt-get update
sudo ACCEPT_EULA=Y apt-get install msodbcsql=13.0.1.0-1 mssql-tools=14.0.2.0-1
sudo apt-get install unixodbc-dev-utf16 #this step is optional but recommended*
#Create symlinks for tools
ln -sfn /opt/mssql-tools/bin/sqlcmd-13.0.1.0 /usr/bin/sqlcmd 
ln -sfn /opt/mssql-tools/bin/bcp-13.0.1.0 /usr/bin/bcp
```

### <a name="suse-linux-enterprise-server-12"></a>SUSE Linux Enterprise Server 12

```
sudo su 
zypper ar https://packages.microsoft.com/config/sles/12/prod.repo 
zypper update 
sudo ACCEPT_EULA=Y zypper install msodbcsql-13.0.1.0-1 mssql-tools-14.0.2.0-1
zypper install unixODBC-utf16-devel
#Create symlinks for tools
ln -sfn /opt/mssql-tools/bin/sqlcmd-13.0.1.0 /usr/bin/sqlcmd 
ln -sfn /opt/mssql-tools/bin/bcp-13.0.1.0 /usr/bin/bcp
```

### <a name="offline-installation"></a>Installazione offline
Se si preferisce/richiedono il [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 13 per essere installato in un computer senza connessione internet, sarà necessario risolvere manualmente le dipendenze di pacchetto. Il [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 13 presenta le seguenti dipendenze dirette:
- Ubuntu: libc6 (> = 2.21), libstdc + + 6 (> = 4.9), libkrb5-3, libcurl3, openssl, debconf (> = 0,5), unixodbc (> = 2.3.1-1)
- Red Hat: ```glibc, e2fsprogs, krb5-libs, openssl, unixODBC```
- SuSE: ```glibc, libuuid1, krb5, openssl, unixODBC```

Ognuno di questi pacchetti, a sua volta ha le proprie dipendenze, che può o potrebbero non essere presente nel sistema. Per una soluzione generale per questo problema, vedere la documentazione della distribuzione del pacchetto manager: [RedHat](https://wiki.centos.org/HowTos/CreateLocalRepos), [Ubuntu](https://unix.stackexchange.com/questions/87130/how-to-quickly-create-a-local-apt-repository-for-random-packages-using-a-debian), e [SUSE](https://en.opensuse.org/Portal:Zypper)

È anche comune per scaricare manualmente tutti i pacchetti dipendenti e inserirli tra loro nel computer di installazione, quindi installare manualmente a sua volta, ogni pacchetto di completamento con il [!INCLUDE[msCoName](../../../includes/msconame_md.md)] pacchetto ODBC Driver 13.

#### <a name="redhat-linux-enterprise-server-7"></a>Redhat Linux Enterprise Server 7
  - Scaricare la versione più recente `msodbcsql` `.rpm` da qui: https://packages.microsoft.com/rhel/7/prod/
  - Installare le dipendenze e il driver
  
```
yum install glibc e2fsprogs krb5-libs openssl unixODBC unixODBC-devel #install dependencies
sudo rpm -i  msodbcsql-13.1.X.X-X.x86_64.rpm #install the Driver
```

#### <a name="ubuntu-1604"></a>Ubuntu 16.04
- Scaricare la versione più recente `msodbcsql` `.deb` da qui: https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/msodbcsql/ 
- Installare le dipendenze e il driver 

```
sudo apt-get install libc6 libstdc++6 libkrb5-3 libcurl3 openssl debconf unixodbc unixodbc-dev #install dependencies
sudo dpkg -i msodbcsql_13.1.X.X-X_amd64.deb #install the Driver
```

#### <a name="suse-linux-enterprise-server-12"></a>SUSE Linux Enterprise Server 12
- Scaricare la versione più recente `msodbcsql` `.rpm` da qui: https://packages.microsoft.com/sles/12/prod/
- Installare le dipendenze e il driver

```
zypper install glibc, libuuid1, krb5, openssl, unixODBC unixODBC-devel #install dependencies
sudo rpm -i  msodbcsql-13.1.X.X-X.x86_64.rpm #install the Driver
```

Dopo aver completato l'installazione del pacchetto, è possibile verificare che il [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 13 possibile trovare tutte le relative dipendenze in esecuzione /ldd ed esaminare l'output per le librerie mancante:
```
ldd /opt/microsoft/msodbcsql/lib64/libmsodbcsql-*
```
  
## <a name="microsoft-odbc-driver-11-for-sql-server-on-linux"></a>Microsoft ODBC Driver 11 for SQL Server in Linux

Prima di poter usare il driver, installare Gestione driver unixODBC. Per altre informazioni, vedere [Installazione di Gestione driver](../../../connect/odbc/linux-mac/installing-the-driver-manager.md).

**Passaggi dell'installazione**  

> [!IMPORTANT]  
> Queste istruzioni fanno riferimento a `msodbcsql-11.0.2270.0.tar.gz`, il file di installazione per Red Hat Linux. Se si sta installando l'anteprima per SUSE Linux, il nome del file è `msodbcsql-11.0.2260.0.tar.gz`.  
  
Per installare il driver:

1.  Assicurarsi di disporre dell'autorizzazione di radice.  

2.  Passare alla directory in cui il download ha inserito il file `msodbcsql-11.0.2270.0.tar.gz`. Verificare di avere il file \*.tar.gz corrispondente alla versione di Linux in uso. Per estrarre i file, eseguire il comando seguente, `tar xvzf msodbcsql-11.0.2270.0.tar.gz`.  
  
3.  Passare alla directory `msodbcsql-11.0.2270.0` contenente un file denominato **install.sh**.  
  
4.  Per visualizzare un elenco delle opzioni di installazione disponibili, eseguire il comando seguente: **./install.sh**  
  
5.  Eseguire il backup di **odbcinst.ini**. L'installazione del driver aggiorna **odbcinst.ini**. odbcinst.ini contiene l'elenco dei driver registrati in Gestione driver unixODBC. Per individuare il percorso di odbcinst.ini nel computer in uso, eseguire il comando seguente: ```odbc_config --odbcinstini```.  
  
6.  Prima di installare il driver, eseguire il comando seguente: `./install.sh verify`. L'output di `./install.sh verify` segnala se il computer dispone del software necessario per supportare il driver ODBC in Linux.  
  
7.  Quando si è pronti a installare il driver ODBC in Linux, eseguire il comando seguente: `./install.sh install`. Se è necessario specificare un comando di installazione (`bin-dir` o `lib-dir`), specificare il comando dopo l'opzione **installa**.  
  
8.  Dopo aver esaminato il contratto di licenza, digitare **YES** per continuare l'installazione.  
  
Programma di installazione inserisce il driver in `/opt/microsoft/msodbcsql/11.0.2270.0`. Il driver e i relativi file di supporto devono trovarsi nella `/opt/microsoft/msodbcsql/11.0.2270.0`.  
  
Per verificare che il driver ODBC Microsoft sia stato registrato in Linux, eseguire il comando seguente: ```odbcinst -q -d -n "ODBC Driver 11 for SQL Server"```.  
  
Nella pagina sull'[uso di esempi relativi a ODBC in MSDN C++ per il driver ODBC Driver in Linux](https://blogs.msdn.com/b/sqlblog/archive/2012/01/26/use-existing-msdn-c-odbc-samples-for-microsoft-linux-odbc-driver.aspx) è illustrato un esempio di codice che consente la connessione a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tramite il driver ODBC in Linux.  
  
**Disinstallazione**  
  
È possibile disinstallare il driver ODBC 11 in Linux eseguendo i comandi seguenti:  
  
1.  `rm -f /usr/bin/sqlcmd`
  
2.  `rm -f /usr/bin/bcp`  
  
3.  `rm -rf /opt/microsoft/msodbcsql`  
  
4.  `odbcinst -u -d -n "ODBC Driver 11 for SQL Server"`
  
## <a name="troubleshooting-connection-problems"></a>Risoluzione dei problemi relativi alla connessione  
Se non si riesce a stabilire una connessione a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tramite il driver ODBC, usare le informazioni seguenti per individuare il problema.  
  
Il problema di connessione più comune è legato alla presenza di due copie di Gestione driver UnixODBC installate. Cercare /usr for libodbc\*.so\*. Se è presente più di una versione del file, è possibile che esistano più installazioni di Gestione driver. L'applicazione potrebbe utilizzare la versione non corretta.
  
Abilitare il log della connessione modificando il `/etc/odbcinst.ini` file contenga la seguente sezione con questi elementi:

```
[ODBC]
Trace = Yes
TraceFile = (path to log file, or /dev/stdout to output directly to the terminal)
```  
  
Se viene generato un altro errore di connessione e il file di registro non è visualizzato, è possibile che nel computer in uso esistano due copie di Gestione driver. In caso contrario, l'output del log avrà un aspetto analogo a quanto segue:  
  
```  
[ODBC][28783][1321576347.077780][SQLDriverConnectW.c][290]  
        Entry:  
            Connection = 0x17c858e0  
            Window Hdl = (nil)  
            Str In = [DRIVER={ODBC Driver 13 for SQL Server};SERVER={contoso.com};Trusted_Connection={YES};WSID={mydb.contoso.com};AP...][length = 139 (SQL_NTS)]  
            Str Out = (nil)  
            Str Out Max = 0  
            Str Out Ptr = (nil)  
            Completion = 0  
        UNICODE Using encoding ASCII 'UTF8' and UNICODE 'UTF16LE'  
```  
  
Se la codifica dei caratteri ASCII è diversa da UTF-8, ad esempio: 
  
```  
UNICODE Using encoding ASCII 'ISO8859-1' and UNICODE 'UCS-2LE'  
```  
  
È presente più di una gestione Driver installato e l'applicazione usa errato uno, o gestione Driver non viene creato correttamente.  
  
Per altre informazioni sulla risoluzione dei problemi di connessione, vedere:  
  
-   [Passaggi per risolvere i problemi di connettività di SQL](https://blogs.msdn.com/b/sql_protocols/archive/2008/04/30/steps-to-troubleshoot-connectivity-issues.aspx)  
  
-   [Risoluzione dei problemi di connettività di SQL Server 2005 - Parte I](https://blogs.msdn.com/b/sql_protocols/archive/2005/10/22/sql-server-2005-connectivity-issue-troubleshoot-part-i.aspx)  
  
-   [Risoluzione dei problemi di connettività in SQL Server 2008 con il buffer circolare della connettività](https://blogs.msdn.com/b/sql_protocols/archive/2008/05/20/connectivity-troubleshooting-in-sql-server-2008-with-the-connectivity-ring-buffer.aspx)  
  
-   [Strumento di risoluzione dei problemi di autenticazione di SQL Server](https://blogs.msdn.com/b/sqlsecurity/archive/2010/03/29/sql-server-authentication-troubleshooter.aspx)  
  
-   [Dettagli errori (https://www.microsoft.com/products/ee/transform.aspx?ProdName=Microsoft+SQL+Server&EvtSrc=MSSQLServer&EvtID=11001)](https://www.microsoft.com/products/ee/transform.aspx?ProdName=Microsoft+SQL+Server&EvtSrc=MSSQLServer&EvtID=001)  
  
    Il numero di errore specificato nell'URL (11001) deve essere modificato in modo che corrisponda all'errore visualizzato.  
  
## <a name="driver-files"></a>File driver
Il Driver ODBC in Linux e MacOS include i componenti seguenti:

### <a name="linux"></a>Linux

|Componente|Descrizione|  
|---------------|-----------------|  
|libmsodbcsql-17. X.so.X.X o libmsodbcsql-13. X.so.X.X|File della libreria di collegamento dinamico dell'oggetto condiviso (`so`) che contiene tutte le funzionalità del driver. Questo file viene installato `/opt/microsoft/msodbcsql17/lib64/` per il Driver 17 e in `/opt/microsoft/msodbcsql/lib64/` per 13 del Driver.|  
|`msodbcsqlr17.rll` o `msodbcsqlr13.rll`|File di risorse associato per la libreria del driver. Questo file viene installato in `[driver .so directory]../share/resources/en_US/`| 
|msodbcsql.h|File di intestazione che contiene tutte le nuove definizioni necessarie per usare il driver.<br /><br /> **Nota:**  Non è possibile fare riferimento a msodbcsql.h e a odbcss.h nello stesso programma.<br /><br /> msodbcsql. h viene installato nella `/opt/microsoft/msodbcsql17/include/` per i Driver 17 e nel `/opt/microsoft/msodbcsql/include/` per 13 del Driver. |
|File License. txt|File di testo che contiene i termini del contratto di licenza dell'utente finale. Questo file si trova nella `/usr/share/doc/msodbcsql17/` per i Driver 17 e nel `/usr/share/doc/msodbcsql/` per 13 del Driver.|
|RELEASE_NOTES|File di testo che contiene le note sulla versione. Questo file si trova nella `/usr/share/doc/msodbcsql17/` per i Driver 17 e nel `/usr/share/doc/msodbcsql/` per 13 del Driver.|


### <a name="macos"></a>MacOS

|Componente|Descrizione|  
|---------------|-----------------|  
|libmsodbcsql.17.dylib o libmsodbcsql.13.dylib|File della libreria di collegamento dinamico (`dylib`) che contiene tutte le funzionalità del driver. Questo file viene installato `/usr/local/lib/`.|  
|`msodbcsqlr17.rll` o `msodbcsqlr13.rll`|File di risorse associato per la libreria del driver. Questo file viene installato `[driver .dylib directory]../share/msodbcsql17/resources/en_US/` per i Driver 17 e nel `[driver .dylib directory]../share/msodbcsql/resources/en_US/` per 13 del Driver. | 
|msodbcsql.h|File di intestazione che contiene tutte le nuove definizioni necessarie per usare il driver.<br /><br /> **Nota:**  Non è possibile fare riferimento a msodbcsql.h e a odbcss.h nello stesso programma.<br /><br /> msodbcsql. h viene installato nella `/usr/local/include/msodbcsql17/` per i Driver 17 e nel `/usr/local/include/msodbcsql/` per 13 del Driver. |
|File License. txt|File di testo che contiene i termini del contratto di licenza dell'utente finale. Questo file si trova nella `/usr/local/share/doc/msodbcsql17/` per i Driver 17 e nel `/usr/local/share/doc/msodbcsql/` per 13 del Driver. |
|RELEASE_NOTES|File di testo che contiene le note sulla versione. Questo file si trova nella `/usr/local/share/doc/msodbcsql17/` per i Driver 17 e nel `/usr/local/share/doc/msodbcsql/` per 13 del Driver. |

## <a name="resource-file-loading"></a>Caricamento di File di risorse

Il driver deve caricare il file di risorse per il funzionamento. Questo file è denominato `msodbcsqlr17.rll` o `msodbcsqlr13.rll` a seconda della versione del driver. Il percorso dei `.rll` file è relativo alla posizione del driver stesso (`so` o `dylib`), come indicato nella tabella precedente. A partire dalla versione 17.1 il driver tenterà anche di caricare il `.rll` dal valore predefinito non riesce se il caricamento dal percorso relativo nella directory. I percorsi dei file di risorse predefiniti sono:

Linux: `/opt/microsoft/msodbcsql17/share/resources/en_US/`

MacOS: `/usr/local/share/msodbcsql17/resources/en_US/`


  
## <a name="see-also"></a>Vedere anche

[Installazione di Gestione driver](../../../connect/odbc/linux-mac/installing-the-driver-manager.md)

[Note sulla versione](../../../connect/odbc/linux-mac/release-notes.md)

[System Requirements](../../../connect/odbc/linux-mac/system-requirements.md)
