---
title: Scrittura di istruzioni Transact-SQL internazionali | Microsoft Docs
ms.custom: ''
ms.date: 04/24/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- writing international statements
- Transact-SQL international considerations
- international considerations [SQL Server], Transact-SQL
- Database Engine international considerations [SQL Server], Transact-SQL
- statements [SQL Server], international
- database international considerations [SQL Server], Transact-SQL
- dates [SQL Server], international considerations
ms.assetid: f0b10fee-27f7-45fe-aece-ccc3f63bdcdb
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 20e587aeb7c0ed34762bf1f90488a06cafc0ec93
ms.sourcegitcommit: 0a4879dad09c6c42ad1ff717e4512cfea46820e9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/27/2019
ms.locfileid: "67412990"
---
# <a name="write-international-transact-sql-statements"></a>Scrittura di istruzioni Transact-SQL internazionali
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  Le linee guida seguenti consentono di aumentare il grado di portabilità tra lingue diverse, nonché il supporto di più lingue, per i database e le applicazioni di database che utilizzano istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] .  

-   A partire da [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] usare:
    -   I tipi di dati **char**, **varchar** e **varchar(max)** con le regole di confronto abilitate per [UTF-8](../../relational-databases/collations/collation-and-unicode-support.md#utf8).
    -   I tipi di dati **nchar**, **nvarchar** e **nvarchar(max)** con le regole di confronto abilitate per [caratteri supplementari](../../relational-databases/collations/collation-and-unicode-support.md#Supplementary_Characters).      

    In questo modo si evitano problemi di conversione della tabella codici. Per altre considerazioni, vedere [Differenze nell'archiviazione tra UTF-8 e UTF-16](../../relational-databases/collations/collation-and-unicode-support.md#storage_differences).  

-   Fino a [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] sostituire tutte le occorrenze dei tipi di dati **char**, **varchar** e **varchar(max)** con **nchar**, **nvarchar** e **nvarchar(max)** . In questo modo si evitano problemi di conversione della tabella codici. Per altre informazioni, vedere [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md). 
    > [!IMPORTANT]
    > Il tipo di dati **text** è deprecato e non deve essere usato in nuovi progetti di sviluppo. Pianificare la conversione dei dati **text** al tipo di dati **varchar(max)** .
  
-   Quando si eseguono confronti e operazioni con mesi o giorni della settimana, usare le parti numeriche della data invece delle stringhe di nomi. I nomi dei mesi e dei giorni della settimana restituiti variano a seconda dell'impostazione della lingua. Ad esempio, `DATENAME(MONTH,GETDATE())` restituisce `May` quando la lingua è impostata su inglese (Stati Uniti), `Mai` se è impostato il tedesco e `mai` se è impostato il francese. Specificare quindi una funzione quale [DATEPART](../../t-sql/functions/datepart-transact-sql.md) che usa il numero invece del nome del mese. Utilizzare i nomi DATEPART quando si compilano i set di risultati da visualizzare all'utente, in quanto le stringhe di nomi sono più significative delle parti numeriche. Non creare tuttavia il codice di logica che dipende dai nomi visualizzati di una lingua specifica.  
  
-   Quando si specificano le date nei confronti o nell'input di istruzioni INSERT e UPDATE, utilizzare costanti che vengono interpretate nello stesso modo indipendentemente dall'impostazione della lingua:  
  
    -   Le applicazioni ADO, OLE DB e ODBC devono utilizzare le clausole di escape seguenti relative a timestamp, data e ora:  
  
         **{ ts'** _aaaa_ **-** _mm_ **-** _gg_ _hh_ **:** _mm_ **:** _ss_ [ **.** _fff_] **'}** , ad esempio: **{ ts'1998-09-24 10:02:20'}**  
  
         **{ d'** _aaaa_ **-** _mm_ **-** _gg_ **'}** ad esempio: **{ d'1998-09-24'}**
  
         **{ t'** _hh_ **:** _mm_ **:** _ss_ **'}** ad esempio: **{ t'10:02:20'}**  
  
    -   Nelle applicazioni che utilizzano altre API, oppure script, stored procedure e trigger di [!INCLUDE[tsql](../../includes/tsql-md.md)] , è necessario utilizzare le stringhe numeriche non separate, Ad esempio, *aaaammgg* come 19980924.  
  
    -   Nelle applicazioni che usano altre API oppure script, stored procedure e trigger di [!INCLUDE[tsql](../../includes/tsql-md.md)] è anche possibile usare l'istruzione [CONVERT](../../t-sql/functions/cast-and-convert-transact-sql.md) con un parametro di stile esplicito per tutte le conversioni tra i tipi di dati **time**, **date**, **smalldate**, **datetime**, **datetime2** e **datetimeoffset** e i tipi di dati stringa di caratteri. L'istruzione seguente viene interpretata nello stesso modo indipendentemente dalle impostazioni di connessione della lingua o del formato della data:  
  
        ```sql  
        SELECT *  
        FROM AdventureWorks2012.Sales.SalesOrderHeader  
        WHERE OrderDate = CONVERT(DATETIME, '20060719', 101)  
        ```  
  
## <a name="see-also"></a>Vedere anche
[CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)     
[DATEPART &#40;Transact-SQL&#41;](../../t-sql/functions/datepart-transact-sql.md)        
[Regole di confronto e supporto Unicode](../../relational-databases/collations/collation-and-unicode-support.md)      
