---
title: Caricamento dei Driver Microsoft per PHP
description: In questa pagina vengono specificate le istruzioni per il caricamento dei Driver Microsoft per PHP per SQL Server nello spazio di elaborazione PHP.
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 73899b2ea917c3981b0c696b78de453eacbf894d
ms.sourcegitcommit: 8ffc23126609b1cbe2f6820f9a823c5850205372
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/17/2020
ms.locfileid: "81632773"
---
# <a name="loading-the-microsoft-drivers-for-php-for-sql-server"></a>Caricamento dei Driver Microsoft per PHP per SQL Server
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

In questa pagina vengono specificate le istruzioni per il caricamento dei [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] nello spazio di elaborazione PHP.  
  
È possibile scaricare i driver predefiniti per la piattaforma in uso dalla pagina del progetto GitHub [Driver Microsoft per PHP per SQL Server](https://github.com/Microsoft/msphpsql/releases). Ogni pacchetto di installazione contiene i file dei driver SQLSRV e PDO_SQLSRV nelle varianti con e senza threading. In Windows sono disponibili anche in varianti a 32 bit e a 64 bit. Vedere [Requisiti di sistema dei driver Microsoft per PHP per SQL Server](system-requirements-for-the-php-sql-driver.md) per un elenco dei file dei driver contenuti in ogni pacchetto. Il file del driver deve corrispondere alla versione di PHP, all'architettura e alle caratteristiche del threading dell'ambiente PHP.

In Linux e macOS i driver in alternativa possono essere installati usando PECL, come indicato nell'[esercitazione sull'installazione](installation-tutorial-linux-mac.md).

È anche possibile compilare i driver dall'origine quando si compila PHP o usando `phpize`. Se si sceglie di compilare i driver dall'origine, è possibile crearli in modo statico in PHP anziché come estensioni condivise aggiungendo `--enable-sqlsrv=static --with-pdo_sqlsrv=static` (in Linux e macOS) o `--enable-sqlsrv=static --with-pdo-sqlsrv=static` (in Windows) al comando `./configure` durante la compilazione di PHP. Per altre informazioni sul sistema di compilazione di PHP e `phpize`, vedere la [documentazione di PHP](http://php.net/manual/install.php).
  
## <a name="moving-the-driver-file-into-your-extension-directory"></a>Spostamento del file del driver nella directory dell'estensione  
Il file del driver deve trovarsi in una directory in cui il runtime PHP è in grado di trovarlo. È più semplice inserire il file del driver nella directory dell'estensione PHP predefinita: per trovare la directory predefinita, eseguire `php -i | sls extension_dir` in Windows o `php -i | grep extension_dir` in Linux/macOS. Se non si usa la directory dell'estensione predefinita, specificare una directory nel file di configurazione PHP (php.ini), usando l'opzione **extension_dir**. Ad esempio, se in Windows il file del driver è stato inserito nella directory `c:\php\ext`, aggiungere la riga seguente a php.ini:
  
```  
extension_dir = "c:\PHP\ext"  
```

## <a name="loading-the-driver-at-php-startup"></a>Caricamento del driver all'avvio di PHP  
Prima di caricare il driver SQLSRV all'avvio di PHP, spostare un file di driver nella directory dell'estensione. Quindi eseguire la procedura seguente:  
  
1.  Per abilitare il driver **SQLSRV**, modificare **php.ini** aggiungendo la riga seguente alla sezione dell'estensione, modificando il nome del file in base alle esigenze:  
  
    In Windows: 
    ```  
    extension=php_sqlsrv_72_ts.dll  
    ```  
    In Linux, se sono stati scaricati i file binari predefiniti per la distribuzione: 
    ```  
    extension=php_sqlsrv_72_nts.so  
    ```
    Se il file binario SQLSRV è stato compilato dall'origine o con PECL, sarà invece denominato sqlsrv.so:
    ```
    extension=sqlsrv.so
    ```
  
2.  Per abilitare il driver **PDO_SQLSRV**, è necessario che l'estensione PHP Data Objects (PDO) sia disponibile come estensione predefinita o come estensione caricata dinamicamente.

    In Windows i file binari PHP predefiniti sono disponibili con PDO come estensione incorporata, quindi non è necessario modificare php.ini per caricarlo. Se tuttavia la compilazione di PHP è stata eseguita dall'origine ed è stata specificata un'estensione PDO separata da compilare, questa verrà denominata `php_pdo.dll` ed è necessario copiarla nella directory dell'estensione e aggiungere la riga seguente a php.ini:  
    ```
    extension=php_pdo.dll  
    ```
    In Linux, se l'installazione di PHP è stata eseguita usando la gestione pacchetti del sistema, è probabile che PDO venga installata come estensione caricata dinamicamente con il nome pdo.so. L'estensione PDO deve essere caricata prima dell'estensione PDO_SQLSRV o il caricamento avrà esito negativo. Le estensioni vengono in genere caricate usando singoli file INI e questi file vengono letti dopo php.ini. Di conseguenza, se pdo.so viene caricato con un proprio file INI, è necessario un file separato che carica il driver PDO_SQLSRV dopo PDO. 

    Per sapere in quale directory si trovano i file INI specifici dell'estensione, eseguire `php --ini` e individuare la directory elencata in `Scan for additional .ini files in:`. Trovare il file che carica pdo.so. È probabile che il nome sia preceduto da un numero, ad esempio 10-pdo.ini. Il prefisso numerico indica l'ordine di caricamento dei file INI, mentre i file che non hanno un prefisso numerico vengono caricati in ordine alfabetico. Creare un file per caricare il file del driver PDO_SQLSRV denominato 30-pdo_sqlsrv.ini (funziona qualsiasi numero superiore al prefisso di pdo.ini) o pdo_sqlsrv.ini (se pdo.ini non ha un prefisso numerico) e aggiungere la riga seguente al file, modificando il nome del file in base alle esigenze:  
    ```
    extension=php_pdo_sqlsrv_72_nts.so
    ```
    Come per SQLSRV, se il file binario SQLSRV è stato compilato dall'origine o con PECL, sarà invece denominato pdo_sqlsrv.so:
    ```
    extension=pdo_sqlsrv.so
    ```
    Copiare questo file nella directory che contiene gli altri file INI. 

    Se la compilazione di PHP è stata eseguita dall'origine con il supporto PDO predefinito, non è necessario un file INI separato ed è possibile aggiungere la riga appropriata a php.ini.
  
3.  Riavviare il server Web.  
  
> [!NOTE]  
> Per determinare se il driver è stato caricato correttamente, eseguire uno script che effettua una chiamata a [phpinfo()](https://php.net/manual/en/function.phpinfo.php).  
  
Per altre informazioni sulle direttive di **php.ini**, vedere [Descrizione delle direttive core di php.ini](https://php.net/manual/en/ini.core.php).  
  
## <a name="see-also"></a>Vedere anche  
[Introduzione ai driver Microsoft per PHP per SQL Server](getting-started-with-the-php-sql-driver.md)

[Requisiti di sistema dei driver Microsoft per PHP per SQL Server](system-requirements-for-the-php-sql-driver.md)

[Guida alla programmazione per i driver Microsoft per PHP per SQL Server](programming-guide-for-php-sql-driver.md)

[Riferimento all'API del driver SQLSRV](sqlsrv-driver-api-reference.md)

[Riferimento all'API del driver PDO_SQLSRV](pdo-sqlsrv-driver-reference.md)  
  
