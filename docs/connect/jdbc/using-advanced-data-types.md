---
title: Uso di tipi di dati avanzati
description: Informazioni su come usare i tipi di dati avanzati JDBC per eseguire la conversione dei tipi di dati SQL Server in tipi di dati Java tramite Microsoft JDBC Driver for SQL Server.
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: b39461d3-48d6-4048-8300-1a886c00756d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 509c2735475b7113887a2291ac6cdfb67dfc865a
ms.sourcegitcommit: 1a96abbf434dfdd467d0a9b722071a1ca1aafe52
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/16/2020
ms.locfileid: "81528725"
---
# <a name="using-advanced-data-types"></a>Uso di tipi di dati avanzati

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

In [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] vengono usati i tipi di dati JDBC avanzati per convertire i tipi di dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in un formato comprensibile nel linguaggio di programmazione Java.  
  
## <a name="remarks"></a>Osservazioni

Nella tabella seguente sono riportati i mapping predefiniti tra i tipi di dati avanzati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], JDBC e del linguaggio di programmazione Java.  
  
|Tipi di SQL Server|Tipi JDBC (java.sql.Types)|Tipi del linguaggio Java|  
|----------------------|-----------------------------------|-------------------------|  
|varbinary(max)<br /><br /> image|LONGVARBINARY|byte[] \(default), Blob, InputStream, String|  
|text<br /><br /> ntext|LONGVARCHAR|String (default), Clob, InputStream|  
|ntext<br /><br /> nvarchar(max)|LONGVARCHAR<br /><br /> LONGNVARCHAR (Java SE 6.0)|String (default), Clob, NClob|  
|Xml|LONGVARCHAR<br /><br /> SQLXML|String (default), InputStream, Clob, byte[], Blob, SQLXML|  
|Udt<sup>1</sup>|VARBINARY|String (default), byte[], InputStream|  
|sqlvariant|SQLVARIANT|Oggetto|  
|geometry<br /><br /> geography|VARBINARY|byte[]|  


<sup>1</sup>[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] supporta l'invio e il recupero di tipi definiti dall'utente (UDT) CLR come dati binari, ma non supporta la manipolazione dei metadati CLR.  
  
Nelle sezioni seguenti vengono forniti esempi di come sia possibile utilizzare il driver JDBC e i tipi di dati avanzati.  
  
## <a name="blob-and-clob-and-nclob-data-types"></a>Tipi di dati BLOB, CLOB e NCLOB

Nel driver JDBC sono implementati tutti i metodi delle interfacce java.sql.Blob, java.sql.Clob e java.sql.NClob.  
  
> [!NOTE]  
> I valori CLOB possono essere usati con i tipi di dati di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] (o versioni successive) per valori di grandi dimensioni. In particolare, i tipi CLOB possono essere usati con i tipi di dati **varchar(max)** e **nvarchar(max)** , i tipi di BLOB possono essere usati con i tipi di dati **varbinary(max)** e **image** e i tipi NCLOB possono essere usati con **ntext** e **nvarchar(max)** .  

## <a name="large-value-data-types"></a>Tipi di dati per valori di grandi dimensioni

Nelle versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] l'uso di tipi di dati per valori di grandi dimensioni richiedeva particolari operazioni di gestione. I tipi di dati per valori di grandi dimensioni sono quelli che superano le dimensioni di riga massime di 8 KB. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è stato introdotto un identificatore max per i tipi di dati **varchar**, **nvarchar** e **varbinary** per consentire l'archiviazione di valori fino a 2^31 byte. Le colonne di tabella e le variabili [!INCLUDE[tsql](../../includes/tsql-md.md)] possono specificare tipi di dati **varchar(max)** , **nvarchar(max)** o **varbinary(max)** .  

Gli scenari principali di utilizzo di tipi per valori di grandi dimensioni riguardano il recupero di tali tipi di dati da un database o l'aggiunta degli stessi a un database. Nelle sezioni seguenti vengono descritti i diversi approcci adottabili per eseguire queste attività.  

### <a name="retrieving-large-value-types-from-a-database"></a>Recupero di tipi per valori di grandi dimensioni da un database

Quando si recupera un tipo di dati per valori di grandi dimensioni non binario, ad esempio **varchar(max)** , da un database, uno degli approcci adottabili consiste nel leggere i dati in questione come flusso di caratteri. Nell'esempio seguente viene usato il metodo [executeQuery](../../connect/jdbc/reference/executequery-method-sqlserverstatement.md) della classe [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) per recuperare dati dal database e restituirli come set di risultati. Viene quindi usato il metodo [getCharacterStream](../../connect/jdbc/reference/getcharacterstream-method-sqlserverresultset.md) della classe [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) per leggere i dati per valori di grandi dimensioni dal set di risultati.  

