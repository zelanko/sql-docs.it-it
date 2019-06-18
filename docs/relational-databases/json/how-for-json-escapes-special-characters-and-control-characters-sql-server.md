---
title: Modalità di uso di FOR JSON delle sequenze di escape per i caratteri speciali e di controllo (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: genemi
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- FOR JSON, special characters
ms.assetid: 4ba90025-5a09-4f0a-836a-54c886324530
author: jovanpop-msft
ms.author: jovanpop
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 49c1cbd82b6a4dd1f65f0c3e31c9f8612d0b11dc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62683781"
---
# <a name="how-for-json-escapes-special-characters-and-control-characters-sql-server"></a>Modalità di uso di FOR JSON delle sequenze di escape per i caratteri speciali e di controllo (SQL Server)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  Questo argomento descrive il modo in cui la clausola **FOR JSON** di un'istruzione **SELECT** di SQL Server usa sequenze di escape per i caratteri speciali e rappresenta i caratteri di controllo nell'output JSON.  

> [!IMPORTANT]
> Questa pagina descrive il supporto incorporato per JSON in Microsoft SQL Server. Per informazioni generali sull'uso di escape e sulla codifica in JSON, vedere la sezione 2.5 della specifica JSON RFC - [https://www.ietf.org/rfc/rfc4627.txt](https://www.ietf.org/rfc/rfc4627.txt).

## <a name="escaping-of-special-characters"></a>Escape di caratteri speciali  
Se i dati di origine contengono caratteri speciali, la clausola **FOR JSON** usa sequenze di escape per tali caratteri nell'output JSON con `\`, come illustrato nella tabella seguente. I caratteri di escape vengono usati sia nei nomi delle proprietà che nei relativi valori.  
  
|**Carattere speciale**|**Output con caratteri di escape**|  
|---------------------------|--------------------------|  
|Virgoletta (")|\\"|  
|Barra rovesciata (\\)|\\\|  
|Barra (/)|\\/|  
|Backspace|\b|  
|Avanzamento carta|\f|  
|Nuova riga|\n|  
|Ritorno a capo|\r|  
|Tabulazione orizzontale|\t|  
  
## <a name="control-characters"></a>Caratteri di controllo  
Se i dati di origine contengono caratteri di controllo, la clausola **FOR JSON** codifica tali caratteri nell'output JSON nel formato `\u<code>`, come illustrato nella tabella seguente.  
  
|**Carattere di controllo**|**Output codificato**|  
|---------------------------|--------------------------|  
|CHAR(0)|\u0000|  
|CHAR(1)|\u0001|  
|...|...|  
|CHAR(31)|\u001f|  
  
## <a name="example"></a>Esempio  
 Di seguito è riportato un esempio dell'output di **FOR JSON** per dati di origine che includono sia caratteri di escape che caratteri di controllo.  
  
 Query:  
  
```sql  
SELECT  
  'VALUE\    /  
  "' as [KEY\/"],  
  CHAR(0) as '0',  
  CHAR(1) as '1',  
  CHAR(31) as '31'  
FOR JSON PATH  
```  
  
 Risultato:  
  
```json  
{
    "KEY\\\t\/\"": "VALUE\\\t\/\r\n\"",
    "0": "\u0000",
    "1": "\u0001",
    "31": "\u001f"
}
```  

## <a name="learn-more-about-json-in-sql-server-and-azure-sql-database"></a>Altre informazioni su JSON in SQL Server e nel database SQL di Azure  
  
### <a name="microsoft-videos"></a>Video Microsoft

Per un'introduzione visiva al supporto JSON predefinito in SQL Server e nel database SQL di Azure, vedere i video seguenti:

-   [SQL Server 2016 and JSON Support](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support) (SQL Server 2016 e supporto JSON)

-   [Using JSON in SQL Server 2016 and Azure SQL Database](https://channel9.msdn.com/Shows/Data-Exposed/Using-JSON-in-SQL-Server-2016-and-Azure-SQL-Database) (Uso di JSON in SQL Server 2016 e nel database SQL di Azure)

-   [JSON as a bridge between NoSQL and relational worlds](https://channel9.msdn.com/events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds) (JSON come ponte tra NoSQL e gli ambienti relazionali)
  
## <a name="see-also"></a>Vedere anche  
 [Formattare i risultati delle query in formato JSON con FOR JSON &#40;SQL Server&#41;](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md)  
[Clausola FOR](../../t-sql/queries/select-for-clause-transact-sql.md)
