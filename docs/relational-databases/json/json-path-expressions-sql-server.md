---
description: Espressioni di percorso JSON (SQL Server)
title: Espressioni di percorso JSON
ms.date: 06/03/2020
ms.prod: sql
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- JSON, path expressions
- path expressions (JSON)
ms.assetid: 25ea679c-84cc-4977-867c-2cbe9d192553
author: jovanpop-msft
ms.author: jovanpop
ms.reviewer: jroth
ms.custom: seo-dt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8be99986e6ca9ded5bb28e53b5c3ae166e8b86b3
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/26/2020
ms.locfileid: "88490948"
---
# <a name="json-path-expressions-sql-server"></a>Espressioni di percorso JSON (SQL Server)
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

 Usare le espressioni di percorso JSON per fare riferimento alle proprietà degli oggetti JSON.  
  
 È necessario specificare un'espressione di percorso quando si chiamano le funzioni seguenti.  
  
-   Quando si chiama **OPENJSON** per creare una vista relazionale dei dati JSON. Per altre informazioni, vedere [OPENJSON &#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md).  
  
-   Quando si chiama **JSON_VALUE** per estrarre un valore dal testo JSON. Per altre informazioni, vedere [JSON_VALUE &#40;Transact-SQL&#41;](../../t-sql/functions/json-value-transact-sql.md).  
  
-   Quando si chiama **JSON_QUERY** per estrarre un oggetto o una matrice JSON. Per altre informazioni, vedere [JSON_QUERY &#40;Transact-SQL&#41;](../../t-sql/functions/json-query-transact-sql.md).  
  
-   Quando si chiama **JSON_MODIFY** per aggiornare il valore di una proprietà in una stringa JSON. Per altre informazioni, vedere [JSON_MODIFY &#40;Transact-SQL&#41;](../../t-sql/functions/json-modify-transact-sql.md).  

## <a name="parts-of-a-path-expression"></a>Parti di un'espressione di percorso
 Un'espressione di percorso include due componenti.  
  
1.  La [modalità percorso](#PATHMODE) facoltativa, con valore **lax** o **strict**.  
  
2.  Il [percorso](#PATH) stesso.  

##  <a name="path-mode"></a><a name="PATHMODE"></a> Path mode  
 All'inizio dell'espressione di percorso, è possibile dichiarare la modalità percorso specificando la parola chiave **lax** o **strict**. Il valore predefinito è **lax**.  
  
-   Nella modalità **lax** la funzione restituisce valori vuoti se l'espressione di percorso contiene un errore. Se ad esempio si richiede il valore **$.name** e il testo JSON non contiene una chiave **name**, la funzione restituisce Null ma non genera un errore.  
  
-   Nella modalità **strict** la funzione genera un errore se l'espressione di percorso contiene un errore.  

La query seguente specifica in modo esplicito la modalità `lax` nell'espressione di percorso.

```sql  
DECLARE @json NVARCHAR(MAX);
SET @json=N'{ ... }';

SELECT * FROM OPENJSON(@json, N'lax $.info');
```  
  
##  <a name="path"></a><a name="PATH"></a> Path  
 Dopo la dichiarazione facoltativa della modalità percorso, specificare il percorso stesso.  
  
-   Il segno di dollaro (`$`) rappresenta l'elemento contesto.  
  
-   Il percorso proprietà è un insieme di passaggi di percorso. I passaggi di percorso possono contenere gli elementi e gli operatori seguenti.  
  
    -   Nomi delle chiavi. Ad esempio, `$.name` e `$."first name"`. Se il nome della chiave inizia con un segno di dollaro o contiene caratteri speciali quali spazi, racchiuderlo tra virgolette.   
  
    -   Elementi matrice. Ad esempio: `$.product[3]`. Le matrici sono in base zero.  
  
    -   L'operatore punto (`.`) indica un membro di un oggetto. Ad esempio, in `$.people[1].surname``surname` è figlio di `people`.
  
## <a name="examples"></a>Esempi  
 Gli esempi inclusi in questa sezione fanno riferimento al testo JSON seguente.  
  
```json  
{
    "people": [{
        "name": "John",
        "surname": "Doe"
    }, {
        "name": "Jane",
        "surname": null,
        "active": true
    }]
}
```  
  
 La tabella seguente illustra alcuni esempi di espressioni di percorso.  
  
|Espressione di percorso|Valore|  
|---------------------|-----------|  
|$.people[0].name|John|  
|$.people[1]|{ "name": "Jane",  "surname": null, "active": true }|  
|$.people[1].surname|Null|  
|$|{ "people": [ { "name": "John",  "surname": "Doe" },<br />   { "name": "Jane",  "surname": null, "active": true } ] }|  
  
## <a name="how-built-in-functions-handle-duplicate-paths"></a>Modalità di gestione dei percorsi duplicati da parte delle funzioni predefinite  
 Se il testo JSON contiene proprietà duplicate, ad esempio due chiavi con lo stesso nome sullo stesso livello, le funzioni **JSON_VALUE** e **JSON_QUERY** restituiscono solo il primo valore corrispondente al percorso. Per analizzare un oggetto JSON che contiene chiavi duplicate e restituire tutti i valori, usare **OPENJSON**, come illustrato nell'esempio seguente.  
  
```sql  
DECLARE @json NVARCHAR(MAX);
SET @json=N'{"person":{"info":{"name":"John", "name":"Jack"}}}';

SELECT value
  FROM OPENJSON(@json,'$.person.info');
```  

## <a name="learn-more-about-json-in-sql-server-and-azure-sql-database"></a>Altre informazioni su JSON in SQL Server e nel database SQL di Azure  
  
### <a name="microsoft-videos"></a>Video Microsoft

Per un'introduzione visiva al supporto JSON predefinito in SQL Server e nel database SQL di Azure, vedere i video seguenti:

-   [SQL Server 2016 and JSON Support](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support) (SQL Server 2016 e supporto JSON)

-   [Using JSON in SQL Server 2016 and Azure SQL Database](https://channel9.msdn.com/Shows/Data-Exposed/Using-JSON-in-SQL-Server-2016-and-Azure-SQL-Database) (Uso di JSON in SQL Server 2016 e nel database SQL di Azure)

-   [JSON as a bridge between NoSQL and relational worlds](https://channel9.msdn.com/events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds) (JSON come ponte tra NoSQL e gli ambienti relazionali)
  
## <a name="see-also"></a>Vedere anche  
 [OPENJSON &#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md)   
 [JSON_VALUE &#40;Transact-SQL&#41;](../../t-sql/functions/json-value-transact-sql.md)   
 [JSON_QUERY &#40;Transact-SQL&#41;](../../t-sql/functions/json-query-transact-sql.md)  
  
  
