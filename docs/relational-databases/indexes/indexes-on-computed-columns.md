---
title: Indici per le colonne calcolate | Microsoft Docs
ms.custom: ''
ms.date: 11/19/2018
ms.prod: sql
ms.prod_service: table-view-index, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- computed columns, index creation
- index creation [SQL Server], computed columns
- imprecise columns
- persisted computed columns
- precise [SQL Server]
ms.assetid: 8d17ac9c-f3af-4bbb-9cc1-5cf647e994c4
author: MikeRayMSFT
ms.author: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: cf54565115df53dc7d502f48aad68f9974adebd0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67909696"
---
# <a name="indexes-on-computed-columns"></a>Indici per le colonne calcolate
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

È possibile definire gli indici per le colonne calcolate purché siano soddisfatti i requisiti seguenti:  
  
-   Requisiti di proprietà  
-   Requisiti di determinismo  
-   Requisiti di precisione  
-   Requisiti del tipo di dati  
-   Requisiti dell'opzione SET  
  
#### <a name="ownership-requirements"></a>Requisiti di proprietà
  
Tutti i riferimenti a funzioni nella colonna calcolata devono avere lo stesso proprietario della tabella.  
  
## <a name="determinism-requirements"></a>Requisiti di determinismo  

Le espressioni sono deterministiche se restituiscono sempre lo stesso risultato per un determinato set di input. La proprietà **IsDeterministic** della funzione [COLUMNPROPERTY](../../t-sql/functions/columnproperty-transact-sql.md) indica se una *computed_column_expression* è deterministica.  
La *computed_column_expression* deve essere deterministica. Una *computed_column_expression* è deterministica quando sono soddisfatte tutte le condizioni seguenti:  
  
-   Tutte le funzioni alle quali l'espressione fa riferimento sono deterministiche e precise. Queste funzioni includono funzioni definite dall'utente e funzioni predefinite. Per altre informazioni, vedere [Funzioni deterministiche e non deterministiche](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md). Le funzioni potrebbero non essere precise se la colonna calcolata è PERSISTED. Per altre informazioni, vedere [Creazione di indici per colonne calcolate persistenti](#BKMK_persisted) più avanti in questo argomento.  
  
-   Tutte le colonne alle quali viene fatto riferimento nell'espressione appartengono alla tabella contenente la colonna calcolata.  
  
-   Nessun riferimento a una colonna estrae dati da più righe. Ad esempio, funzioni di aggregazione quali SUM o AVG dipendono dai dati presenti in più righe e renderebbero non deterministica una *computed_column_expression* .  
  
-   L'espressione *computed_column_expression* è priva di accesso ai dati di sistema o ai dati utente.  
  
Qualsiasi colonna calcolata contenente un'espressione CLR (Common Language Runtime) deve essere deterministica e contrassegnata come PERSISTED prima di poter essere indicizzata. Le espressioni di tipo CLR definito dall'utente sono consentite nelle definizioni delle colonne calcolate. Le colonne calcolate di tipo CLR definito dall'utente possono essere indicizzate purché il tipo sia confrontabile. Per altre informazioni, vedere [Tipi CLR definiti dall'utente](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md).  

#### <a name="cast-and-convert"></a>CAST e CONVERT

Quando si fa riferimento ai valori letterali stringa del tipo di dati relativo alla data in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], si consiglia di convertire in modo esplicito il valore letterale nel tipo di data che si desidera utilizzando uno stile di formato di data deterministico. Per un elenco degli stili del formato di data deterministici, vedere [CAST e CONVERT](../../t-sql/functions/cast-and-convert-transact-sql.md). 

Per altre informazioni, vedere [Conversione non deterministica di stringhe di valori letterali in valori DATE](../../t-sql/data-types/nondeterministic-convert-date-literals.md).

#### <a name="compatibility-level"></a>Livello di compatibilità

La conversione implicita dei dati di tipo carattere non Unicode tra regole di confronto viene considerata non deterministica, a meno che il livello di compatibilità non sia impostato su un valore minore o uguale a 80.  

Se l'impostazione del livello di compatibilità del database è 90, non è possibile creare indici su colonne calcolate contenenti tali espressioni. Tuttavia, le colonne calcolate esistenti che includono queste espressioni da un database aggiornato sono gestibili. Se si utilizzano colonne calcolate che includono conversioni implicite da valori di tipo stringa a valori di tipo data, verificare che le impostazioni LANGUAGE e DATEFORMAT siano consistenti nei database e nelle applicazioni per evitare l'eventuale danneggiamento dell'indice.

Il livello di compatibilità 90 corrisponde a SQL Server 2005.



## <a name="precision-requirements"></a>Requisiti di precisione
  
 La *computed_column_expression* deve essere precisa. Una *computed_column_expression* è precisa quando viene soddisfatta una o più delle condizioni seguenti:  
  
