---
title: Formattazione di stringhe decimali e valori money (driver SQLSRV) | Microsoft Docs
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
ms.openlocfilehash: 76b6d27acedcfe2ec462a764559237a1a2218f78
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62669603"
---
# <a name="formatting-decimal-strings-and-money-values-sqlsrv-driver"></a>Formattazione di stringhe decimali e valori money (driver SQLSRV)
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Accuratezza, mantenere [tipi di dati decimali o numerici](https://docs.microsoft.com/sql/t-sql/data-types/decimal-and-numeric-transact-sql) vengono sempre recuperati sotto forma di stringhe con valori di precisione esatte e scale. Se qualsiasi valore è minore di 1, lo zero iniziale è manca. È la stessa operazione con i campi di tipo money e smallmoney così come sono campi decimali con una scala fissa pari a 4.

## <a name="add-leading-zeroes-if-missing"></a>Aggiungere zeri iniziali se mancante
Partire dalla versione 5.6.0, l'opzione `FormatDecimals` viene aggiunto al livello di connessione e istruzione sqlsrv, che consente all'utente di formattare le stringhe decimali. Questa opzione è previsto un valore booleano (true o false) e influisce solo sulla formattazione di valori numerici o decimali nei risultati recuperati. In altre parole, il `FormatDecimals` opzione non ha alcun effetto sulle altre operazioni, ad esempio inserimento o aggiornamento.

L'impostazione predefinita di `FormatDecimals` è **false**. Se impostato su true, gli zeri iniziali per le stringhe decimali verrà aggiunti per qualsiasi valore decimale minore di 1.

## <a name="configure-number-of-decimal-places"></a>Configurare numero di posizioni decimali
Con `FormatDecimals` attivata, un'altra opzione, `DecimalPlaces`, consente agli utenti di configurare il numero di posizioni decimali, la visualizzazione di dati money e smallmoney. Accetta i valori integer compreso nell'intervallo [0, 4], e potrebbe verificarsi l'arrotondamento quando visualizzata. Tuttavia, i dati sottostanti di denaro rimangono invariati.

Entrambe le opzioni possono essere impostate a livello di istruzione o di connessione e l'istruzione che imposta sempre esegue l'override dell'impostazione di connessione corrispondente. Si noti che il `DecimalPlaces` opzione **solo** influisce sui dati di denaro, e `FormatDecimals` deve essere impostata su true per `DecimalPlaces` abbiano effetto. In caso contrario, la formattazione è stata disattivata indipendentemente `DecimalPlaces` impostazione.

> [!NOTE]
> Poiché i campi di denaro o smallmoney hanno scala 4, impostazione `DecimalPlaces` valore per i numeri negativi o qualsiasi valore maggiore di 4 verranno ignorati. È consigliabile non usare tutti i dati formattati denaro come input per un calcolo qualsiasi.

## <a name="example---a-simple-fetch"></a>Esempio: un'operazione di recupero semplice
Nell'esempio seguente viene illustrato come usare le nuove opzioni in un'operazione di recupero semplice.

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

## <a name="example---format-the-output-parameter"></a>Esempio - formato il parametro di output
Se un campo di dati decimale o numerico viene restituito come le [parametro di output](../../connect/php/how-to-retrieve-output-parameters-using-the-sqlsrv-driver.md), il valore restituito sarà considerato come una stringa normale varchar. Tuttavia, se viene specificato SQLSRV_SQLTYPE_DECIMAL o SQLSRV_SQLTYPE_NUMERIC, è possibile impostare `FormatDecimals` su true per assicurarsi che non ci sia alcun mancante zeri iniziali per il valore di stringa numerici. Per altre informazioni, vedere [Procedura: Recuperare i parametri di output mediante il driver SQLSRV](../..//connect/php/how-to-retrieve-output-parameters-using-the-sqlsrv-driver.md).

Nell'esempio seguente viene illustrato come formattare il parametro di output di una stored procedure che restituisce un valore decimal(8,4).

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