```java
ResultSet rs = stmt.executeQuery("SELECT TOP 1 * FROM Test1");  
rs.next();  
Reader reader = rs.getCharacterStream(2);  
```

> [!NOTE]
> Questo stesso approccio può essere usato anche per i tipi di dati **text**, **ntext** e **nvarchar(max)** .  

Quando si recupera un tipo di dati per valori di grandi dimensioni binario, ad esempio **varbinary(max)** , da un database, è possibile adottare diversi approcci. L'approccio più efficace consiste nel leggere i dati come flusso binario, come nell'esempio seguente:  

```java
ResultSet rs = stmt.executeQuery("SELECT photo FROM mypics");  
rs.next();  
InputStream is = rs.getBinaryStream(2);  
```

È inoltre possibile usare il metodo [getBytes](../../connect/jdbc/reference/getbytes-method-sqlserverresultset.md) per leggere i dati come matrice di byte, come nell'esempio seguente:  

```java
ResultSet rs = stmt.executeQuery("SELECT photo FROM mypics");  
rs.next();  
byte [] b = rs.getBytes(2);  
```

> [!NOTE]  
> È inoltre possibile leggere i dati come BLOB. Tuttavia, questo metodo è meno efficace dei due precedenti.  

### <a name="adding-large-value-types-to-a-database"></a>Aggiunta di tipi per valori di grandi dimensioni a un database

Il caricamento di dati di grandi dimensioni con il driver JDBC funziona bene per i dati di dimensioni pari a quelle della memoria, e nel caso di dati di dimensioni maggiori di quelle della memoria, l'opzione principale è rappresentata dall'utilizzo di flussi. Tuttavia, il modo più efficace per caricare dati di grandi dimensioni è mediante interfacce di flusso.  

È però possibile utilizzare anche stringhe o byte, come nell'esempio seguente:  

```java
PreparedStatement pstmt = con.prepareStatement("INSERT INTO test1 (c1_id, c2_vcmax) VALUES (?, ?)");  
pstmt.setInt(1, 1);  
pstmt.setString(2, htmlStr);  
pstmt.executeUpdate();  
```

> [!NOTE]  
> Questo approccio può essere usato anche per valori archiviati in colonne **text**, **ntext** e **nvarchar(max)** .  

Se nel server è presente una libreria di immagini ed è necessario caricare interi file di immagine binari in una colonna **varbinary(max)** , il modo più efficace per eseguire tale attività con il driver JDBC consiste nell'usare direttamente flussi, come nell'esempio seguente:  

```java
try (PreparedStatement pstmt = con.prepareStatement("INSERT INTO test1 (Col1, Col2) VALUES(?,?)")) { 
  File inputFile = new File("CLOBFile20mb.jpg");  
  try (FileInputStream inStream = new FileInputStream(inputFile)) {
    int id = 1;  
    pstmt.setInt(1,id);  
    pstmt.setBinaryStream(2, inStream);  
    pstmt.executeUpdate();
  }
}
```

> [!NOTE]  
> L'utilizzo del metodo Clob o Blob non rappresenta un modo efficace di caricamento di dati di grandi dimensioni.  

### <a name="modifying-large-value-types-in-a-database"></a>Modifica dei tipi per valori di grandi dimensioni in un database

Nella maggior parte dei casi, l'approccio consigliato per aggiornare o modificare valori di grandi dimensioni nel database consiste nel passare parametri mediante le classi [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) e [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md), usando comandi [!INCLUDE[tsql](../../includes/tsql-md.md)] quali `UPDATE`, `WRITE` e `SUBSTRING`.  

Se è necessario sostituire l'istanza di una parola in un file di testo di grandi dimensioni, quale ad esempio un file HTML archiviato, è possibile usare un oggetto Clob, come nell'esempio seguente:  

```java
String SQL = "SELECT * FROM test1;";  
try (Statement stmt = con.createStatement(ResultSet.TYPE_SCROLL_SENSITIVE, ResultSet.CONCUR_UPDATABLE)
     ResultSet rs = stmt.executeQuery(SQL)) {
  rs.next();

  Clob clob = rs.getClob(2);  
  long pos = clob.position("dog", 1);  
  clob.setString(pos, "cat");  
  rs.updateClob(2, clob);  
  rs.updateRow();  
}
```

Inoltre, è possibile eseguire tutte le operazioni sul server e quindi passare solo i parametri a un'istruzione UPDATE preparata.  

