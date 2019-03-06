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
manager: mbarwin
ms.openlocfilehash: 35626c192c3d74ad0201cee3c5e97adbce92a3aa
ms.sourcegitcommit: c1105ce638078d2c941cd656b34f78486e6b2d89
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 02/22/2019
ms.locfileid: "56676556"
---
# <a name="formatting-decimal-strings-and-money-values-pdosqlsrv-driver"></a>Formattazione di stringhe decimali e valori money (driver PDO_SQLSRV)
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Accuratezza, mantenere [tipi di dati decimali o numerici](https://docs.microsoft.com/sql/t-sql/data-types/decimal-and-numeric-transact-sql) vengono sempre recuperati sotto forma di stringhe con valori di precisione esatte e scale. Se qualsiasi valore è minore di 1, lo zero iniziale è manca. È la stessa operazione con i campi di tipo money e smallmoney così come sono campi decimali con una scala fissa pari a 4.

## <a name="add-leading-zeroes-if-missing"></a>Aggiungere zeri iniziali se mancante
A partire da versione 5.6.0, la connessione o l'attributo di istruzione `PDO::SQLSRV_ATTR_FORMAT_DECIMALS` consente all'utente di formattare le stringhe decimali. Questo attributo è previsto un valore booleano (true o false) e influisce solo sulla formattazione dei valori numerici o decimali nei risultati recuperati. In altre parole, questo attributo non ha effetto sulle altre operazioni, ad esempio inserimento o aggiornamento.

Per impostazione predefinita `PDO::SQLSRV_ATTR_FORMAT_DECIMALS` viene **false**. Se impostato su true, gli zeri iniziali per le stringhe decimali verrà aggiunti per qualsiasi valore decimale minore di 1.

## <a name="configure-number-of-decimal-places"></a>Configurare numero di posizioni decimali
Con `PDO::SQLSRV_ATTR_FORMAT_DECIMALS` attivata, un altro attributo di connessione o istruzione, `PDO::SQLSRV_ATTR_DECIMAL_PLACES`, consente agli utenti di configurare il numero di posizioni decimali, la visualizzazione di dati money e smallmoney. Accetta i valori integer compreso nell'intervallo [0, 4], e potrebbe verificarsi l'arrotondamento quando visualizzata. Tuttavia, i dati sottostanti di denaro rimangono invariati.

Gli attributi di istruzione sempre eseguire l'override delle impostazioni di connessione corrispondente. Si noti che il `PDO::SQLSRV_ATTR_DECIMAL_PLACES` opzione **solo** influisce sui dati, money e `PDO::SQLSRV_ATTR_FORMAT_DECIMALS` deve essere impostata su true. In caso contrario, la formattazione è stata disattivata indipendentemente `PDO::SQLSRV_ATTR_DECIMAL_PLACES` impostazione.

> [!NOTE]
> Poiché i campi di denaro o smallmoney hanno scala 4, impostazione `PDO::SQLSRV_ATTR_DECIMAL_PLACES` per i numeri negativi o qualsiasi valore maggiore di 4 verranno ignorati. È consigliabile non usare tutti i dati formattati denaro come input per un calcolo qualsiasi.

### <a name="to-set-the-connection-attributes"></a>Per impostare gli attributi di connessione

-   Impostare gli attributi al momento della connessione:

    ```php
    $attrs = array(PDO::SQLSRV_ATTR_FORMAT_DECIMALS => true,
                   PDO::SQLSRV_ATTR_DECIMAL_PLACES => 2);

    $conn = new PDO("sqlsrv:Server = myServer; Database = myDB", $username, $password, $attrs);
    ```

-   Impostare gli attributi di connessione post:

    ```php
    $conn = new PDO("sqlsrv:Server = myServer; Database = myDB", $username, $password);
    $conn->setAttribute(PDO::SQLSRV_ATTR_FORMAT_DECIMALS, true);
    $conn->setAttribute(PDO::SQLSRV_ATTR_DECIMAL_PLACES, 2);
    ```

## <a name="example---format-money-data"></a>Esempio: formattare i dati di denaro
Nell'esempio seguente viene illustrato come recuperare usando dati di denaro [pdostatement:: Bindcolumn](../../connect/php/pdostatement-bindcolumn.md):

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

## <a name="example---override-connection-attributes"></a>Esempio - override gli attributi di connessione
Nell'esempio seguente viene illustrato come eseguire l'override gli attributi di connessione:

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
