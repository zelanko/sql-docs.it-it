---
title: Tipi di cursore (driver PDO_SQLSRV) | Microsoft Docs
ms.custom: ''
ms.date: 05/03/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 49ea6a6e-78d4-40f8-85eb-180b527f0537
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 357bf9be35cbb976e1f35e07dc0489e9f2dc00a8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66796221"
---
# <a name="cursor-types-pdosqlsrv-driver"></a>Tipi di cursore (driver PDO_SQLSRV)
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Il driver PDO_SQLSRV consente di creare set di risultati scorrevoli con uno dei diversi cursori disponibili.

Per informazioni su come specificare un cursore con il driver PDO_SQLSRV e per esempi di codice, vedere [PDO::prepare](../../connect/php/pdo-prepare.md).

## <a name="pdosqlsrv-and-server-side-cursors"></a>PDO_SQLSRV e cursori lato server
Nelle versioni dei [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] precedenti alla 3.0, il driver PDO_SQLSRV consente di creare un set di risultati con un cursore statico o forward-only lato server. A partire dalla versione 3.0 dei [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)], sono disponibili anche cursori dinamici e keyset.

È possibile indicare il tipo di cursore lato server usando [PDO::prepare](../../connect/php/pdo-prepare.md) per selezionare uno dei tipi di cursore seguenti:

-   `PDO::ATTR_CURSOR => PDO::CURSOR_FWDONLY`

-   `PDO::ATTR_CURSOR => PDO::CURSOR_SCROLL`

È possibile richiedere un cursore dinamico, statico o keyset specificando `PDO::ATTR_CURSOR => PDO::CURSOR_SCROLL` e quindi passando il valore appropriato a `PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE`. I valori che è possibile passare a `PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE` per i cursori lato server sono i seguenti:

-   `PDO::SQLSRV_CURSOR_DYNAMIC`

-   `PDO::SQLSRV_CURSOR_STATIC`

-   `PDO::SQLSRV_CURSOR_KEYSET`

## <a name="pdosqlsrv-and-client-side-cursors"></a>PDO_SQLSRV e cursori lato client
I cursori lato client sono stati aggiunti nella versione 3.0 dei [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] e consentono di memorizzare nella cache in memoria un intero set di risultati. Un vantaggio è rappresentato dal fatto che dopo l'esecuzione di una query è disponibile il numero delle righe.

È consigliabile usare i cursori lato client per set di risultati di piccole e medie dimensioni. Per set di risultati di grandi dimensioni, usare i cursori lato server.

Quando si usa un cursore lato client, se le dimensioni del buffer non sono sufficienti a contenere un intero set di risultati, una query restituirà false. Si possono aumentare le dimensioni del buffer fino al limite di memoria di PHP.

È possibile configurare le dimensioni del buffer contenente il set di risultati con l'attributo `PDO::SQLSRV_ATTR_CLIENT_BUFFER_MAX_KB_SIZE` di [PDO::setAttribute](../../connect/php/pdo-setattribute.md) o [PDOStatement::setAttribute](../../connect/php/pdostatement-setattribute.md). Le dimensioni massime del buffer possono anche essere impostate nel file php.ini con pdo_sqlsrv.client_buffer_max_kb_size (ad esempio, pdo_sqlsrv.client_buffer_max_kb_size = 1024).

È possibile richiedere un cursore lato client con [PDO::prepare](../../connect/php/pdo-prepare.md), specificando il tipo di cursore `PDO::ATTR_CURSOR => PDO::CURSOR_SCROLL` e quindi `PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE => PDO::SQLSRV_CURSOR_BUFFERED`.

## <a name="example"></a>Esempio
L'esempio seguente illustra come specificare un cursore con buffer.
```
<?php
$database = "AdventureWorks";
$server = "(local)";
$conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "");

$query = "select * from Person.ContactType";
$stmt = $conn->prepare( $query, array(PDO::ATTR_CURSOR => PDO::CURSOR_SCROLL, PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE => PDO::SQLSRV_CURSOR_BUFFERED));
$stmt->execute();
print $stmt->rowCount();

echo "\n";

while ( $row = $stmt->fetch( PDO::FETCH_ASSOC ) ){
   print "$row[Name]\n";
}
echo "\n..\n";

$row = $stmt->fetch( PDO::FETCH_BOTH, PDO::FETCH_ORI_FIRST );
print_r($row);

$row = $stmt->fetch( PDO::FETCH_ASSOC, PDO::FETCH_ORI_REL, 1 );
print "$row[Name]\n";

$row = $stmt->fetch( PDO::FETCH_NUM, PDO::FETCH_ORI_NEXT );
print "$row[1]\n";

$row = $stmt->fetch( PDO::FETCH_NUM, PDO::FETCH_ORI_PRIOR );
print "$row[1]..\n";

$row = $stmt->fetch( PDO::FETCH_NUM, PDO::FETCH_ORI_ABS, 0 );
print_r($row);

$row = $stmt->fetch( PDO::FETCH_NUM, PDO::FETCH_ORI_LAST );
print_r($row);
?>
```

## <a name="see-also"></a>Vedere anche
[Specifica di un tipo di cursore e selezione di righe](../../connect/php/specifying-a-cursor-type-and-selecting-rows.md)