Per ulteriori informazioni sui tipi per valori di grandi dimensioni, vedere la sezione relativa all'utilizzo di tipi per valori di grandi dimensioni nella Documentazione online di SQL Server.  

## <a name="xml-data-type"></a>Tipo di dati XML

In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è disponibile il tipo di dati **xml**, che consente di archiviare documenti e frammenti XML in un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Il tipo di dati **xml**,un tipo di dati predefinito di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è simile per alcuni aspetti ad altri tipi predefiniti, quali **int** e **varchar**. Come accade con gli altri tipi predefiniti, è possibile usare il tipo di dati **xml** come tipo di colonna quando si crea una tabella, come tipo di variabile, come tipo di parametro o come tipo restituito da una funzione oppure nelle funzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] CAST e CONVERT.  
  
Nel driver JDBC, è possibile eseguire il mapping del tipo di dati **xml** come stringa, matrice di byte, flusso o oggetto CLOB, BLOB o SQLXML. Il mapping predefinito è come stringa. A partire da Microsoft JDBC Driver versione 2.0, il driver JDBC offre il supporto per l'API di JDBC 4.0, in cui viene presentata l'interfaccia SQLXML. Tale interfaccia definisce i metodi per interagire e modificare i dati XML. Il tipo di dati **SQLXML** corrisponde al tipo di dati **xml** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per altre informazioni su come leggere e scrivere dati XML da e in un database relazionale con il tipo di dati Java **SQLXML**, vedere [Supporto dei dati XML](../../connect/jdbc/supporting-xml-data.md).  
  
L'implementazione del tipo di dati **xml** nel driver JDBC consente di supportare quanto segue:  
  
- Accesso al codice XML come stringa UTF-16 Java standard per la maggior parte degli scenari di programmazione comuni  
  
- Input di codice XML in formato UTF-8 e con altri tipi di codifica a 8 bit  
  
- Accesso al codice XML come matrice di byte, con un indicatore dell'ordine di byte (BOM) iniziale in caso di codifica in formato UTF-16 per l'interscambio con altri processori e file su disco XML  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] richiede un indicatore dell'ordine di byte (BOM) iniziale per il codice XML con codifica UTF-16. Questo elemento deve essere fornito dall'applicazione quando i valori dei parametri XML vengono forniti come matrici di byte. Nell'output di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] i valori XML sono sempre presenti come stringhe UTF-16 senza indicatore dell'ordine di byte (BOM) né dichiarazione di codifica incorporata. Quando vengono recuperati valori XML come byte[], BinaryStream o Blob, un BOM UTF-16 viene anteposto al valore.  
  
Per altre informazioni sul tipo di dati **xml**, vedere l'argomento "Tipo di dati XML" nella documentazione online di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="user-defined-data-type"></a>Tipo di dati definito dall'utente  

L'introduzione di tipi definiti dall'utente (UDT, User-Defined Type) in [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] estende il sistema di tipi SQL consentendo di archiviare oggetti e strutture di dati personalizzate in un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. I tipi definiti dall'utente possono contenere più tipi di dati e possono assumere comportamenti, differenziandoli dai tipi di dati alias tradizionali costituiti da un singolo tipo di dati di sistema [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. I tipi di dati UDT vengono definiti utilizzando uno qualsiasi dei linguaggi supportati dalla funzionalità CLR (Common Language Runtime) di Microsoft .NET in grado di produrre codice verificabile, tra cui Microsoft Visual C# e Visual Basic .NET. I dati vengono esposti come campi e proprietà di una classe o una struttura basata su .NET Framework e i comportamenti vengono definiti dai metodi della classe o della struttura in questione.  
  
In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è possibile usare un tipo di dati UDT come definizione di colonna di una tabella, come variabile in un batch [!INCLUDE[tsql](../../includes/tsql-md.md)] o come argomento di una funzione o una stored procedure [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
Per altre informazioni sui tipi di dati definiti dall'utente, vedere la sezione sull'uso e la modifica delle istanze dei tipi definiti dall'utente nella documentazione online di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="sql_variant-data-type"></a>Tipo di dati sql_variant

Per informazioni sul tipo di dati sql_variant, vedere [Uso del tipo di dati sql_variant](../../connect/jdbc/using-sql-variant-datatype.md).  

## <a name="spatial-data-types"></a>Tipi di dati spaziali

Per informazioni sui tipi di dati spaziali, vedere [Uso dei tipi di dati spaziali](../../connect/jdbc/use-spatial-datatypes.md).  

## <a name="see-also"></a>Vedere anche

[Informazioni sui tipi di dati del driver JDBC](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
