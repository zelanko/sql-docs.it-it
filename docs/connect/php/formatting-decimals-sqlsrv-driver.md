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
manager: v-mabarw
ms.openlocfilehash: 4a5ac641a98077c09bb38a5fc8fbd3fb1a4bf73d
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/16/2019
ms.locfileid: "68265139"
---
# <a name="formatting-decimal-strings-and-money-values-sqlsrv-driver"></a>Formattazione di stringhe decimali e valori money (driver SQLSRV)
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Per mantenere l'accuratezza, i [tipi decimali o numerici](https://docs.microsoft.com/sql/t-sql/data-types/decimal-and-numeric-transact-sql) vengono sempre recuperati come stringhe con precisione e scale esatte. Se un valore è minore di 1, lo zero principale risulta mancante. Si tratta dello stesso valore con i campi Money e smallmoney, perché si tratta di campi decimali con una scala fissa uguale a 4.

## <a name="add-leading-zeroes-if-missing"></a>Aggiungi zeri iniziali se mancanti
A partire dalla versione 5.6.0, l' `FormatDecimals` opzione viene aggiunta alla connessione sqlsrv e ai livelli di istruzione, che consente all'utente di formattare le stringhe decimali. Questa opzione prevede un valore booleano (true o false) e influiscono solo sulla formattazione dei valori decimali o numerici nei risultati recuperati. In altre parole, l' `FormatDecimals` opzione non ha alcun effetto su altre operazioni come l'inserimento o l'aggiornamento.

L'impostazione predefinita di `FormatDecimals` è **false**. Se è impostato su true, verranno aggiunti gli zeri iniziali alle stringhe decimali per qualsiasi valore decimale minore di 1.

## <a name="configure-number-of-decimal-places"></a>Configurare il numero di posizioni decimali
Con `FormatDecimals` attivato, un'altra opzione, `DecimalPlaces`, consente agli utenti di configurare il numero di posizioni decimali durante la visualizzazione dei dati Money e smallmoney. Accetta i valori interi nell'intervallo [0, 4] e l'arrotondamento può verificarsi quando viene visualizzato. Tuttavia, i dati monetari sottostanti rimangono invariati.

Entrambe le opzioni possono essere impostate sul livello di connessione o di istruzione e l'impostazione dell'istruzione esegue sempre l'override dell'impostazione di connessione corrispondente. Si noti che `DecimalPlaces` l'opzione influisce **solo** sui dati `FormatDecimals` Money e deve essere impostata su `DecimalPlaces` true per avere effetto. In caso contrario, la formattazione viene disattivata indipendentemente dall' `DecimalPlaces` impostazione.

> [!NOTE]
> Poiché i campi Money o smallmoney hanno scala 4, `DecimalPlaces` l'impostazione del valore su un numero negativo o su un valore maggiore di 4 verrà ignorata. Non è consigliabile usare i dati di Money formattati come input per qualsiasi calcolo.

## <a name="example---a-simple-fetch"></a>Esempio: recupero semplice
Nell'esempio seguente viene illustrato come utilizzare le nuove opzioni in un recupero semplice.

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
Se come [parametro di output](../../connect/php/how-to-retrieve-output-parameters-using-the-sqlsrv-driver.md)viene restituito un campo numerico o decimale, il valore restituito verrà considerato come una normale stringa varchar. Tuttavia, se si specifica SQLSRV_SQLTYPE_DECIMAL o SQLSRV_SQLTYPE_NUMERIC, è possibile impostare `FormatDecimals` su true per assicurarsi che non sia presente zero per il valore della stringa numerica. Per altre informazioni, vedere [Procedura: Recuperare i parametri di output mediante il driver SQLSRV](../..//connect/php/how-to-retrieve-output-parameters-using-the-sqlsrv-driver.md).

Nell'esempio seguente viene illustrato come formattare il parametro di output di un stored procedure che restituisce un valore Decimal (8, 4).

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
