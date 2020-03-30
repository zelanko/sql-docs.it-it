---
title: Gestione dei valori NULL
description: Viene illustrato come usare i valori GUID e uniqueidentifier in SQL Server e .NET.
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: f18b288f-b265-4bbe-957f-c6833c0645ef
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: 2bcd54ab83429b1f7961480210c12eb546a2aa70
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "78896730"
---
# <a name="handling-null-values"></a>Gestione dei valori NULL

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

Se il valore di una colonna è sconosciuto o mancante, viene usato un valore Null in un database relazionale. Un valore Null non è né una stringa vuota (per i tipi di dati character o datetime) né un valore zero (per i tipi di dati numerici). La specifica ANSI SQL-92 indica che un valore Null deve essere lo stesso per tutti i tipi di dati, in modo che tutti i valori Null vengano gestiti in modo coerente. Lo spazio dei nomi <xref:System.Data.SqlTypes> specifica la semantica Null implementando l'interfaccia <xref:System.Data.SqlTypes.INullable>. Ogni tipo di dati in <xref:System.Data.SqlTypes> ha una propria proprietà `IsNull` e un valore `Null` che può essere assegnato a un'istanza di tale tipo di dati.  
  
> [!NOTE]
>  In .NET Framework versione 2.0 e .NET Core versione 1.0 è stato introdotto il supporto per i tipi nullable, che consentono ai programmatori di estendere un tipo di valore per rappresentare tutti i valori del tipo sottostante. I tipi nullable CLR rappresentano un'istanza della struttura <xref:System.Nullable>. Questa funzionalità è particolarmente utile quando i tipi di valore sono boxed e unboxed, garantendo una maggiore compatibilità con i tipi di oggetto. I tipi nullable CLR non sono destinati all'archiviazione dei valori Null del database perché un valore Null ANSI SQL non si comporta in modo analogo a un riferimento `null` (o `Nothing` in Visual Basic). Per usufruire dei valori Null SQL ANSI del database, usare valori Null <xref:System.Data.SqlTypes> anziché <xref:System.Nullable>. Per altre informazioni sull'uso di tipi nullable CLR in C#, vedere [Tipi nullable](https://docs.microsoft.com/dotnet/csharp/programming-guide/nullable-types/) e per C# vedere [Utilizzo dei tipi nullable](https://docs.microsoft.com/dotnet/csharp/programming-guide/nullable-types/using-nullable-types/).  
  
## <a name="nulls-and-three-valued-logic"></a>Valori Null e logica a tre valori  
Consentendo i valori Null nelle definizioni di colonna si introduce una logica a tre valori nell'applicazione. Un confronto può restituire una delle tre condizioni seguenti:  
  
- True  
  
- False  
  
- Unknown  
  
Poiché il valore Null è considerato sconosciuto, due valori Null confrontati tra loro non sono considerati uguali. Nelle espressioni che usano operatori aritmetici, se uno degli operandi è Null, anche il risultato è Null.  
  
## <a name="nulls-and-sqlboolean"></a>Valori Null e SqlBoolean  
Il confronto tra qualsiasi <xref:System.Data.SqlTypes> restituisce un elemento <xref:System.Data.SqlTypes.SqlBoolean>. La funzione `IsNull` per ogni `SqlType` restituisce un elemento <xref:System.Data.SqlTypes.SqlBoolean> e può essere usata per verificare la presenza di valori Null. Le seguenti tabelle di veridicità illustrano la funzione degli operatori AND, OR e NOT in presenza di un valore Null. (T=true, F=false e U=unknown o Null)  
  
![Tabella Truth](../media/truthtable-bpuedev11.gif "TruthTable_bpuedev11")  
  
### <a name="understanding-the-ansi_nulls-option"></a>Informazioni sull'opzione ANSI_NULLS  
<xref:System.Data.SqlTypes> offre la stessa semantica di quando si imposta l'opzione ANSI_NULLS in SQL Server. Tutti gli operatori aritmetici (+, -, *, /, %), gli operatori bit per bit (~, &, &#124;) e la maggior parte delle funzioni restituiscono Null se uno degli operandi o degli argomenti è Null, ad eccezione della proprietà `IsNull`.  
  
