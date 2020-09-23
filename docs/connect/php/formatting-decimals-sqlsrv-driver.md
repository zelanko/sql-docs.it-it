---
title: Formattazione di stringhe decimali e valori money (driver SQLSRV)
description: Informazioni su come usare le opzioni FormatDecimals e DecimalPlaces per formattare valori decimali o valori money quando si usa il driver Microsoft SQLSRV per PHP per SQL Server.
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
ms.openlocfilehash: c6d77fb9fcfdc720c4053688f8f0dcf759af15c8
ms.sourcegitcommit: d1051f05a7db81ec62d9785bb6af572408f3d4e0
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2020
ms.locfileid: "88680726"
---
# <a name="formatting-decimal-strings-and-money-values-sqlsrv-driver"></a>Formattazione di stringhe decimali e valori money (driver SQLSRV)
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Per mantenere l'accuratezza, i [tipi decimali o numerici](https://docs.microsoft.com/sql/t-sql/data-types/decimal-and-numeric-transact-sql) vengono sempre recuperati come stringhe con precisioni e scale esatte. Se un valore è minore di 1, lo zero iniziale è mancante. Lo stesso vale per i campi money e smallmoney, poiché sono campi decimali con una scala fissa uguale a 4.

## <a name="add-leading-zeroes-if-missing"></a>Aggiungere zeri iniziali se mancanti
A partire dalla versione 5.6.0, l'opzione `FormatDecimals` viene aggiunta ai livelli di connessione e istruzione sqlsrv per consentire all'utente di formattare le stringhe decimali. Questa opzione prevede un valore booleano (true o false) e riguarda solo la formattazione dei valori decimali o numerici nei risultati recuperati. In altri termini, l'opzione `FormatDecimals` non ha effetto su altre operazioni come l'inserimento o l'aggiornamento.

L'impostazione predefinita di `FormatDecimals` è **false**. Se è impostato su true, verranno aggiunti gli zeri iniziali alle stringhe decimali per qualsiasi valore decimale minore di 1.

## <a name="configure-number-of-decimal-places"></a>Configurare il numero di posizioni decimali
Con l'opzione `FormatDecimals` attivata, un'altra opzione, `DecimalPlaces`, consente agli utenti di configurare il numero di posizioni decimali durante la visualizzazione dei dati money e smallmoney. Accetta i valori interi nell'intervallo [0, 4] e può essere arrotondato quando indicato. I dati di tipo money sottostanti rimangono tuttavia invariati.

Entrambe le opzioni possono essere impostate sul livello di connessione o di istruzione e l'impostazione dell'istruzione esegue sempre l'override dell'impostazione della connessione corrispondente. Si noti che l'opzione `DecimalPlaces` riguarda **solo** i dati di tipo money ed è necessario impostare `FormatDecimals` su true affinché `DecimalPlaces` abbia effetto. In caso contrario, la formattazione viene disattivata indipendentemente dall'impostazione di `DecimalPlaces`.

> [!NOTE]
> Poiché i campi money o smallmoney hanno scala 4, se si imposta il valore di `DecimalPlaces` su un numero negativo o su un valore maggiore di 4 tale impostazione verrà ignorata. Non è consigliabile usare i dati di tipo money formattati come input per qualsiasi calcolo.

## <a name="example---a-simple-fetch"></a>Esempio: recupero semplice
Nell'esempio seguente viene illustrato come usare le nuove opzioni in un recupero semplice.

```php
<?php
$username = 'myusername';
$password = 'mypasword';
$tableName = 'mytable';

$connectionInfo = array("UID" => $username, "PWD" => $password, "Database" => "myDB", "FormatDecimals" => true);  
$server = "myServer";  // IP address also works
$conn = sqlsrv_connect( $server, $connectionInfo);  

$numDigits = 2;
$query = "SELECT money1 FROM $tableName";
$options = array("DecimalPlaces" => $numDigits);
$stmt = sqlsrv_prepare($conn, $query, array(), $options);
sqlsrv_execute($stmt);

if (sqlsrv_fetch($stmt)) {
    $field = sqlsrv_get_field($stmt, 0);  
    echo $field;   // expect a numeric value string with 2 decimal places
}

sqlsrv_free_stmt($stmt);
sqlsrv_close($conn);
?>
```

## <a name="example---format-the-output-parameter"></a>Esempio: formattare il parametro di output
Se un campo decimale o numerico viene restituito come [parametro di output](../../connect/php/how-to-retrieve-output-parameters-using-the-sqlsrv-driver.md), il valore restituito verrà considerato come una normale stringa varchar. Se tuttavia si specifica sia SQLSRV_SQLTYPE_DECIMAL sia SQLSRV_SQLTYPE_NUMERIC, è possibile impostare `FormatDecimals` su true per assicurarsi che non vi siano zeri iniziali mancanti per il valore della stringa numerica. Per altre informazioni, vedere [Procedura: Recuperare i parametri di output mediante il driver SQLSRV](../..//connect/php/how-to-retrieve-output-parameters-using-the-sqlsrv-driver.md).

Nell'esempio seguente viene illustrato come formattare il parametro di output di una stored procedure che restituisce un valore decimale (8, 4).

```php
$outString = '';
$outSql = '{CALL myStoredProc(?)}';
$stmt = sqlsrv_prepare($conn, 
                       $outSql, 
                       array(array(&$outString, SQLSRV_PARAM_OUT, null, SQLSRV_SQLTYPE_DECIMAL(8, 4))),
                       array('FormatDecimals' => true));

if (sqlsrv_execute($stmt)) {
    echo $outString;  // expect a numeric value string with no missing leading zero
}
```

## <a name="see-also"></a>Vedere anche
[Formattazione di stringhe decimali e valori money (driver PDO_SQLSRV)](../../connect/php/formatting-decimals-pdo-sqlsrv-driver.md)

[Recupero di dati](../../connect/php/retrieving-data.md)
