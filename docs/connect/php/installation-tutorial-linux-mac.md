---
title: Esercitazione sull'installazione in Linux e macOS dei driver Microsoft per PHP per SQL Server | Microsoft Docs
ms.date: 06/21/2019
ms.prod: sql
ms.prod_service: connectivity
ms.custom: ''
ms.technology: connectivity
ms.topic: conceptual
author: ulvii
ms.author: v-ulibra
manager: v-mabarw
ms.openlocfilehash: 90d2b5850010d49e881ea0169566fe8e7d046f0d
ms.sourcegitcommit: 630f7cacdc16368735ec1d955b76d6d030091097
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/24/2019
ms.locfileid: "67343905"
---
# <a name="linux-and-macos-installation-tutorial-for-the-microsoft-drivers-for-php-for-sql-server"></a>Esercitazione sull'installazione in Linux e macOS dei driver Microsoft per PHP per SQL Server
Le istruzioni seguenti presuppongono che venga usato un ambiente pulito e illustrano come installare PHP 7.x, il driver Microsoft ODBC, Apache e i driver Microsoft per PHP per SQL Server in Ubuntu 16.04, 18.04 e 18.10, Red Hat 7, Debian 8 e 9, Suse 12 e 15 e macOS 10.12, 10.13 e 10.14. I consigli contenuti in queste istruzioni riguardano l'installazione dei driver con PECL, ma è anche possibile scaricare i file binari precompilati dalla pagina del progetto GitHub relativo ai [driver Microsoft per PHP per SQL Server](https://github.com/Microsoft/msphpsql/releases) e installare tali file seguendo le istruzioni riportate in [Caricamento dei driver Microsoft per PHP per SQL Server](../../connect/php/loading-the-php-sql-driver.md). Per una spiegazione del caricamento delle estensioni e dei motivi per cui non si aggiungeranno le estensioni a php.ini, vedere la sezione relativa al [caricamento dei driver](../../connect/php/loading-the-php-sql-driver.md##loading-the-driver-at-php-startup).

Per impostazione predefinita, con queste istruzioni viene installato PHP 7.3. Si noti che alcune distribuzioni Linux supportate installano per impostazione predefinita PHP 7.0 o versioni precedenti, che non sono supportate per i driver PHP per SQL Server. Per installare invece PHP 7.1 o 7.2, vedere le note all'inizio di ogni sezione.

## <a name="contents-of-this-page"></a>Contenuto della pagina:

- [Installazione dei driver in Ubuntu 16.04, 18.04 e 18.10](#installing-the-drivers-on-ubuntu-1604-1804-and-1810)
- [Installazione dei driver in Red Hat 7](#installing-the-drivers-on-red-hat-7)
- [Installazione dei driver in Debian 8 e 9](#installing-the-drivers-on-debian-8-and-9)
- [Installazione dei driver in Suse 12 e 15](#installing-the-drivers-on-suse-12-and-15)
- [Installazione dei driver in macOS Sierra, High Sierra e Mojave](#installing-the-drivers-on-macos-sierra-high-sierra-and-mojave)

## <a name="installing-the-drivers-on-ubuntu-1604-1804-and-1810"></a>Installazione dei driver in Ubuntu 16.04, 18.04 e 18.10

> [!NOTE]
> Per installare PHP 7.1 o 7.2, sostituire 7.3 con 7.1 o 7.2 nei comandi seguenti.

### <a name="step-1-install-php"></a>Passaggio 1. Installare PHP
```
sudo su
add-apt-repository ppa:ondrej/php -y
apt-get update
apt-get install php7.3 php7.3-dev php7.3-xml -y --allow-unauthenticated
```
### <a name="step-2-install-prerequisites"></a>Passaggio 2. Prerequisiti di installazione
Installare il driver ODBC per Ubuntu seguendo le istruzioni riportate nella pagina relativa all'[installazione in Linux e macOS](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md).

### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>Passaggio 3. Installare i driver PHP per Microsoft SQL Server
```
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
sudo su
printf "; priority=20\nextension=sqlsrv.so\n" > /etc/php/7.3/mods-available/sqlsrv.ini
printf "; priority=30\nextension=pdo_sqlsrv.so\n" > /etc/php/7.3/mods-available/pdo_sqlsrv.ini
exit
sudo phpenmod -v 7.3 sqlsrv pdo_sqlsrv
```

Se è presente solo una versione PHP nel sistema, l'ultimo passaggio può essere semplificato nel `phpenmod sqlsrv pdo_sqlsrv`.

### <a name="step-4-install-apache-and-configure-driver-loading"></a>Passaggio 4. Installare Apache e configurare il caricamento dei driver
```
sudo su
apt-get install libapache2-mod-php7.3 apache2
a2dismod mpm_event
a2enmod mpm_prefork
a2enmod php7.3
exit
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>Passaggio 5. Riavviare Apache e testare lo script di esempio
```
sudo service apache2 restart
```
Per testare l'installazione, vedere [Test dell'installazione](#testing-your-installation) alla fine di questo documento.

## <a name="installing-the-drivers-on-red-hat-7"></a>Installazione dei driver in Red Hat 7

> [!NOTE]
> Per installare PHP 7.1 o 7.2, sostituire remi-php73 rispettivamente con remi-php71 o remi-php72 nei comandi seguenti.

### <a name="step-1-install-php"></a>Passaggio 1. Installare PHP

```
sudo su
wget https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
wget https://rpms.remirepo.net/enterprise/remi-release-7.rpm
rpm -Uvh remi-release-7.rpm epel-release-latest-7.noarch.rpm
subscription-manager repos --enable=rhel-7-server-optional-rpms
yum install yum-utils
yum-config-manager --enable remi-php73
yum update
yum install php php-pdo php-xml php-pear php-devel re2c gcc-c++ gcc
```
### <a name="step-2-install-prerequisites"></a>Passaggio 2. Prerequisiti di installazione
Installare il driver ODBC per Red Hat 7 seguendo le istruzioni riportate nella pagina relativa all'[installazione in Linux e macOS](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md).

### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>Passaggio 3. Installare i driver PHP per Microsoft SQL Server
```
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
sudo su
echo extension=pdo_sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/pdo_sqlsrv.ini
echo extension=sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/sqlsrv.ini
exit
```

In alternativa, è possibile scaricare i file binari precompilati dalla [pagina del progetto GitHub](https://github.com/Microsoft/msphpsql/releases) oppure eseguire l'installazione dal repository Remi:
```
sudo yum install php-sqlsrv
```
### <a name="step-4-install-apache"></a>Passaggio 4. Installare Apache
```
sudo yum install httpd
```
SELinux viene installato per impostazione predefinita ed eseguito in modalità Enforcing. Per consentire la connessione di Apache ai database tramite SELinux, eseguire questo comando:
```
sudo setsebool -P httpd_can_network_connect_db 1
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>Passaggio 5. Riavviare Apache e testare lo script di esempio
```
sudo apachectl restart
```
Per testare l'installazione, vedere [Test dell'installazione](#testing-your-installation) alla fine di questo documento.

## <a name="installing-the-drivers-on-debian-8-and-9"></a>Installazione dei driver in Debian 8 e 9

> [!NOTE]
> Per installare PHP 7.1 o 7.2, nei comandi seguenti sostituire 7.3 con 7.1 o 7.2.

### <a name="step-1-install-php"></a>Passaggio 1. Installare PHP
```
sudo su
apt-get install curl apt-transport-https
wget -O /etc/apt/trusted.gpg.d/php.gpg https://packages.sury.org/php/apt.gpg
echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" > /etc/apt/sources.list.d/php.list
apt-get update
apt-get install -y php7.3 php7.3-dev php7.3-xml
```
### <a name="step-2-install-prerequisites"></a>Passaggio 2. Prerequisiti di installazione
Installare il driver ODBC per Debian seguendo le istruzioni riportate nella pagina relativa all'[installazione in Linux e macOS](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md). 

Per ottenere la visualizzazione corretta dell'output PHP in un browser, potrebbe essere necessario anche generare le impostazioni locali corrette. Per le impostazioni locali en_US UTF-8, ad esempio, eseguire questi comandi:
```
sudo su
sed -i 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/g' /etc/locale.gen
locale-gen
```

### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>Passaggio 3. Installare i driver PHP per Microsoft SQL Server
```
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
sudo su
printf "; priority=20\nextension=sqlsrv.so\n" > /etc/php/7.3/mods-available/sqlsrv.ini
printf "; priority=30\nextension=pdo_sqlsrv.so\n" > /etc/php/7.3/mods-available/pdo_sqlsrv.ini
exit
sudo phpenmod -v 7.3 sqlsrv pdo_sqlsrv
```

Se è presente solo una versione PHP nel sistema, l'ultimo passaggio può essere semplificato nel `phpenmod sqlsrv pdo_sqlsrv`.

### <a name="step-4-install-apache-and-configure-driver-loading"></a>Passaggio 4. Installare Apache e configurare il caricamento dei driver
```
sudo su
apt-get install libapache2-mod-php7.3 apache2
a2dismod mpm_event
a2enmod mpm_prefork
a2enmod php7.3
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>Passaggio 5. Riavviare Apache e testare lo script di esempio
```
sudo service apache2 restart
```
Per testare l'installazione, vedere [Test dell'installazione](#testing-your-installation) alla fine di questo documento.

## <a name="installing-the-drivers-on-suse-12-and-15"></a>Installazione dei driver in Suse 12 e 15

> [!NOTE]
> Nelle istruzioni seguenti, sostituire <SuseVersion> con la propria versione di Suse: SLE_15 o SLE_15_SP1 se si usa Suse Enterprise Linux 15 e valori analoghi per le altre versioni. Non tutte le versioni di PHP sono disponibili per tutte le versioni di Suse Linux. Vedere `http://download.opensuse.org/repositories/devel:/languages:/php` per verificare in quali versioni di Suse è disponibile la versione predefinita di PHP o `http://download.opensuse.org/repositories/devel:/languages:/php:/` per verificare quali altre versioni di PHP sono disponibili per le singole versioni di Suse.

> [!NOTE]
> I pacchetti per PHP 7.3 non sono disponibili per Suse 12. Per installare PHP 7.1, sostituire l'URL del repository riportato di seguito con questo URL: `https://download.opensuse.org/repositories/devel:/languages:/php:/php71/<SuseVersion>/devel:languages:php:php71.repo`.
> Per installare PHP 7.2, sostituire l'URL del repository riportato di seguito con questo URL: `https://download.opensuse.org/repositories/devel:/languages:/php:/php72/<SuseVersion>/devel:languages:php:php72.repo`.

### <a name="step-1-install-php"></a>Passaggio 1. Installare PHP
```
sudo su
zypper -n ar -f https://download.opensuse.org/repositories/devel:languages:php/<SuseVersion>/devel:languages:php.repo
zypper --gpg-auto-import-keys refresh
zypper -n install php7 php7-pear php7-devel php7-openssl
```
### <a name="step-2-install-prerequisites"></a>Passaggio 2. Prerequisiti di installazione
Installare il driver ODBC per Suse seguendo le istruzioni riportate nella pagina relativa all'[installazione in Linux e macOS](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md).

### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>Passaggio 3. Installare i driver PHP per Microsoft SQL Server
> [!NOTE]
> Se viene visualizzato il messaggio di errore `Connection to 'pecl.php.net:443' failed: Unable to find the socket transport "ssl"`, modificare lo script PECL in /usr/bin/pecl e rimuovere l'opzione `-n` nell'ultima riga. Questa opzione impedisce a PECL di caricare file INI quando viene chiamato PHP, impedendo così il caricamento dell'estensione OpenSSL.

```
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
sudo su
echo extension=pdo_sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/pdo_sqlsrv.ini
echo extension=sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/sqlsrv.ini
exit
```
### <a name="step-4-install-apache-and-configure-driver-loading"></a>Passaggio 4. Installare Apache e configurare il caricamento dei driver
```
sudo su
zypper install apache2 apache2-mod_php7
a2enmod php7
echo "extension=sqlsrv.so" >> /etc/php7/apache2/php.ini
echo "extension=pdo_sqlsrv.so" >> /etc/php7/apache2/php.ini
exit
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>Passaggio 5. Riavviare Apache e testare lo script di esempio
```
sudo systemctl restart apache2
```
Per testare l'installazione, vedere [Test dell'installazione](#testing-your-installation) alla fine di questo documento.

## <a name="installing-the-drivers-on-macos-sierra-high-sierra-and-mojave"></a>Installazione dei driver in macOS Sierra, High Sierra e Mojave

Se non è già presente, installare brew come illustrato di seguito:
```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

> [!NOTE]
> Per installare PHP 7.1 o 7.2, sostituire php@7.3 rispettivamente con php@7.1 o php@7.2 nei comandi seguenti.

### <a name="step-1-install-php"></a>Passaggio 1. Installare PHP

```
brew tap
brew tap homebrew/core
brew install php@7.3
```
PHP dovrebbe ora trovarsi nel percorso previsto. Eseguire `php -v` per verificare che sia in esecuzione la versione corretta di PHP. Se PHP non si trova nel percorso previsto o la versione non è corretta, eseguire questo comando:
```
brew link --force --overwrite php@7.3
```

### <a name="step-2-install-prerequisites"></a>Passaggio 2. Prerequisiti di installazione
Installare il driver ODBC per macOS seguendo le istruzioni riportate nella pagina relativa all'[installazione in Linux e macOS](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md). 

Potrebbe essere necessario anche installare gli strumenti GNU make:
```
brew install autoconf automake libtool
```

### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>Passaggio 3. Installare i driver PHP per Microsoft SQL Server
```
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
```
### <a name="step-4-install-apache-and-configure-driver-loading"></a>Passaggio 4. Installare Apache e configurare il caricamento dei driver
```
brew install apache2
```
Per trovare il file di configurazione di Apache per l'installazione di Apache in uso, eseguire: 
```
apachectl -V | grep SERVER_CONFIG_FILE
``` 
Sostituire quindi il percorso di `httpd.conf` nei comandi seguenti:
```
echo "LoadModule php7_module /usr/local/opt/php@7.3/lib/httpd/modules/libphp7.so" >> /usr/local/etc/httpd/httpd.conf
(echo "<FilesMatch .php$>"; echo "SetHandler application/x-httpd-php"; echo "</FilesMatch>";) >> /usr/local/etc/httpd/httpd.conf
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>Passaggio 5. Riavviare Apache e testare lo script di esempio
```
sudo apachectl restart
```
Per testare l'installazione, vedere [Test dell'installazione](#testing-your-installation) alla fine di questo documento.

## <a name="testing-your-installation"></a>Test dell'installazione

Per testare questo script di esempio, creare un file denominato testsql.php nella radice dei documenti del sistema, che è `/var/www/html/` in Ubuntu, Debian e Red Hat, `/srv/www/htdocs` in SUSE e `/usr/local/var/www` in macOS. Copiarvi lo script seguente, sostituendo il server, il database, il nome utente e la password nel modo appropriato.
```
<?php
$serverName = "yourServername";
$connectionOptions = array(
    "database" => "yourDatabase",
    "uid" => "yourUsername",
    "pwd" => "yourPassword"
);

// Establishes the connection
$conn = sqlsrv_connect($serverName, $connectionOptions);
if ($conn === false) {
    die(formatErrors(sqlsrv_errors()));
}

// Select Query
$tsql = "SELECT @@Version AS SQL_VERSION";

// Executes the query
$stmt = sqlsrv_query($conn, $tsql);

// Error handling
if ($stmt === false) {
    die(formatErrors(sqlsrv_errors()));
}
?>

<h1> Results : </h1>

<?php
while ($row = sqlsrv_fetch_array($stmt, SQLSRV_FETCH_ASSOC)) {
    echo $row['SQL_VERSION'] . PHP_EOL;
}

sqlsrv_free_stmt($stmt);
sqlsrv_close($conn);

function formatErrors($errors)
{
    // Display errors
    echo "Error information: <br/>";
    foreach ($errors as $error) {
        echo "SQLSTATE: ". $error['SQLSTATE'] . "<br/>";
        echo "Code: ". $error['code'] . "<br/>";
        echo "Message: ". $error['message'] . "<br/>";
    }
}
?>
```
Passare nel browser a https://localhost/testsql.php (https://localhost:8080/testsql.php in macOS). Dovrebbe ora essere possibile connettersi al database SQL di Azure/SQL Server.

## <a name="see-also"></a>Vedere anche  
[Introduzione ai driver Microsoft per PHP per SQL Server](../../connect/php/getting-started-with-the-php-sql-driver.md)

[Caricamento dei Driver Microsoft per PHP per SQL Server](../../connect/php/loading-the-php-sql-driver.md)

[Requisiti di sistema dei driver Microsoft per PHP per SQL Server](../../connect/php/system-requirements-for-the-php-sql-driver.md)