Lo standard ANSI SQL-92 non supporta *columnName* = NULL in una clausola WHERE. In SQL Server l'opzione ANSI_NULLS controlla sia il supporto di valori Null predefinito nel database, sia la valutazione dei confronti con i valori Null. Se l'opzione ANSI_NULLS è attivata (impostazione predefinita), è necessario usare l'operatore IS NULL nelle espressioni quando si effettuano test dei valori Null. Ad esempio, se l'opzione ANSI_NULLS è impostata su ON, il confronto seguente restituisce sempre UNKNOWN:  
  
```console
colname > NULL  
```  
  
Il confronto con una variabile che contiene un valore Null restituisce anche Unknown:  
  
```console
colname > @MyVariable  
```  
  
Per verificare la presenza di un valore Null, usare il predicato IS NULL o IS NOT NULL. La clausola WHERE potrebbe risultare in tal modo più complessa. Ad esempio, la colonna TerritoryID nella tabella Customer di AdventureWorks consente i valori Null. Un'istruzione SELECT che oltre ad altri valori deve verificare i valori Null deve includere il predicato IS NULL:  
  
```sql
SELECT CustomerID, AccountNumber, TerritoryID  
FROM AdventureWorks.Sales.Customer  
WHERE TerritoryID IN (1, 2, 3)  
   OR TerritoryID IS NULL  
```  
  
Se si imposta ANSI_NULLS come disattivata in SQL Server, è possibile creare espressioni che usano l'operatore di uguaglianza per eseguire il confronto con il valore Null. Tuttavia, non è possibile impedire a diverse connessioni di impostare opzioni Null per tale connessione. L'uso di IS NULL per testare i valori Null funziona sempre, indipendentemente dalle impostazioni di ANSI_NULLS per una connessione.  
  
L'impostazione di ANSI_NULLS come disattivata non è supportata in un oggetto `DataSet`, che segue sempre lo standard ANSI SQL-92 per la gestione dei valori Null in <xref:System.Data.SqlTypes>.  
  
## <a name="assigning-null-values"></a>Assegnazione di valori Null  
I valori Null sono speciali e la relativa semantica di archiviazione e assegnazione varia tra sistemi di tipi e sistemi di archiviazione diversi. Un oggetto `Dataset` è progettato per essere usato con sistemi di tipi e di archiviazione diversi.  
  
In questa sezione viene descritta la semantica Null per l'assegnazione di valori Null a un <xref:System.Data.DataColumn> in un <xref:System.Data.DataRow> nei diversi sistemi di tipi.  
  
`DBNull.Value`  
Questa assegnazione è valida per un `DataColumn` di qualsiasi tipo. Se il tipo implementa `INullable`, `DBNull.Value` viene assegnato forzatamente al valore Null fortemente tipizzato appropriato.  
  
`SqlType.Null`  
Tutti i tipi di dati <xref:System.Data.SqlTypes> implementano `INullable`. Se il valore Null fortemente tipizzato può essere convertito nel tipo di dati della colonna usando gli operatori di cast impliciti, l'assegnazione ha esito positivo. In caso contrario, viene generata un'eccezione di cast non valido.  
  
`null`  
Se "null" è un valore valido per il tipo di dati `DataColumn` specificato, viene assegnato forzatamente all'oggetto `DbNull.Value` o `Null` appropriato associato al tipo `INullable` (`SqlType.Null`)  
  
`derivedUdt.Null`  
Per le colonne con tipo definito dall'utente (UDT), i valori Null vengono sempre archiviati in base al tipo associato a `DataColumn`. Si consideri il caso di un UDT associato a un `DataColumn` che non implementa un elemento `INullable` mentre la relativa sottoclasse lo implementa. In questo caso, se viene assegnato un valore Null fortemente tipizzato associato alla classe derivata, viene archiviato come `DbNull.Value` non tipizzato, perché l'archiviazione Null è sempre coerente con il tipo di dati di DataColumn.  
  
> [!NOTE]
>  La struttura di `Nullable<T>` o <xref:System.Nullable> non è attualmente supportata in `DataSet`.  
  