-   Non è un'espressione dei tipi di dati **float** o **real** .  
-   Nella definizione dell'espressione non viene usato il tipo di dati **float** o **real** . Ad esempio, nell'istruzione seguente la colonna `y` è di tipo **int** ed è deterministica, ma non precisa.  
  
    ```sql  
    CREATE TABLE t2 (a int, b int, c int, x float,   
       y AS CASE x   
             WHEN 0 THEN a   
             WHEN 1 THEN b   
             ELSE c   
          END);  
    ```  
  
> [!NOTE]  
> Le espressioni di tipo **float** o **real** sono considerate non precise e non possono essere usate come chiavi di un indice. Un'espressione **float** o **real** può essere usata in una vista indicizzata, ma non come chiave. Questa considerazione è valida anche per le colonne calcolate. Funzioni, espressioni oppure funzioni definite dall'utente sono considerate non precise se includono espressioni **float** o **real** . Sono comprese le espressioni logiche (confronti).  
  
La proprietà **IsPrecise** della funzione COLUMNPROPERTY indica se una *computed_column_expression* è precisa.  


## <a name="data-type-requirements"></a>Requisiti del tipo di dati
  
-   L'espressione *computed_column_expression* definita per la colonna calcolata non può restituire i tipi di dati **text**, **ntext**o **image** .  
-   Le colonne calcolate derivate dai tipi di dati **image**, **ntext**, **text**, **varchar(max)** , **nvarchar(max)** , **varbinary(max)** e **xml** possono essere indicizzate purché il tipo di dati della colonna calcolata sia consentito come colonna chiave dell'indice.  
-   Le colonne calcolate derivate dai tipi di dati **image**, **ntext**e **text** possono essere colonne non chiave (incluse) in un indice non cluster purché il tipo di dati della colonna calcolata sia consentito come colonna non chiave dell'indice.  


## <a name="set-option-requirements"></a>Requisiti dell'opzione SET
  
-   Quando viene eseguita l'istruzione CREATE TABLE o ALTER TABLE che definisce la colonna calcolata, è necessario impostare su ON l'opzione a livello di connessione ANSI_NULL. La funzione [OBJECTPROPERTY](../../t-sql/functions/objectproperty-transact-sql.md) indica se l'opzione è impostata su ON nella proprietà **IsAnsiNullsOn** .  
-   Per la connessione in corrispondenza della quale viene creato l'indice e per tutte le connessioni che tentano di eseguire istruzioni INSERT, UPDATE o DELETE che modificano i valori dell'indice, sei opzioni SET devono essere impostate su ON e un'opzione SET deve essere impostata su OFF. Per tutte le eventuali istruzioni SELECT eseguite da una connessione per la quale non sono state definite esattamente le impostazioni delle opzioni indicate di seguito, Query Optimizer ignora gli indici definiti su una colonna calcolata.  
  
    -   L'opzione NUMERIC_ROUNDABORT deve essere impostata su OFF e le opzioni seguenti su ON.  
    -   ANSI_NULLS  
    -   ANSI_PADDING  
    -   ANSI_WARNINGS  
    -   ARITHABORT  
    -   CONCAT_NULL_YIELDS_NULL  
    -   QUOTED_IDENTIFIER  
  
> [!NOTE]
> Quando il livello di compatibilità del database è impostato su 90 o su un valore maggiore, l'impostazione di ANSI_WARNINGS su ON comporta anche l'impostazione implicita di ARITHABORT su ON.  
  
## <a name="BKMK_persisted"></a> Creazione di indici per colonne calcolate persistenti  

In alcuni casi è possibile creare una colonna calcolata definita con un'espressione che pur essendo deterministica risulta imprecisa. È possibile farlo quando la colonna è contrassegnata come PERSISTED nell'istruzione CREATE TABLE o ALTER TABLE.

Questo significa che [!INCLUDE[ssDE](../../includes/ssde-md.md)] archivia i valori calcolati nella tabella e li aggiorna quando vengono aggiornate altre colonne da cui dipende la colonna calcolata. [!INCLUDE[ssDE](../../includes/ssde-md.md)] utilizza questi valori persistenti quando crea un indice sulla colonna e quando viene fatto riferimento all'indice all'interno di una query.

Questa opzione consente di creare un indice in una colonna calcolata quando [!INCLUDE[ssDE](../../includes/ssde-md.md)] non è in grado di verificare esattamente se una funzione che restituisce espressioni di colonne calcolate, in particolare una funzione CLR creata in [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], sia deterministica e precisa.  


  
## <a name="related-content"></a>Contenuto correlato  
 [COLUMNPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/columnproperty-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)    
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)
  
  
