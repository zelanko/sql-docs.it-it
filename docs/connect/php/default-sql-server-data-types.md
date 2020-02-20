---
title: Tipi di dati di SQL Server predefiniti | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- default data types
- converting data types
ms.assetid: 65c7c211-96d3-4e65-a1de-1fe8d21348e7
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 69c138e7eb5d2c4f6dbace0db59ce235e1c0a5f9
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "67993664"
---
# <a name="default-sql-server-data-types"></a>Tipi di dati di SQL Server predefiniti
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Se l'utente non ha specificato alcun tipo di dati di SQL Server, quando si inviano dati al server, i [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] convertono i dati dal tipo di dati PHP a un tipo di dati di SQL Server. Nella tabella seguente sono elencati il tipo di dati PHP (il tipo di dati inviato al server) e il tipo di dati di SQL Server predefinito (il tipo di dati in cui i dati vengono convertiti). Per informazioni dettagliate su come specificare i tipi di dati in fase di invio dei dati al server, vedere [Procedura: Specificare i tipi di dati di SQL Server con il driver SQLSRV](../../connect/php/how-to-specify-sql-server-data-types-when-using-the-sqlsrv-driver.md).  
  
|Tipo di dati PHP|Tipo di dati di Server SQL predefinito nel driver SQLSRV|Tipo di dati di Server SQL predefinito nel driver PDO_SQLSRV|  
|-----------------|------------------------------------------------|-----------------------------------------------------|  
|NULL|varchar(1)|non supportato|  
|Boolean|bit|bit|  
|Integer|INT|INT|  
|Float|float(24)|non supportato|  
|Stringa (lunghezza minore di 8000 byte)|varchar(<string length>)|varchar(<string length>)|  
|Stringa (lunghezza maggiore di 8000 byte)|ntext|ntext|  
|Risorsa|Non supportato.|Non supportato.|  
|Flusso (codifica: non binaria)|ntext|ntext|  
|Flusso (codifica: binaria)|varbinary|varbinary|  
|Array|Non supportato.|Non supportato.|  
|Oggetto|Non supportato.|Non supportato.|  
|DateTime (1)|Datetime|Non supportato.|  
  
## <a name="see-also"></a>Vedere anche  
[Costanti &#40;driver Microsoft per PHP per SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)

[Conversione dei tipi di dati](../../connect/php/converting-data-types.md)

[sqlsrv_field_metadata](../../connect/php/sqlsrv-field-metadata.md)

[Tipi PHP](https://php.net/manual/language.types.php)

[Tipi di dati (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/data-types/data-types-transact-sql)  
  