### <a name="multiple-column-row-assignment"></a>Assegnazione di più colonne (righe)  
`DataTable.Add`, `DataTable.LoadDataRow` o altre API che accettano un elemento <xref:System.Data.DataRow.ItemArray%2A> che viene mappato a una riga, eseguono il mapping di "null" al valore predefinito di DataColumn. Se un oggetto nella matrice contiene `DbNull.Value` o la relativa controparte fortemente tipizzata, vengono applicate le stesse regole descritte sopra.  
  
Per un'istanza di assegnazioni di valori Null di `DataRow.["columnName"]` si applicano inoltre le regole seguenti:  
  
- Il valore predefinito *default* è `DbNull.Value` per tutte le colonne ad eccezione di quelle Null fortemente tipizzate, alle quali si applica il valore Null fortemente tipizzato appropriato.  
  
- I valori Null non vengono mai scritti durante la serializzazione nei file XML (come in "xsi:nil").  
  
- Tutti i valori non Null, incluse le impostazioni predefinite, vengono sempre scritti durante la serializzazione in XML, a differenza della semantica XSD/XML in cui un valore Null (xsi:nil) è esplicito e il valore predefinito è implicito (se non è presente in XML, un parser di convalida può ottenerlo da uno schema XSD associato). Per un oggetto `DataTable` è vero il contrario: un valore Null è implicito e il valore predefinito è esplicito.  
  
- A tutti i valori di colonna mancanti per le righe lette dall'input XML viene assegnato NULL. Alle righe create con <xref:System.Data.DataTable.NewRow%2A> o metodi simili viene assegnato il valore predefinito di DataColumn.  
  
- Il metodo <xref:System.Data.DataRow.IsNull%2A> restituisce `true` sia per `DbNull.Value` che per `INullable.Null`.  
  
## <a name="assigning-null-values"></a>Assegnazione di valori Null  
Il valore predefinito per qualsiasi istanza di <xref:System.Data.SqlTypes> è Null.  
  
I valori Null in <xref:System.Data.SqlTypes> sono specifici del tipo e non possono essere rappresentati da un singolo valore, ad esempio `DbNull`. Usare la proprietà `IsNull` per verificare la presenza di valori Null.  
  
È possibile assegnare valori Null a un <xref:System.Data.DataColumn> come illustrato nell'esempio di codice seguente. È possibile assegnare direttamente i valori Null alle variabili `SqlTypes` senza generare un'eccezione.  
  
### <a name="example"></a>Esempio  
Nell'esempio di codice seguente viene creato un <xref:System.Data.DataTable> con due colonne definite come <xref:System.Data.SqlTypes.SqlInt32> e <xref:System.Data.SqlTypes.SqlString>. Il codice aggiunge una riga di valori noti, una riga di valori Null e quindi scorre esegue l'iterazione in <xref:System.Data.DataTable>, assegnando i valori alle variabili e visualizzando l'output nella finestra della console.  
  
[!code-csharp[DataWorks SqlInt32_IsNull#1](~/../sqlclient/doc/samples/SqlInt32_IsNull.cs#1)]
  
L'esempio visualizza i risultati seguenti:  
  
```console
isColumnNull=False, ID=123, Description=Side Mirror  
isColumnNull=True, ID=Null, Description=Null  
```  
  
## <a name="comparing-null-values-with-sqltypes-and-clr-types"></a>Confronto di valori Null con i tipi SqlTypes e CLR  
Quando si confrontano i valori Null, è importante comprendere la differenza tra il modo in cui il metodo `Equals` valuta i valori Null in <xref:System.Data.SqlTypes> e il modo in cui funziona con i tipi CLR. Tutti i metodi <xref:System.Data.SqlTypes>`Equals` usano la semantica del database per valutare i valori Null: se uno o entrambi i valori sono Null, il confronto restituisce Null. D'altra parte, l'uso del metodo CLR `Equals` per due <xref:System.Data.SqlTypes> genera True se entrambi i valori sono Null. Ciò riflette la differenza tra l'uso di un metodo di istanza, ad esempio il metodo CLR `String.Equals`, e l'uso del metodo statico/condiviso, `SqlString.Equals`.  
  
Nell'esempio seguente viene illustrata la differenza nei risultati tra il metodo `SqlString.Equals` e il metodo `String.Equals` quando a ognuno viene passata una coppia di valori Null e quindi una coppia di stringhe vuote.  
  
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
