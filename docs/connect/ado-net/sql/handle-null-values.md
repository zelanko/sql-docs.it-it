---
title: Gestione dei valori NULL
description: Viene illustrato come utilizzare i valori GUID e uniqueidentifier in SQL Server e .NET.
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: f18b288f-b265-4bbe-957f-c6833c0645ef
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 6ae2bc8d816dd2bc32572447483dacd76dd967f0
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452192"
---
# <a name="handling-null-values"></a>Gestione dei valori NULL

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[Scaricare ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

Se il valore di una colonna è sconosciuto o mancante, viene utilizzato un valore null in un database relazionale. Un valore null non è né una stringa vuota (per i tipi di dati character o DateTime) né un valore zero (per i tipi di dati numerici). La specifica ANSI SQL-92 indica che un valore null deve essere lo stesso per tutti i tipi di dati, in modo che tutti i valori null vengano gestiti in modo coerente. Lo spazio dei nomi <xref:System.Data.SqlTypes> fornisce la semantica null implementando l'interfaccia <xref:System.Data.SqlTypes.INullable>. Ognuno dei tipi di dati in <xref:System.Data.SqlTypes> dispone di una propria proprietà `IsNull` e di un valore `Null` che può essere assegnato a un'istanza di tale tipo di dati.  
  
> [!NOTE]
>  Nel .NET Framework versione 2,0 e .NET Core versione 1,0 è stato introdotto il supporto per i tipi nullable, che consentono ai programmatori di estendere un tipo di valore per rappresentare tutti i valori del tipo sottostante. Questi tipi CLR Nullable rappresentano un'istanza della struttura <xref:System.Nullable>. Questa funzionalità è particolarmente utile quando i tipi di valore sono boxed e unboxed, garantendo una maggiore compatibilità con i tipi di oggetto. I tipi CLR Nullable non sono destinati all'archiviazione di valori null di database perché un valore Null ANSI SQL non si comporta in modo analogo a un riferimento `null` (o `Nothing` in Visual Basic). Per l'utilizzo di valori null SQL ANSI del database, utilizzare <xref:System.Data.SqlTypes> valori null anziché <xref:System.Nullable>. Per ulteriori informazioni sull'utilizzo dei tipi nullable CLR in C# , vedere [tipi nullable](https://docs.microsoft.com/dotnet/csharp/programming-guide/nullable-types/)e per C# vedere [utilizzo di tipi nullable](https://docs.microsoft.com/dotnet/csharp/programming-guide/nullable-types/using-nullable-types/).  
  
## <a name="nulls-and-three-valued-logic"></a>Valori null e logica a tre valori  
Consentire valori null nelle definizioni di colonna introduce una logica a tre valori nell'applicazione. Un confronto può restituire una delle tre condizioni seguenti:  
  
- True  
  
- False  
  
- Unknown  
  
Poiché il valore null è considerato sconosciuto, due valori null confrontati tra loro non sono considerati uguali. Nelle espressioni che usano operatori aritmetici, se uno degli operandi è null, anche il risultato è null.  
  
## <a name="nulls-and-sqlboolean"></a>Valori null e SqlBoolean  
Il confronto tra qualsiasi <xref:System.Data.SqlTypes> restituirà una <xref:System.Data.SqlTypes.SqlBoolean>. La funzione `IsNull` per ogni `SqlType` restituisce un <xref:System.Data.SqlTypes.SqlBoolean> e può essere usata per verificare la presenza di valori null. Le tabelle di verità seguenti illustrano la funzione degli operatori AND, OR e NOT in presenza di un valore null. (T = true, F = false e U = Unknown o null).  
  
![Tabella Truth](../media/truthtable-bpuedev11.gif "|::ref1::|")  
  
### <a name="understanding-the-ansi_nulls-option"></a>Informazioni sull'opzione ANSI_NULLS  
<xref:System.Data.SqlTypes> fornisce la stessa semantica di quando l'opzione ANSI_NULLS è impostata su on SQL Server. Tutti gli operatori aritmetici (+, -, *, /, %), gli operatori bit per bit (~, &, &#124;) e la maggior parte delle funzioni restituiscono Null se uno degli operandi o degli argomenti è Null, ad eccezione della proprietà `IsNull`.  
  
Lo standard ANSI SQL-92 non supporta *columnName* = NULL in una clausola WHERE. In SQL Server, l'opzione ANSI_NULLS controlla sia il supporto di valori null predefinito nel database sia la valutazione dei confronti con i valori null. Se ANSI_NULLS è attivato (impostazione predefinita), è necessario utilizzare l'operatore IS NULL nelle espressioni quando si verificano valori null. Ad esempio, se l'opzione ANSI_NULLS è impostata su ON, il confronto seguente restituisce sempre UNKNOWN:  
  
```console
colname > NULL  
```  
  
Il confronto con una variabile che contiene un valore null restituisce anche Unknown:  
  
```console
colname > @MyVariable  
```  
  
Per verificare la presenza di un valore Null, usare il predicato IS NULL o IS NOT NULL. La clausola WHERE potrebbe risultare in tal modo più complessa. Ad esempio, la colonna TerritoryID nella tabella Customer di AdventureWorks consente valori null. Un'istruzione SELECT che oltre ad altri valori deve verificare i valori Null deve includere il predicato IS NULL:  
  
```sql
SELECT CustomerID, AccountNumber, TerritoryID  
FROM AdventureWorks.Sales.Customer  
WHERE TerritoryID IN (1, 2, 3)  
   OR TerritoryID IS NULL  
```  
  
Se si imposta ANSI_NULLS OFF in SQL Server, è possibile creare espressioni che usano l'operatore di uguaglianza per eseguire il confronto con il valore null. Tuttavia, non è possibile impedire a diverse connessioni di impostare opzioni null per tale connessione. L'utilizzo di è NULL per verificare se i valori null funzionano sempre, indipendentemente dalle impostazioni ANSI_NULLS per una connessione.  
  
L'impostazione di ANSI_NULLS OFF non è supportata in un `DataSet`, che segue sempre lo standard ANSI SQL-92 per la gestione dei valori null in <xref:System.Data.SqlTypes>.  
  
## <a name="assigning-null-values"></a>Assegnazione di valori null  
I valori null sono speciali e la relativa semantica di archiviazione e assegnazione differisce tra sistemi di tipi e sistemi di archiviazione diversi. Un `Dataset` è progettato per essere utilizzato con sistemi di archiviazione e tipi diversi.  
  
In questa sezione viene descritta la semantica null per l'assegnazione di valori null a un <xref:System.Data.DataColumn> in un <xref:System.Data.DataRow> tra i diversi sistemi di tipi.  
  
`DBNull.Value`  
Questa assegnazione è valida per un `DataColumn` di qualsiasi tipo. Se il tipo implementa `INullable`, `DBNull.Value` viene assegnato al valore null fortemente tipizzato appropriato.  
  
`SqlType.Null`  
Tutti i tipi di dati <xref:System.Data.SqlTypes> implementano `INullable`. Se il valore null fortemente tipizzato può essere convertito nel tipo di dati della colonna utilizzando gli operatori di cast impliciti, l'assegnazione verrà superata. In caso contrario, viene generata un'eccezione cast non valida.  
  
`null`  
Se ' null ' è un valore valido per il tipo di dati `DataColumn` specificato, viene assegnato all'`DbNull.Value` o `Null` appropriato associato al tipo di `INullable` (`SqlType.Null`)  
  
`derivedUdt.Null`  
Per le colonne con tipo definito dall'utente, i valori null vengono sempre archiviati in base al tipo associato all'`DataColumn`. Si consideri il caso di un tipo definito dall'utente associato a un `DataColumn` che non implementa `INullable` mentre la relativa sottoclasse. In questo caso, se viene assegnato un valore null fortemente tipizzato associato alla classe derivata, viene archiviato come `DbNull.Value` non tipizzato, perché l'archiviazione null è sempre coerente con il tipo di dati di DataColumn.  
  
> [!NOTE]
>  La struttura di `Nullable<T>` o <xref:System.Nullable> non è attualmente supportata nella `DataSet`.  
  
### <a name="multiple-column-row-assignment"></a>Assegnazione di più colonne (riga)  
`DataTable.Add`, `DataTable.LoadDataRow` o altre API che accettano un <xref:System.Data.DataRow.ItemArray%2A> di cui viene eseguito il mapping a una riga, mappano ' null ' al valore predefinito di DataColumn. Se un oggetto nella matrice contiene `DbNull.Value` o la relativa controparte fortemente tipizzata, vengono applicate le stesse regole descritte in precedenza.  
  
Per un'istanza di assegnazioni di valori Null di `DataRow.["columnName"]` si applicano inoltre le regole seguenti:  
  
- Il valore predefinito *default* è `DbNull.Value` per tutte le colonne ad eccezione di quelle Null fortemente tipizzate, alle quali si applica il valore Null fortemente tipizzato appropriato.  
  
- I valori null non vengono mai scritti durante la serializzazione in file XML (come in "xsi: nil").  
  
- Tutti i valori non null, incluse le impostazioni predefinite, vengono sempre scritti durante la serializzazione in XML. A differenza della semantica XSD/XML in cui un valore null (xsi: nil) è esplicito e il valore predefinito è implicito (se non è presente in XML, un parser di convalida può ottenerlo da uno schema XSD associato). Il contrario è true per un `DataTable`: un valore null è implicito e il valore predefinito è Explicit.  
  
- A tutti i valori di colonna mancanti per le righe lette dall'input XML viene assegnato un valore NULL. Alle righe create con <xref:System.Data.DataTable.NewRow%2A> o a metodi simili viene assegnato il valore predefinito di DataColumn.  
  
- Il metodo <xref:System.Data.DataRow.IsNull%2A> restituisce `true` sia per `DbNull.Value` che per `INullable.Null`.  
  
## <a name="assigning-null-values"></a>Assegnazione di valori null  
Il valore predefinito per qualsiasi istanza di <xref:System.Data.SqlTypes> è null.  
  
I valori null in <xref:System.Data.SqlTypes> sono specifici del tipo e non possono essere rappresentati da un singolo valore, ad esempio `DbNull`. Utilizzare la proprietà `IsNull` per verificare la presenza di valori null.  
  
È possibile assegnare valori null a un <xref:System.Data.DataColumn> come illustrato nell'esempio di codice seguente. È possibile assegnare direttamente valori null a `SqlTypes` variabili senza generare un'eccezione.  
  
### <a name="example"></a>Esempio  
Nell'esempio di codice seguente viene creato un <xref:System.Data.DataTable> con due colonne definite come <xref:System.Data.SqlTypes.SqlInt32> e <xref:System.Data.SqlTypes.SqlString>. Il codice aggiunge una riga di valori noti, una riga di valori null e quindi scorre la <xref:System.Data.DataTable>, assegnando i valori alle variabili e visualizzando l'output nella finestra della console.  
  
[!code-csharp[DataWorks SqlInt32_IsNull#1](~/../sqlclient/doc/samples/SqlInt32_IsNull.cs#1)]
  
In questo esempio vengono visualizzati i risultati seguenti:  
  
```console
isColumnNull=False, ID=123, Description=Side Mirror  
isColumnNull=True, ID=Null, Description=Null  
```  
  
## <a name="comparing-null-values-with-sqltypes-and-clr-types"></a>Confronto di valori null con SqlTypes e tipi CLR  
Quando si confrontano i valori null, è importante comprendere la differenza tra il modo in cui il metodo `Equals` valuta i valori null in <xref:System.Data.SqlTypes> rispetto al modo in cui funziona con i tipi CLR. Tutti i metodi di `Equals` <xref:System.Data.SqlTypes> utilizzano la semantica del database per valutare i valori null: se uno o entrambi i valori sono null, il confronto restituisce null. D'altra parte, l'utilizzo del metodo CLR `Equals` su due <xref:System.Data.SqlTypes> produrrà true se entrambi i valori sono null. Ciò riflette la differenza tra l'utilizzo di un metodo di istanza, ad esempio il metodo CLR `String.Equals` e l'utilizzo del metodo statico/condiviso `SqlString.Equals`.  
  
Nell'esempio seguente viene illustrata la differenza nei risultati tra il metodo `SqlString.Equals` e il metodo `String.Equals` quando a ogni viene passata una coppia di valori null e quindi una coppia di stringhe vuote.  
  
[!code-csharp[DataWorks SqlString_Equals#1](~/../sqlclient/doc/samples/SqlString_Equals.cs#1)]
  
Il codice produce l'output seguente:  
  
```console
SqlString.Equals shared/static method:  
  Two nulls=Null  
  
String.Equals instance method:  
  Two nulls=True  
  
SqlString.Equals shared/static method:  
  Two empty strings=True  
  
String.Equals instance method:  
  Two empty strings=True   
```  
  
## <a name="next-steps"></a>Passaggi successivi
- [Tipi di dati SQL Server e ADO.NET](sql-server-data-types.md)
