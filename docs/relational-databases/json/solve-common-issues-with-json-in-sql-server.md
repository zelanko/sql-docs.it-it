---
description: Risolvere i problemi comuni di JSON in SQL Server
title: Risolvere i problemi comuni di JSON in SQL Server
ms.date: 06/03/2020
ms.prod: sql
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- JSON, FAQ
ms.assetid: feae120b-55cc-4601-a811-278ef1c551f9
author: jovanpop-msft
ms.author: jovanpop
ms.reviewer: jroth
ms.custom: seo-dt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 3d898f2e0c61b0775d9094580e319640f2aeadf2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88490903"
---
# <a name="solve-common-issues-with-json-in-sql-server"></a>Risolvere i problemi comuni di JSON in SQL Server
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

 In questo articolo sono contenute le risposte ad alcune domande comuni sul supporto JSON integrato in SQL Server.  
 
## <a name="for-json-and-json-output"></a>Output di FOR JSON e JSON

### <a name="for-json-path-or-for-json-auto"></a>FOR JSON PATH o FOR JSON AUTO?  
 **Domanda.** Si desidera creare un risultato di testo JSON da una semplice query SQL su una singola tabella. FOR JSON PATH e FOR JSON AUTO producono lo stesso output. Quali di queste due opzioni deve essere usata?  
  
 **Risposta.** Usare FOR JSON PATH. Anche se non esiste alcuna differenza nell'output JSON, la modalità AUTO dispone di una logica aggiuntiva che controlla se le colonne devono essere nidificate. Considerare PATH come opzione predefinita.  

### <a name="create-a-nested-json-structure"></a>Creare una struttura JSON nidificata  
 **Domanda.** Si desidera produrre una struttura JSON complessa con numerose matrici sullo stesso livello. FOR JSON PATH è in grado di creare oggetti nidificati usando percorsi e FOR JSON AUTO crea livelli di nidificazione aggiuntivi per ciascuna tabella. Nessuna di queste due opzioni consente di generare l'output desiderato. Come è possibile creare un formato JSON personalizzato che le opzioni esistenti non supportano direttamente?  
  
 **Risposta.** È possibile creare qualsiasi struttura dei dati aggiungendo query FOR JSON come espressioni di colonna che restituiscono testo JSON. È anche possibile creare manualmente JSON tramite la funzione JSON_QUERY. Queste tecniche vengono illustrate nell'esempio seguente.  
  
```sql  
SELECT col1, col2, col3,  
     (SELECT col11, col12, col13 FROM t11 WHERE t11.FK = t1.PK FOR JSON PATH) as t11,  
     (SELECT col21, col22, col23 FROM t21 WHERE t21.FK = t1.PK FOR JSON PATH) as t21,  
     (SELECT col31, col32, col33 FROM t31 WHERE t31.FK = t1.PK FOR JSON PATH) as t31,  
     JSON_QUERY('{"'+col4'":"'+col5+'"}') as t41  
FROM t1  
FOR JSON PATH  
```  
  
Ogni risultato di una query FOR JSON o della funzione JSON_QUERY nelle espressioni di colonna è formattato come un oggetto secondario JSON nidificato a parte e incluso nel risultato principale.  

### <a name="prevent-double-escaped-json-in-for-json-output"></a>Evitare JSON con doppi caratteri di escape nell'output FOR JSON  
 **Domanda.** Il testo JSON è archiviato in una colonna di tabella. Si desidera includerlo nell'output di FOR JSON. Tuttavia, FOR JSON usa caratteri di escape per tutti i caratteri nel file JSON, quindi si ottiene una stringa JSON anziché un oggetto nidificato, come illustrato nell'esempio seguente.  
  
```sql  
SELECT 'Text' AS myText, '{"day":23}' AS myJson  
FOR JSON PATH  
```  
  
 Questa query produce l'output riportato di seguito.  
  
```json  
[{"myText":"Text", "myJson":"{\"day\":23}"}]  
```  
  
 Come è possibile evitare questo comportamento? Si desidera che `{"day":23}` venga restituito come oggetto JSON e non come testo con caratteri di escape.  
  
 **Risposta.** L'oggetto JSON archiviato in una colonna di testo o in un valore letterale viene trattato come qualsiasi testo. Ovvero, è racchiuso tra virgolette doppie e caratteri di escape. Se si desidera restituire un oggetto JSON senza caratteri di escape, passare la colonna JSON come argomento alla funzione JSON_QUERY, come illustrato nell'esempio seguente.  
  
```sql  
SELECT col1, col2, col3, JSON_QUERY(jsoncol1) AS jsoncol1  
FROM tab1  
FOR JSON PATH  
```  
  
 JSON_QUERY, senza il secondo parametro facoltativo, restituisce il primo argomento come risultato. Poiché JSON_QUERY restituisce sempre un oggetto JSON valido, FOR JSON sa che questo risultato non deve essere preceduto da caratteri di escape.

### <a name="json-generated-with-the-without_array_wrapper-clause-is-escaped-in-for-json-output"></a>JSON generato con la clausola WITHOUT_ARRAY_WRAPPER viene preceduto da caratteri di escape nell'output FOR JSON  
 **Domanda.** Si tenta di formattare un'espressione di colonna con FOR JSON e l'opzione WITHOUT_ARRAY_WRAPPER.  
  
