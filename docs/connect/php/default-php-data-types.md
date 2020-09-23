---
title: Tipi di dati PHP predefiniti
description: Questo argomento elenca tutti i tipi di dati predefiniti PHP con i relativi tipi di dati SQL Server quando si usa il driver Microsoft SQLSRV per PHP per SQL Server
ms.custom: ''
ms.date: 08/10/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- default data types
- converting data types
ms.assetid: b66c301d-3d20-45b8-a112-225d8f01c0bd
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c1e1cf91baf80fd6298eaaca9c9e12a0b5858d9f
ms.sourcegitcommit: d1051f05a7db81ec62d9785bb6af572408f3d4e0
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2020
ms.locfileid: "88680791"
---
# <a name="default-php-data-types"></a>Tipi di dati PHP predefiniti
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Quando si recuperano dati dal server, i [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] convertono i dati in un tipo di dati PHP predefinito se non è stato specificato alcun tipo di dati PHP dall'utente.  
  
Quando vengono restituiti dati mediante il driver PDO_SQLSRV, il tipo di dati sarà int o string.  
  
Nella parte restante di questo argomento sono descritti i tipi di dati predefiniti del driver SQLSRV.  
  
Nella tabella seguente sono elencati i tipi di dati di SQL Server (recuperati dal server), i tipi di dati PHP predefiniti (nei quali vengono convertiti i dati), nonché la codifica predefinita per i flussi e le stringhe. Per informazioni dettagliate su come specificare i tipi di dati durante il recupero di dati dal server, vedere [How to: Specify PHP Data Types](../../connect/php/how-to-specify-php-data-types.md).  
  
|Tipo di SQL Server|Tipo PHP predefinito|Codifica predefinita|  
|-------------------|--------------------|--------------------|  
|bigint|string|carattere a 8 bit<sup>1</sup>|  
|BINARY|Stream<sup>2</sup>|Binario<sup>3</sup>|  
|bit|Integer|carattere a 8 bit<sup>1</sup>|  
|char|string|carattere a 8 bit<sup>1</sup>|  
|date<sup>4</sup>|Datetime|Non applicabile|  
|datetime<sup>4</sup>|Datetime|Non applicabile|  
|datetime2<sup>4</sup>|Datetime|Non applicabile|  
|datetimeoffset<sup>4</sup>|Datetime|Non applicabile|  
|decimal|string|carattere a 8 bit<sup>1</sup>|  
|float|Float|carattere a 8 bit<sup>1</sup>|  
|geography|Stream|Binario<sup>3</sup>|  
|geometry|Stream|Binario<sup>3</sup>|  
|image<sup>5</sup>|Stream<sup>2</sup>|Binario<sup>3</sup>|  
|INT|Integer|carattere a 8 bit<sup>1</sup>|  
|money|string|carattere a 8 bit<sup>1</sup>|  
|NCHAR|string|carattere a 8 bit<sup>1</sup>|  
|NUMERIC|string|carattere a 8 bit<sup>1</sup>|  
|NVARCHAR|string|carattere a 8 bit<sup>1</sup>|  
|nvarchar(MAX)|Stream<sup>2</sup>|carattere a 8 bit<sup>1</sup>|  
|ntext<sup>6</sup>|Stream<sup>2</sup>|carattere a 8 bit<sup>1</sup>|  
|real|Float|carattere a 8 bit<sup>1</sup>|  
|smalldatetime|Datetime|carattere a 8 bit<sup>1</sup>|  
|SMALLINT|Integer|carattere a 8 bit<sup>1</sup>|  
|SMALLMONEY|string|carattere a 8 bit<sup>1</sup>|  
|sql_variant<sup>7</sup>|string|carattere a 8 bit<sup>1</sup>|  
|text<sup>8</sup>|Stream<sup>2</sup>|carattere a 8 bit<sup>1</sup>|  
|time<sup>4</sup>|Datetime|Non applicabile|  
|timestamp|string|carattere a 8 bit<sup>1</sup>|  
|TINYINT|Integer|carattere a 8 bit<sup>1</sup>|  
|UDT|Stream<sup>2</sup>|Binario<sup>3</sup>|  
|UNIQUEIDENTIFIER|String<sup>9</sup>|carattere a 8 bit<sup>1</sup>|  
|varbinary|Stream<sup>2</sup>|Binario<sup>3</sup>|  
|varbinary(MAX)|Stream<sup>2</sup>|Binario<sup>3</sup>|  
|varchar|string|carattere a 8 bit<sup>1</sup>|  
|varchar(MAX)|Stream<sup>2</sup>|carattere a 8 bit<sup>1</sup>|
|Xml|Stream<sup>2</sup>|carattere a 8 bit<sup>1</sup>|  
  

