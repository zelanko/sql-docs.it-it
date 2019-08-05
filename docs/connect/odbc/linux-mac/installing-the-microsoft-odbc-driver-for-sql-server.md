---
title: Installazione di Microsoft ODBC Driver for SQL Server in Linux e macOS | Microsoft Docs
ms.custom: ''
ms.date: 12/05/2018
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
ms.openlocfilehash: a1cffb5050a548acfd1bbd9ec9d38a8c9b48d63f
ms.sourcegitcommit: e821cd8e5daf95721caa1e64c2815a4523227aa4
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 08/01/2019
ms.locfileid: "68702733"
---
# <a name="installing-the-microsoft-odbc-driver-for-sql-server-on-linux-and-macos"></a>Installazione di Microsoft ODBC Driver for SQL Server in Linux e macOS
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

Questo articolo spiega come installare [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in Linux e macOS, gli strumenti da riga di comando facoltativi per SQL Server (`bcp` e `sqlcmd`) e le intestazioni di sviluppo unixODBC.

## <a name="microsoft-odbc-driver-17-for-sql-server"></a>Microsoft ODBC Driver 17 per SQL Server 

> [!IMPORTANT]
> Se è stato installato il pacchetto `msodbcsql` v17 rimasto disponibile per poco tempo, rimuoverlo prima di installare il pacchetto `msodbcsql17`. Si eviteranno così conflitti. È possibile installare il pacchetto `msodbcsql17` side-by-side con il pacchetto `msodbcsql` v13.

### <a name="debian"></a>Debian
```
sudo su 
curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -

#Download appropriate package for the OS version
#Choose only ONE of the following, corresponding to your OS version

#Debian 8
curl https://packages.microsoft.com/config/debian/8/prod.list > /etc/apt/sources.list.d/mssql-release.list

#Debian 9
curl https://packages.microsoft.com/config/debian/9/prod.list > /etc/apt/sources.list.d/mssql-release.list

#Debian 10
curl https://packages.microsoft.com/config/debian/10/prod.list > /etc/apt/sources.list.d/mssql-release.list

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

### <a name="redhat-enterprise-server"></a>RedHat Enterprise Server
```
sudo su

#Download appropriate package for the OS version
#Choose only ONE of the following, corresponding to your OS version

#RedHat Enterprise Server 6
curl https://packages.microsoft.com/config/rhel/6/prod.repo > /etc/yum.repos.d/mssql-release.repo

#RedHat Enterprise Server 7
curl https://packages.microsoft.com/config/rhel/7/prod.repo > /etc/yum.repos.d/mssql-release.repo

#RedHat Enterprise Server 8
curl https://packages.microsoft.com/config/rhel/8/prod.repo > /etc/yum.repos.d/mssql-release.repo

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

### <a name="suse-linux-enterprise-server"></a>SuSE Linux Enterprise Server

```
sudo su

#Download appropriate package for the OS version
#Choose only ONE of the following, corresponding to your OS version

#SUSE Linux Enterprise Server 11 SP4
zypper ar https://packages.microsoft.com/config/sles/11/prod.repo

#SUSE Linux Enterprise Server 12
zypper ar https://packages.microsoft.com/config/sles/12/prod.repo

#SUSE Linux Enterprise Server 15
zypper ar https://packages.microsoft.com/config/sles/15/prod.repo
SUSEConnect -p sle-module-legacy/15/x86_64

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

### <a name="ubuntu"></a>Ubuntu
```
sudo su 
curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -

#Download appropriate package for the OS version
#Choose only ONE of the following, corresponding to your OS version

#Ubuntu 14.04
curl https://packages.microsoft.com/config/ubuntu/14.04/prod.list > /etc/apt/sources.list.d/mssql-release.list

#Ubuntu 16.04
curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list > /etc/apt/sources.list.d/mssql-release.list

#Ubuntu 18.04
curl https://packages.microsoft.com/config/ubuntu/18.04/prod.list > /etc/apt/sources.list.d/mssql-release.list

#Ubuntu 18.10
curl https://packages.microsoft.com/config/ubuntu/18.10/prod.list > /etc/apt/sources.list.d/mssql-release.list

#Ubuntu 19.04
curl https://packages.microsoft.com/config/ubuntu/19.04/prod.list > /etc/apt/sources.list.d/mssql-release.list

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
> - È necessaria la versione del driver 17.2 o versione successiva per il supporto di Ubuntu 18.04.
> - È necessaria la versione del driver 17.3 o versione successiva per il supporto di Ubuntu 18.10.   

### <a name="macos"></a>MacOS

```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
brew tap microsoft/mssql-release https://github.com/Microsoft/homebrew-mssql-release
brew update
brew install msodbcsql17 mssql-tools
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

### <a name="redhat-enterprise-server-6"></a>RedHat Enterprise Server 6
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

### <a name="redhat-enterprise-server-7"></a>RedHat Enterprise Server 7
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
brew install msodbcsql@13.1.9.2 mssql-tools@14.0.6.0
```

## <a name="microsoft-odbc-driver-13-for-sql-server"></a>Microsoft ODBC Driver 13 for SQL Server

### <a name="redhat-enterprise-server-6"></a>RedHat Enterprise Server 6
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

### <a name="redhat-enterprise-server-7"></a>RedHat Enterprise Server 7
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
Se si preferisce o si deve installare [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 13 in un computer senza connessione Internet, sarà necessario risolvere manualmente le dipendenze del pacchetto. [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 13 presenta le dipendenze dirette seguenti:
- Ubuntu: libc6 (>= 2.21), libstdc++6 (>= 4.9), libkrb5-3, libcurl3, openssl, debconf (>= 0.5), unixodbc (>= 2.3.1-1)
- Red Hat: ```glibc, e2fsprogs, krb5-libs, openssl, unixODBC```
- SuSE: ```glibc, libuuid1, krb5, openssl, unixODBC```

Ognuno di questi pacchetti ha a sua volta le proprie dipendenze, che potrebbero o meno essere presenti nel sistema. Per una soluzione generale di questo problema, fare riferimento alla documentazione della gestione pacchetti per la distribuzione: [Redhat](https://wiki.centos.org/HowTos/CreateLocalRepos), [Ubuntu](https://unix.stackexchange.com/questions/87130/how-to-quickly-create-a-local-apt-repository-for-random-packages-using-a-debian) e [SUSE](https://en.opensuse.org/Portal:Zypper)

È anche una pratica comune scaricare manualmente tutti i pacchetti dipendenti, inserirli nel computer di installazione, quindi installare manualmente ogni pacchetto e terminare con il pacchetto [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 13.

#### <a name="redhat-linux-enterprise-server-7"></a>Redhat Linux Enterprise Server 7
  - Scaricare la versione più recente di `msodbcsql` `.rpm` da qui: https://packages.microsoft.com/rhel/7/prod/
  - Installare le dipendenze e il driver
  
```
yum install glibc e2fsprogs krb5-libs openssl unixODBC unixODBC-devel #install dependencies
sudo rpm -i  msodbcsql-13.1.X.X-X.x86_64.rpm #install the Driver
```

#### <a name="ubuntu-1604"></a>Ubuntu 16.04
- Scaricare la versione più recente di `msodbcsql` `.deb` da qui: https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/msodbcsql/ 
- Installare le dipendenze e il driver 

```
sudo apt-get install libc6 libstdc++6 libkrb5-3 libcurl3 openssl debconf unixodbc unixodbc-dev #install dependencies
sudo dpkg -i msodbcsql_13.1.X.X-X_amd64.deb #install the Driver
```

#### <a name="suse-linux-enterprise-server-12"></a>SUSE Linux Enterprise Server 12
- Scaricare la versione più recente di `msodbcsql` `.rpm` da qui: https://packages.microsoft.com/sles/12/prod/
- Installare le dipendenze e il driver

```
zypper install glibc, libuuid1, krb5, openssl, unixODBC unixODBC-devel #install dependencies
sudo rpm -i  msodbcsql-13.1.X.X-X.x86_64.rpm #install the Driver
```

Dopo aver completato l'installazione del pacchetto, è possibile verificare che [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 13 trovi tutte le relative dipendenze. Eseguire ldd e verificare l'output per individuare le librerie mancanti:
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
  
L'installazione inserisce il driver in `/opt/microsoft/msodbcsql/11.0.2270.0`. Il driver e i relativi file di supporto devono trovarsi in `/opt/microsoft/msodbcsql/11.0.2270.0`.  
  
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
  
Abilitare il log della connessione modificando il file `/etc/odbcinst.ini` affinché contenga la sezione seguente con questi elementi:

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
  
Sono installate più copie di Gestione driver e l'applicazione usa quella sbagliata oppure Gestione driver non è stato compilato correttamente.  
  
Per altre informazioni sulla risoluzione dei problemi di connessione, vedere:  
  
-   [Passaggi per risolvere i problemi di connettività di SQL](https://blogs.msdn.com/b/sql_protocols/archive/2008/04/30/steps-to-troubleshoot-connectivity-issues.aspx)  
  
-   [Risoluzione dei problemi di connettività di SQL Server 2005 - Parte I](https://blogs.msdn.com/b/sql_protocols/archive/2005/10/22/sql-server-2005-connectivity-issue-troubleshoot-part-i.aspx)  
  
-   [Risoluzione dei problemi di connettività in SQL Server 2008 con il buffer circolare della connettività](https://blogs.msdn.com/b/sql_protocols/archive/2008/05/20/connectivity-troubleshooting-in-sql-server-2008-with-the-connectivity-ring-buffer.aspx)  
  
-   [Strumento di risoluzione dei problemi di autenticazione di SQL Server](https://blogs.msdn.com/b/sqlsecurity/archive/2010/03/29/sql-server-authentication-troubleshooter.aspx)  
  
-   [Dettagli errori (https://www.microsoft.com/products/ee/transform.aspx?ProdName=Microsoft+SQL+Server&EvtSrc=MSSQLServer&EvtID=11001)](https://www.microsoft.com/products/ee/transform.aspx?ProdName=Microsoft+SQL+Server&EvtSrc=MSSQLServer&EvtID=001)  
  
    Il numero di errore specificato nell'URL (11001) deve essere modificato in modo che corrisponda all'errore visualizzato.  
  
## <a name="driver-files"></a>File driver
Il driver ODBC in Linux e MacOS include i componenti seguenti:

### <a name="linux"></a>Linux

|Componente|Descrizione|  
|---------------|-----------------|  
|libmsodbcsql-17.X.so.X.X o libmsodbcsql-13.X.so.X.X|File della libreria di collegamento dinamico dell'oggetto condiviso (`so`) che contiene tutte le funzionalità del driver. Questo file viene installato in `/opt/microsoft/msodbcsql17/lib64/` per Driver 17 e in `/opt/microsoft/msodbcsql/lib64/` per Driver 13.|  
|`msodbcsqlr17.rll` o `msodbcsqlr13.rll`|File di risorse associato per la libreria del driver. Questo file viene installato in `[driver .so directory]../share/resources/en_US/`| 
|msodbcsql.h|File di intestazione che contiene tutte le nuove definizioni necessarie per usare il driver.<br /><br /> **Nota:**  non è possibile fare riferimento a msodbcsql.h e odbcss.h nello stesso programma.<br /><br /> msodbcsql.h viene installato in `/opt/microsoft/msodbcsql17/include/` per Driver 17 e in `/opt/microsoft/msodbcsql/include/` per Driver 13. |
|LICENSE.txt|File di testo che contiene i termini del contratto di licenza con l'utente finale. Questo file viene inserito in `/usr/share/doc/msodbcsql17/` per Driver 17 e in `/usr/share/doc/msodbcsql/` per Driver 13.|
|RELEASE_NOTES|File di testo che contiene le note sulla versione. Questo file viene inserito in `/usr/share/doc/msodbcsql17/` per Driver 17 e in `/usr/share/doc/msodbcsql/` per Driver 13.|


### <a name="macos"></a>MacOS

|Componente|Descrizione|  
|---------------|-----------------|  
|libmsodbcsql.17.dylib o libmsodbcsql.13.dylib|File della libreria di collegamento dinamico (`dylib`) che contiene tutte le funzionalità del driver. Questo file viene installato in `/usr/local/lib/`.|  
|`msodbcsqlr17.rll` o `msodbcsqlr13.rll`|File di risorse associato per la libreria del driver. Questo file viene installato in `[driver .dylib directory]../share/msodbcsql17/resources/en_US/` per Driver 17 e in `[driver .dylib directory]../share/msodbcsql/resources/en_US/` per Driver 13. | 
|msodbcsql.h|File di intestazione che contiene tutte le nuove definizioni necessarie per usare il driver.<br /><br /> **Nota:**  non è possibile fare riferimento a msodbcsql.h e odbcss.h nello stesso programma.<br /><br /> msodbcsql.h viene installato in `/usr/local/include/msodbcsql17/` per Driver 17 e in `/usr/local/include/msodbcsql/` per Driver 13. |
|LICENSE.txt|File di testo che contiene i termini del contratto di licenza con l'utente finale. Questo file viene inserito in `/usr/local/share/doc/msodbcsql17/` per Driver 17 e in `/usr/local/share/doc/msodbcsql/` per Driver 13. |
|RELEASE_NOTES|File di testo che contiene le note sulla versione. Questo file viene inserito in `/usr/local/share/doc/msodbcsql17/` per Driver 17 e in `/usr/local/share/doc/msodbcsql/` per Driver 13. |

## <a name="resource-file-loading"></a>Caricamento del file di risorse

Perché possa funzionare, il driver deve caricare il file di risorse. Questo file è denominato `msodbcsqlr17.rll` o `msodbcsqlr13.rll` a seconda della versione del driver. La posizione del file `.rll` dipende dalla posizione del driver stesso (`so` o `dylib`), come indicato nella tabella precedente. A partire dalla versione 17.1 il driver tenterà anche di caricare il file `.rll` dalla directory predefinita se il caricamento dal percorso relativo non riesce. I percorsi predefiniti del file di risorse sono i seguenti:

Linux: `/opt/microsoft/msodbcsql17/share/resources/en_US/`

MacOS: `/usr/local/share/msodbcsql17/resources/en_US/`


  
## <a name="see-also"></a>Vedere anche

[Installazione di Gestione driver](../../../connect/odbc/linux-mac/installing-the-driver-manager.md)

[Note sulla versione](../../../connect/odbc/linux-mac/release-notes-odbc-sql-server-linux-mac.md)

[System Requirements](../../../connect/odbc/linux-mac/system-requirements.md)
