---
title: Formattazione di stringhe decimali e valori money (driver PDO_SQLSRV) | Microsoft Docs
ms.custom: ''
ms.date: 02/11/2019
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- formatting, decimal types, money values
author: yitam
ms.author: v-yitam
manager: v-mabarw
ms.openlocfilehash: 76c314159faf15e63bf77b17a8a45abf217b205c
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/16/2019
ms.locfileid: "68265146"
---
# <a name="formatting-decimal-strings-and-money-values-pdosqlsrv-driver"></a>Formattazione di stringhe decimali e valori money (driver PDO_SQLSRV)
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Per mantenere l'accuratezza, i [tipi decimali o numerici](https://docs.microsoft.com/sql/t-sql/data-types/decimal-and-numeric-transact-sql) vengono sempre recuperati come stringhe con precisione e scale esatte. Se un valore è minore di 1, lo zero principale risulta mancante. Si tratta dello stesso valore con i campi Money e smallmoney, perché si tratta di campi decimali con una scala fissa uguale a 4.

## <a name="add-leading-zeroes-if-missing"></a>Aggiungi zeri iniziali se mancanti
A partire dalla versione 5.6.0, l'attributo `PDO::SQLSRV_ATTR_FORMAT_DECIMALS` Connection o Statement consente all'utente di formattare stringhe decimali. Questo attributo prevede un valore booleano (true o false) e influiscono solo sulla formattazione dei valori decimali o numerici nei risultati recuperati. In altre parole, questo attributo non ha alcun effetto su altre operazioni come l'inserimento o l'aggiornamento.

L'impostazione predefinita di `PDO::SQLSRV_ATTR_FORMAT_DECIMALS` è **false**. Se è impostato su true, verranno aggiunti gli zeri iniziali alle stringhe decimali per qualsiasi valore decimale minore di 1.

## <a name="configure-number-of-decimal-places"></a>Configurare il numero di posizioni decimali
Con `PDO::SQLSRV_ATTR_FORMAT_DECIMALS` attivato, un altro attributo di connessione o di `PDO::SQLSRV_ATTR_DECIMAL_PLACES`istruzione,, consente agli utenti di configurare il numero di posizioni decimali durante la visualizzazione dei dati Money e smallmoney. Accetta i valori interi nell'intervallo [0, 4] e l'arrotondamento può verificarsi quando viene visualizzato. Tuttavia, i dati monetari sottostanti rimangono invariati.

Gli attributi dell'istruzione sostituiscono sempre le impostazioni di connessione corrispondenti. Si noti che `PDO::SQLSRV_ATTR_DECIMAL_PLACES` l'opzione influisca **solo** sui dati `PDO::SQLSRV_ATTR_FORMAT_DECIMALS` Money e deve essere impostata su true. In caso contrario, la formattazione viene disattivata indipendentemente dall' `PDO::SQLSRV_ATTR_DECIMAL_PLACES` impostazione.

> [!NOTE]
> Poiché i campi Money o smallmoney hanno scala 4, `PDO::SQLSRV_ATTR_DECIMAL_PLACES` l'impostazione su un numero negativo o su un valore maggiore di 4 verrà ignorata. Non è consigliabile usare i dati di Money formattati come input per qualsiasi calcolo.

### <a name="to-set-the-connection-attributes"></a>Per impostare gli attributi di connessione

-   Impostare gli attributi al momento della connessione:

    ```php
    $attrs = array(PDO::SQLSRV_ATTR_FORMAT_DECIMALS => true,
                   PDO::SQLSRV_ATTR_DECIMAL_PLACES => 2);

    $conn = new PDO("sqlsrv:Server = myServer; Database = myDB", $username, $password, $attrs);
    ```

-   Imposta attributi post connessione:

    ```php
    $conn = new PDO("sqlsrv:Server = myServer; Database = myDB", $username, $password);
    $conn->setAttribute(PDO::SQLSRV_ATTR_FORMAT_DECIMALS, true);
    $conn->setAttribute(PDO::SQLSRV_ATTR_DECIMAL_PLACES, 2);
    ```

## <a name="example---format-money-data"></a>Esempio-formattare i dati Money
Nell'esempio seguente viene illustrato come recuperare i dati Money usando [PDOStatement:: bindColumn](../../connect/php/pdostatement-bindcolumn.md):

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

## <a name="example---override-connection-attributes"></a>Esempio-override degli attributi di connessione
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