```sql  
SELECT 'Text' as myText,  
   (SELECT 12 day, 8 mon FOR JSON PATH, WITHOUT_ARRAY_WRAPPER) as myJson  
FOR JSON PATH   
```  
  
 Sembra che il testo restituito dalla query FOR JSON sia preceduto da caratteri di escape come testo normale. Ciò si verifica solo se la clausola WITHOUT_ARRAY_WRAPPER è specificata. Perché non viene trattato come un oggetto JSON e incluso senza caratteri di escape nel risultato?  
  
 **Risposta.** Se si specifica l'opzione `WITHOUT_ARRAY_WRAPPER` nella query `FOR JSON` interna, il testo JSON risultante non è necessariamente JSON valido. Pertanto la query `FOR JSON` esterna presuppone che si tratti di testo normale e usa caratteri di escape per la stringa. Se si è certi che l'output JSON sia valido, eseguirne il wrapping con la funzione `JSON_QUERY` per convertirlo in oggetto JSON formattato correttamente, come illustrato nell'esempio seguente.  
  
```sql  
SELECT 'Text' as myText,  
      JSON_QUERY((SELECT 12 day, 8 mon FOR JSON PATH, WITHOUT_ARRAY_WRAPPER)) as myJson  
FOR JSON PATH    
```  

## <a name="openjson-and-json-input"></a>Input di OPENJSON e JSON

### <a name="return-a-nested-json-sub-object-from-json-text-with-openjson"></a>Restituire l'oggetto secondario JSON nidificato dal testo JSON con OPENJSON  
 **Domanda.** Non è possibile aprire una matrice di oggetti JSON complessi che contiene sia valori scalari sia oggetti, e matrici usando OPENJSON con uno schema esplicito. Quando si aggiunge un riferimento a una chiave nella clausola WITH, vengono restituiti solo i valori scalari. Oggetti e matrici vengono restituiti come valori null. Come è possibile estrarre oggetti o matrici come oggetti JSON?  
  
 **Risposta.** Se si desidera restituire un oggetto o una matrice come colonna, usare l'opzione AS JSON nella definizione di colonna, come illustrato nell'esempio seguente.  
  
```sql  
SELECT scalar1, scalar2, obj1, obj2, arr1  
FROM OPENJSON(@json)  
    WITH ( scalar1 int,  
        scalar2 datetime2,  
        obj1 NVARCHAR(MAX) AS JSON,  
        obj2 NVARCHAR(MAX) AS JSON,  
        arr1 NVARCHAR(MAX) AS JSON)  
```  

### <a name="return-long-text-value-with-openjson-instead-of-json_value"></a>Restituire il valore di testo lungo con OPENJSON anziché JSON_VALUE
 **Domanda.** La chiave di descrizione nel testo JSON contiene testo lungo. `JSON_VALUE(@json, '$.description')` restituisce NULL anziché un valore.  
  
 **Risposta.** JSON_VALUE è progettato per restituire valori scalari piccoli. In genere la funzione restituisce NULL anziché un errore di overflow. Se si desidera restituire valori più lunghi, usare OPENJSON, che supporta valori NVARCHAR (MAX), come illustrato nell'esempio seguente.  
  
```sql  
SELECT myText FROM OPENJSON(@json) WITH (myText NVARCHAR(MAX) '$.description')  
```  

### <a name="handle-duplicate-keys-with-openjson-instead-of-json_value"></a>Gestire chiavi duplicate con OPENJSON anziché con JSON_VALUE
 **Domanda.** Il testo JSON contiene chiavi duplicate. JSON_VALUE restituisce solo la prima chiave trovata nel percorso. Come è possibile visualizzare tutte le chiavi con lo stesso nome?  
  
 **Risposta.** Le funzioni scalari JSON integrate restituiscono solo la prima occorrenza dell'oggetto di riferimento. Se è necessaria più di una chiave, usare la funzione con valori di tabella OPENJSON, come illustrato nell'esempio seguente.  
  
```sql  
SELECT value FROM OPENJSON(@json, '$.info.settings')  
WHERE [key] = 'color'  
```  

### <a name="openjson-requires-compatibility-level-130"></a>OPENJSON richiede il livello di compatibilità 130  
 **Domanda.** È in corso un tentativo di esecuzione di OPENJSON in SQL Server 2016 e viene visualizzato l'errore riportato di seguito.  
  
 `Msg 208, Level 16, State 1 'Invalid object name OPENJSON'`  
  
 **Risposta.** La funzione OPENJSON è disponibile solo nel livello di compatibilità 130. Se il livello di compatibilità del database è inferiore a 130, la funzione OPENJSON è nascosta. Altre funzioni JSON sono disponibili in tutti i livelli di compatibilità.  
 
## <a name="other-questions"></a>Altre domande

### <a name="reference-keys-that-contain-non-alphanumeric-characters-in-json-text"></a>Aggiungere il riferimento alle chiavi che contengono caratteri non alfanumerici nel testo JSON  
 **Domanda.** Le chiavi del testo JSON contengono caratteri non alfanumerici. Come è possibile aggiungere un riferimento a queste proprietà?  
  
 **Risposta.** È necessario racchiuderle tra virgolette nei percorsi JSON. Ad esempio: `JSON_VALUE(@json, '$."$info"."First Name".value')`.
 
## <a name="learn-more-about-json-in-sql-server-and-azure-sql-database"></a>Altre informazioni su JSON in SQL Server e nel database SQL di Azure  
  
### <a name="microsoft-videos"></a>Video Microsoft

Per un'introduzione visiva al supporto JSON predefinito in SQL Server e nel database SQL di Azure, vedere i video seguenti:

-   [SQL Server 2016 and JSON Support](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support) (SQL Server 2016 e supporto JSON)

-   [Using JSON in SQL Server 2016 and Azure SQL Database](https://channel9.msdn.com/Shows/Data-Exposed/Using-JSON-in-SQL-Server-2016-and-Azure-SQL-Database) (Uso di JSON in SQL Server 2016 e nel database SQL di Azure)

-   [JSON as a bridge between NoSQL and relational worlds](https://channel9.msdn.com/events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds) (JSON come ponte tra NoSQL e gli ambienti relazionali)