1.  I dati vengono restituiti come caratteri a 8 bit come specificato nella tabella codici delle impostazioni locali di Windows impostate nel sistema. Eventuali caratteri multibyte o che non eseguono il mapping in questa tabella codici vengono sostituiti con un carattere punto interrogativo (?) a byte singolo.  
  
2.  Se viene usato [sqlsrv_fetch_array](../../connect/php/sqlsrv-fetch-array.md) o [sqlsrv_fetch_object](../../connect/php/sqlsrv-fetch-object.md) per il recupero di dati con il tipo PHP predefinito Stream, i dati vengono restituiti come stringa con la stessa codifica del flusso. Se ad esempio un tipo binario di Microsoft SQL Server viene recuperato usando **sqlsrv_fetch_array**, il tipo restituito predefinito è una stringa binaria.  
  
3.  I dati vengono restituiti come flusso di byte non elaborati proveniente dal server senza alcuna codifica o conversione.  

4.  I tipi date e time possono essere recuperati come stringhe. Per altre informazioni, vedere [Procedura: Recuperare il tipo data e ora come stringhe usando il driver SQLSRV](../../connect/php/how-to-retrieve-date-and-time-type-as-strings-using-the-sqlsrv-driver.md).  

5.  Si tratta di un tipo legacy che esegue il mapping al tipo varbinary(max).

6. Si tratta di un tipo legacy che esegue il mapping al tipo nvarchar(max).

7.  sql_variant non è supportato nei parametri bidirezionali o di output.

8.  Si tratta di un tipo legacy che esegue il mapping al tipo varchar(max).  
  
9.  UNIQUEIDENTIFIER sono GUID rappresentati dall'espressione regolare seguente:  
  
    [0-9a-fA-F]{8}-[0-9a-fA-F]{4}-[0-9a-fA-f]{4}-[0-9a-fA-f]{4}-[0-9a-fA-F]{12}  
 
 
## <a name="other-new-sql-server-2008-data-types-and-features"></a>Nuovi tipi di dati e funzionalità di SQL Server 2008  
I tipi di dati nuovi in SQL Server 2008 e presenti all'esterno delle colonne, ad esempio i parametri con valori di tabella, non sono supportati in [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]. Nella tabella seguente viene riepilogato il supporto PHP per le nuove funzionalità di SQL Server 2008.  
  
|Feature|Supporto PHP|  
|-----------|---------------|  
|Parametro con valori di tabella|No|  
|Colonne di tipo sparse|Partial|  
|Compressione bit Null|Sì|  
|Tipi CLR definiti dall'utente di grandi dimensioni (UDT)|Sì|  
|Nome dell'entità servizio|No|  
|MERGE|Sì|  
|FILESTREAM|Partial|  
  
Il supporto dei tipi parziale indica che non è possibile eseguire una query a livello di programmazione per il tipo della colonna.  
  
## <a name="see-also"></a>Vedere anche  
[Costanti &#40;driver Microsoft per PHP per SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)

[Conversione dei tipi di dati](../../connect/php/converting-data-types.md)

[Tipi PHP](https://php.net/manual/en/language.types.php)

[Tipi di dati (Transact-SQL)](../../t-sql/data-types/data-types-transact-sql.md)

[sqlsrv_field_metadata](../../connect/php/sqlsrv-field-metadata.md)  
  
