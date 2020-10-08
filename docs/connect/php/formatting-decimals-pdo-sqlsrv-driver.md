---
title: Formattazione di stringhe decimali e valori money (driver PDO_SQLSRV)
description: Informazioni su come usare gli attributi PDO::SQLSRV_ATTR_FORMAT_DECIMALS e SQLSRV_ATTR_DECIMAL_PLACES per formattare valori decimali o valori money quando si usa il driver PDO_SQLSRV
ms.custom: ''
ms.date: 08/10/2020
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- formatting, decimal types, money values
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: db9392b523be8777a96e4d262cfca5acccc8f406
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/05/2020
ms.locfileid: "91726842"
---
# <a name="formatting-decimal-strings-and-money-values-pdo_sqlsrv-driver"></a>Formattazione di stringhe decimali e valori money (driver PDO_SQLSRV)
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Per mantenere l'accuratezza, i [tipi decimali o numerici](../../t-sql/data-types/decimal-and-numeric-transact-sql.md) vengono sempre recuperati come stringhe con precisioni e scale esatte. Se un valore è minore di 1, lo zero iniziale è mancante. Lo stesso vale per i campi money e smallmoney, poiché sono campi decimali con una scala fissa uguale a 4.

## <a name="add-leading-zeroes-if-missing"></a>Aggiungere zeri iniziali se mancanti
A partire dalla versione 5.6.0, l'attributo di connessione o di istruzione `PDO::SQLSRV_ATTR_FORMAT_DECIMALS` consente all'utente di formattare le stringhe decimali. Questo attributo prevede un valore booleano (true o false) e riguarda solo la formattazione dei valori decimali o numerici nei risultati recuperati. In altri termini, questo attributo non ha effetto su altre operazioni come l'inserimento o l'aggiornamento.

L'impostazione predefinita di `PDO::SQLSRV_ATTR_FORMAT_DECIMALS` è **false**. Se è impostato su true, verranno aggiunti gli zeri iniziali alle stringhe decimali per qualsiasi valore decimale minore di 1.

## <a name="configure-number-of-decimal-places"></a>Configurare il numero di posizioni decimali
Con l'attributo `PDO::SQLSRV_ATTR_FORMAT_DECIMALS` attivato, un altro attributo di connessione o di istruzione, `PDO::SQLSRV_ATTR_DECIMAL_PLACES`, consente agli utenti di configurare il numero di posizioni decimali durante la visualizzazione dei dati money e smallmoney. Accetta i valori interi nell'intervallo [0, 4] e può essere arrotondato quando indicato. I dati di tipo money sottostanti rimangono tuttavia invariati.

Gli attributi dell'istruzione eseguono sempre l'override delle impostazioni della connessione corrispondenti. Si noti che l'opzione `PDO::SQLSRV_ATTR_DECIMAL_PLACES` riguarda **solo** i dati di tipo money e l'attributo `PDO::SQLSRV_ATTR_FORMAT_DECIMALS` deve essere impostato su true. In caso contrario, la formattazione viene disattivata indipendentemente dall'impostazione di `PDO::SQLSRV_ATTR_DECIMAL_PLACES`.

> [!NOTE]
> Poiché i campi money o smallmoney hanno scala 4, l'impostazione di `PDO::SQLSRV_ATTR_DECIMAL_PLACES` su un numero negativo o su un valore maggiore di 4 verrà ignorata. Non è consigliabile usare i dati di tipo money formattati come input per qualsiasi calcolo.

### <a name="to-set-the-connection-attributes"></a>Per impostare gli attributi di connessione

-   Impostare gli attributi nel punto di connessione:

    ```php
    $attrs = array(PDO::SQLSRV_ATTR_FORMAT_DECIMALS => true,
                   PDO::SQLSRV_ATTR_DECIMAL_PLACES => 2);

    $conn = new PDO("sqlsrv:Server = myServer; Database = myDB", $username, $password, $attrs);
    ```

-   Impostare gli attributi dopo la connessione:

    ```php
    $conn = new PDO("sqlsrv:Server = myServer; Database = myDB", $username, $password);
    $conn->setAttribute(PDO::SQLSRV_ATTR_FORMAT_DECIMALS, true);
    $conn->setAttribute(PDO::SQLSRV_ATTR_DECIMAL_PLACES, 2);
    ```

## <a name="example---format-money-data"></a>Esempio: formattare i dati di tipo money
Nell'esempio seguente viene illustrato come recuperare i dati di tipo money tramite [PDOStatement::bindColumn](../../connect/php/pdostatement-bindcolumn.md):

```php
<?php
$database = "myDB";
$server = "(local)";
$conn = new PDO( "sqlsrv:server=$server; Database = $database", "", "");
$conn->setAttribute(PDO::SQLSRV_ATTR_FORMAT_DECIMALS, true);

$numDigits = 3;
$query = "SELECT smallmoney1 FROM aTable";
$options = array(PDO::SQLSRV_ATTR_DECIMAL_PLACES => $numDigits);
$stmt = $conn->prepare($query, $options);
$stmt->execute();

$stmt->bindColumn('smallmoney1', $field);
$result = $stmt->fetch(PDO::FETCH_BOUND);
echo $field;    // expect a number string with 3 decimal places

unset($stmt);
unset($conn);
?>
```

## <a name="example---override-connection-attributes"></a>Esempio: eseguire l'override degli attributi di connessione
Nell'esempio seguente viene illustrato come eseguire l'override degli attributi di connessione:

```php
<?php
$database = 'myDatabase';
$server = 'myServer';
$username = 'myuser';
$password = 'mypassword'

$conn = new PDO("sqlsrv:server=$server; Database = $database", $username, $password);
$conn->setAttribute(PDO::SQLSRV_ATTR_FORMAT_DECIMALS, true);
$conn->setAttribute(PDO::SQLSRV_ATTR_DECIMAL_PLACES, 2);

$query = 'SELECT smallmoney1 FROM testTable1';
$options = array(PDO::SQLSRV_ATTR_FORMAT_DECIMALS => false);
$stmt = $conn->prepare($query, $options);
$stmt->execute();

$stmt->bindColumn('smallmoney1', $field);
$result = $stmt->fetch(PDO::FETCH_BOUND);  
echo $field;   // expect a number string showing the original scale -- 4 decimal places

unset($stmt);
unset($conn);
?>
```

## <a name="see-also"></a>Vedere anche
[Formattazione di stringhe decimali e valori money (driver SQLSRV)](../../connect/php/formatting-decimals-sqlsrv-driver.md)

[Recupero di dati](../../connect/php/retrieving-data.md)