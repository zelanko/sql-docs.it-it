---
title: Caricamento dei driver Microsoft per PHP per SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 02/11/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- loading the driver
ms.assetid: e5c114c5-8204-49c2-94eb-62ca63f5d3ec
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 4b2f02fc81b969f8633a5a951483745c1d2635b0
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66799642"
---
# <a name="loading-the-microsoft-drivers-for-php-for-sql-server"></a>Caricamento dei Driver Microsoft per PHP per SQL Server
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

In questa pagina vengono specificate le istruzioni per il caricamento dei [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] nello spazio di elaborazione PHP.  
  
È possibile scaricare i driver predefiniti per la piattaforma nella [Microsoft Drivers per PHP per SQL Server](https://github.com/Microsoft/msphpsql/releases) pagina del progetto Github. Ogni pacchetto di installazione contiene file di driver SQLSRV e PDO_SQLSRV le varianti con thread e non a thread singolo. In Windows, sono anche disponibili le varianti a 32 e 64 bit. Visualizzare [requisiti di sistema per Microsoft Drivers per PHP per SQL Server](../../connect/php/system-requirements-for-the-php-sql-driver.md) per un elenco dei file di driver che sono contenuti in ogni pacchetto. Il file del driver deve corrispondere la versione PHP, architettura e threadedness dell'ambiente di PHP.

In Linux e macOS, i driver possono in alternativa essere installati usando PECL, come individuata nel [esercitazione sull'installazione](../../connect/php/installation-tutorial-linux-mac.md).

È anche possibile compilare i driver dall'origine o durante la compilazione di PHP o tramite `phpize`. Se si sceglie di creare i driver dall'origine, è possibile scegliere di crearle in modo statico in PHP invece di compilare le estensioni come condivise aggiungendo `--enable-sqlsrv=static --with-pdo_sqlsrv=static` (in Linux e macOS) o `--enable-sqlsrv=static --with-pdo-sqlsrv=static` (on Windows) per il `./configure` comando prima di compilazione di PHP. Per altre informazioni su PHP sistema di compilazione e `phpize`, vedere la [documentazione di PHP](http://php.net/manual/install.php).
  
## <a name="moving-the-driver-file-into-your-extension-directory"></a>Spostamento del file del driver nella directory dell'estensione  
Il file del driver debba trovarsi in una directory in cui possibile trovare il runtime PHP. È più semplice inserire il file di driver nella directory dell'estensione PHP predefinito, per trovare la directory predefinita, eseguire `php -i | sls extension_dir` in Windows o `php -i | grep extension_dir` su Linux/macOS. Se non si usa la directory di estensione predefinite, specificare una directory nel file di configurazione PHP (PHP. ini), usando il **extension_dir** opzione. Ad esempio, in Windows, se è stato inserito il file del driver `c:\php\ext` directory, aggiungere la riga seguente al file PHP. ini:
  
```  
extension_dir = "c:\PHP\ext"  
```

## <a name="loading-the-driver-at-php-startup"></a>Caricamento del driver all'avvio di PHP  
Prima di caricare il driver SQLSRV all'avvio di PHP, spostare un file di driver nella directory dell'estensione. Quindi eseguire la procedura seguente:  
  
1.  Per abilitare la **SQLSRV** driver, modificare **PHP. ini** aggiungendo la riga seguente alla sezione dell'estensione, modificare il nome del file come appropriato:  
  
    In Windows: 
    ```  
    extension=php_sqlsrv_72_ts.dll  
    ```  
    In Linux, se sono stati scaricati i file binari precompilati per la distribuzione: 
    ```  
    extension=php_sqlsrv_72_nts.so  
    ```
    Se sono stati compilati SQLSRV binaria dall'origine o con PECL, verrà invece denominata sqlsrv.so:
    ```
    extension=sqlsrv.so
    ```
  
2.  Per abilitare la **PDO_SQLSRV** driver, l'estensione di oggetti dati PHP (PDO) deve essere disponibile come estensione incorporata o come un'estensione caricata in modo dinamico.

    In Windows, i file binari PHP predefiniti forniti con PDO predefinito, in modo che non è necessario modificare PHP. ini per caricarlo. Se, tuttavia, si hanno compilato PHP dall'origine e un'estensione PDO separata da compilare, verranno denominate `php_pdo.dll`, ed è necessario copiarlo nella directory dell'estensione e aggiungere la riga seguente al file PHP. ini:  
    ```
    extension=php_pdo.dll  
    ```
    In Linux, se è stato installato PHP usando Gestione pacchetti del sistema, PDO è probabilmente installato come estensione di caricato in modo dinamico denominata pdo.so. L'estensione PDO deve essere caricato prima l'estensione PDO_SQLSRV o il caricamento avrà esito negativo. Le estensioni vengono caricate in genere utilizzando i file ini singoli e questi file vengono lette dopo PHP. ini. Pertanto, se pdo.so viene caricato tramite il proprio file con estensione ini, è necessario un file separato, il caricamento del driver PDO_SQLSRV dopo PDO. 

    Per scoprire quale directory si trovano i file ini specifici dell'estensione, eseguire `php --ini` e prendere nota della directory indicata sotto `Scan for additional .ini files in:`. Trovare il file che consente di caricare pdo.so, che probabilmente è preceduto da un numero, ad esempio 10 pdo.ini. Il prefisso numerico indica l'ordine di caricamento dei file. ini, mentre i file che non hanno un prefisso numerico vengono caricati in ordine alfabetico. Creare un file per caricare il file del driver PDO_SQLSRV chiamato 30-pdo_sqlsrv.ini (qualsiasi numero maggiore di quello che i prefissi works pdo.ini) oppure pdo_sqlsrv.ini (se pdo.ini non preceduta da un numero) e aggiungere la riga seguente, modificando il nome del file come appropriato:  
    ```
    extension=php_pdo_sqlsrv_72_nts.so
    ```
    Come con SQLSRV, se sono stati compilati PDO_SQLSRV binaria dall'origine o con PECL, verrà invece denominata pdo_sqlsrv.so:
    ```
    extension=pdo_sqlsrv.so
    ```
    Copiare questo file nella directory che contiene altri file. ini. 

    Se sono stati compilati PHP dall'origine con il supporto PDO predefinito, non è necessario un file. ini separato ed è possibile aggiungere la riga appropriata in precedenza in PHP. ini.
  
3.  Riavviare il server Web.  
  
> [!NOTE]  
> Per determinare se il driver è stato caricato correttamente, eseguire uno script che effettua una chiamata a [phpinfo()](https://php.net/manual/en/function.phpinfo.php).  
  
Per altre informazioni sulle direttive di **php.ini**, vedere [Descrizione delle direttive core di php.ini](https://php.net/manual/en/ini.core.php).  
  
## <a name="see-also"></a>Vedere anche  
[Introduzione ai driver Microsoft per PHP per SQL Server](../../connect/php/getting-started-with-the-php-sql-driver.md)

[Requisiti di sistema dei driver Microsoft per PHP per SQL Server](../../connect/php/system-requirements-for-the-php-sql-driver.md)

[Guida di programmazione per i driver Microsoft per PHP per SQL Server](../../connect/php/programming-guide-for-php-sql-driver.md)

[Riferimento all'API del driver SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)

[Riferimento all'API del driver PDO_SQLSRV](../../connect/php/pdo-sqlsrv-driver-reference.md)  
  
