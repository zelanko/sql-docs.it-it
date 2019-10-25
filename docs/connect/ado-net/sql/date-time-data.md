---
title: Dati relativi a data e ora
description: Viene descritto come utilizzare i nuovi tipi di dati di data e ora introdotti in SQL Server 2008.
ms.date: 09/30/2019
dev_langs:
- csharp
ms.assetid: 6f5ff56a-a57e-49d7-8ae9-bbed697e42e3
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 38626c6c726b9f45bd2d37d5deda480880556856
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452258"
---
# <a name="date-and-time-data"></a>Dati relativi a data e ora

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[Scaricare ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

SQL Server 2008 introduce nuovi tipi di dati per la gestione delle informazioni di data e ora. I nuovi tipi di dati includono tipi distinti per data e ora e tipi di dati espansi con maggiore intervallo, precisione e riconoscimento del fuso orario. Il provider di dati Microsoft SqlClient per SQL Server (<xref:Microsoft.Data.SqlClient>) fornisce il supporto completo per tutte le nuove funzionalità del motore di database SQL Server 2008. Per usare queste nuove funzionalità con SqlClient, è necessario installare la .NET Framework 3,5 SP1 (o versione successiva) o .NET Core 1,0 (o versione successiva).  
  
Le versioni di SQL Server precedenti al SQL Server 2008 hanno solo due tipi di dati per l'utilizzo di valori di data e ora: `datetime` e `smalldatetime`. Entrambi questi tipi di dati contengono sia il valore della data che un valore dell'ora e quindi risulta difficile usare solo uno dei due valori. Inoltre, questi tipi di dati supportano solo le date che si verificano dopo l'introduzione del calendario gregoriano in Inghilterra in 1753. Un altro limite è costituito dal fatto che questi tipi di dati meno recenti non sono compatibili con il fuso orario, rendendo difficile l'utilizzo dei dati che hanno origine da più fusi orari.  
  
La documentazione completa per i tipi di dati SQL Server è disponibile documentazione online di SQL Server. Vedere [utilizzo dei dati di data e ora](https://go.microsoft.com/fwlink/?LinkID=98361) per gli argomenti a livello di voce sui dati relativi a data e ora.
  
## <a name="datetime-data-types-introduced-in-sql-server-2008"></a>Tipi di dati di data e ora introdotti in SQL Server 2008  
 Nella tabella seguente vengono descritti i nuovi tipi di dati di data e ora.  
  
|Tipo di dati di SQL Server|Descrizione|  
|--------------------------|-----------------|  
|`date`|Il tipo di dati `date` include un intervallo compreso tra il 1 gennaio 01 e il 31 dicembre 9999 con un'accuratezza di 1 giorno. Il valore predefinito è 1 gennaio 1900. La dimensione dello spazio di archiviazione è 3 byte.|  
|`time`|Il tipo di dati `time` archivia i valori solo in base a un formato a 24 ore. Il tipo di dati `time` ha un intervallo compreso tra 00:00:00.0000000 e 23:59:59.9999999 con un'accuratezza di 100 nanosecondi. Il valore predefinito è 00:00:00.0000000 (mezzanotte). Il tipo di dati `time` supporta la precisione in secondi frazionari definita dall'utente e le dimensioni di archiviazione variano da 3 a 6 byte in base alla precisione specificata.|  
|`datetime2`|Il tipo di dati `datetime2` combina l'intervallo e la precisione dei tipi di dati `date` e `time` in un unico tipo di dati.<br /><br /> I valori predefiniti e i formati di valore letterale stringa sono identici a quelli definiti nei tipi di dati `date` e `time`.|  
|`datetimeoffset`|Il tipo di dati `datetimeoffset` include tutte le funzionalità di `datetime2`, con l'aggiunta di un offset di fusi orari. L'offset di fusi orari è rappresentato come [+&#124;-] HH:MM. HH è un numero di due cifre, compreso tra 00 e 14, che rappresenta il numero di ore nella differenza di fuso orario. MM è un numero di due cifre, compreso tra 00 e 59, che rappresenta il numero di minuti aggiuntivi della differenza di fuso orario. I formati di ora sono supportati fino a 100 nanosecondi. Il segno + o obbligatorio indica se la differenza di fuso orario viene aggiunta o sottratta dall'ora UTC (Universal Time Coordinate o Greenwich Mean Time) per ottenere l'ora locale.|  
  
> [!NOTE]
>  Per altre informazioni sull'uso della parola chiave `Type System Version`, vedere <xref:Microsoft.Data.SqlClient.SqlConnection.ConnectionString%2A>.  
  
## <a name="date-format-and-date-order"></a>Formato data e ordine data  
Il modo in cui SQL Server analizza i valori di data e ora dipende non solo dalla versione del sistema di tipi e dalla versione del server, ma anche dalle impostazioni predefinite della lingua e del formato del server. Una stringa di data che funziona per i formati di data di una lingua potrebbe non essere riconoscibile se la query viene eseguita da una connessione che utilizza un'impostazione diversa per lingua e formato data.  
  
L'istruzione Transact-SQL SET LANGUAGE imposta in modo implicito l'oggetto DATEFORMAT che determina l'ordine delle parti della data. È possibile utilizzare l'istruzione Transact-SQL SET DATEFORMAT in una connessione per distinguere i valori di data ordinando le parti della data in MDY, DMY, YMD, AGM, MYD o DYM Order.  
  
Se non si specifica alcun oggetto DATEFORMAT per la connessione, SQL Server utilizza la lingua predefinita associata alla connessione. Una stringa di data "01/02/03", ad esempio, verrebbe interpretata come MDY (2 gennaio 2003) in un server con un'impostazione della lingua Stati Uniti lingua inglese e come DMY (1 febbraio 2003) in un server con una lingua britannica inglese. L'anno viene determinato tramite la regola di cambio anno di SQL Server, che definisce la data di taglio per l'assegnazione del valore di secolo. Per altre informazioni, vedere [Opzione two digit year cutoff](https://go.microsoft.com/fwlink/?LinkId=120473) nella documentazione online di SQL Server.  
  
> [!NOTE]
>  Il formato di data AGM non è supportato quando si esegue la conversione da un formato stringa a `date`, `time`, `datetime2` o `datetimeoffset`.  
  
Per altre informazioni sulla modalità di interpretazione dei dati relativi a data e ora in SQL Server, vedere [Uso di dati relativi a data e ora](https://go.microsoft.com/fwlink/?LinkID=98361) nella documentazione online di SQL Server 2008.  
  
## <a name="datetime-data-types-and-parameters"></a>Parametri e tipi di dati di data/ora  
Per supportare i nuovi tipi di dati di data e ora sono state aggiunte le enumerazioni seguenti al <xref:System.Data.SqlDbType>.  
  
- `SqlDbType.Date`  
  
- `SqlDbType.Time`  
  
- `SqlDbType.DateTime2`  
  
- `SqlDbType.DateTimeOffSet`  

È possibile specificare il tipo di dati di un oggetto <xref:Microsoft.Data.SqlClient.SqlParameter> usando una delle enumerazioni <xref:System.Data.SqlDbType> precedenti. 

> [!NOTE]
> Non è possibile impostare la proprietà `DbType` di un `SqlParameter` `SqlDbType.Date`.

È anche possibile specificare il tipo di un oggetto <xref:Microsoft.Data.SqlClient.SqlParameter> in modo generico impostando la proprietà <xref:Microsoft.Data.SqlClient.SqlParameter.DbType%2A> di un oggetto `SqlParameter` su un particolare valore dell'enumerazione <xref:System.Data.DbType>. I valori di enumerazione seguenti sono stati aggiunti a <xref:System.Data.DbType> per supportare i tipi di dati `datetime2` e `datetimeoffset`:  
  
- DbType. DateTime2  
  
- DbType. DateTimeOffset  
  
Queste nuove enumerazioni integrano le enumerazioni `Date`, `Time` e `DateTime`.  
  
Il tipo di provider di dati Microsoft SqlClient di un oggetto Parameter viene dedotto dal tipo .NET del valore dell'oggetto Parameter o dal `DbType` dell'oggetto Parameter. Non sono stati introdotti nuovi tipi di dati <xref:System.Data.SqlTypes> per supportare i nuovi tipi di dati di data e ora. Nella tabella seguente vengono descritti i mapping tra i tipi di dati SQL Server 2008 data e ora e i tipi di dati CLR.  
  
|Tipo di dati di SQL Server|Tipo .NET|System. Data. SqlDbType|System. Data. DbType|  
|--------------------------|-------------------------|---------------------------|------------------------|  
|Data|System.DateTime|date|date|  
|time|System.TimeSpan|Time|Time|  
|datetime2|System.DateTime|datetime2|datetime2|  
|datetimeoffset|System.DateTimeOffset|DateTimeOffset|DateTimeOffset|  
|DATETIME|System.DateTime|DateTime|DateTime|  
|smalldatetime|System.DateTime|DateTime|DateTime|  
  
### <a name="sqlparameter-properties"></a>Proprietà di SqlParameter  
 Nella tabella seguente vengono descritte `SqlParameter` proprietà rilevanti per i tipi di dati di data e ora.  
  
|Proprietà|Descrizione|  
|--------------|-----------------|  
|<xref:Microsoft.Data.SqlClient.SqlParameter.IsNullable%2A>|Ottiene o imposta un valore che indica se un valore ammette i valori null. Quando si invia un valore di parametro null al server, è necessario specificare <xref:System.DBNull>, anziché `null` (`Nothing` in Visual Basic). Per ulteriori informazioni sui valori null di database, vedere [gestione di valori null](handle-null-values.md).|  
|<xref:Microsoft.Data.SqlClient.SqlParameter.Precision%2A>|Ottiene o imposta il numero massimo di cifre usate per rappresentare il valore. Questa impostazione viene ignorata per i tipi di dati di data e ora.|  
|<xref:Microsoft.Data.SqlClient.SqlParameter.Scale%2A>|Ottiene o imposta il numero di posizioni decimali in cui viene risolta la parte del valore relativa all'ora per `Time`, `DateTime2` e `DateTimeOffset`. Il valore predefinito è 0, che indica che la scala effettiva viene dedotta dal valore e inviata al server.|  
|<xref:Microsoft.Data.SqlClient.SqlParameter.Size%2A>|Ignorato per i tipi di dati di data e ora.|  
|<xref:Microsoft.Data.SqlClient.SqlParameter.Value%2A>|Ottiene o imposta il valore del parametro.|  
|<xref:Microsoft.Data.SqlClient.SqlParameter.SqlValue%2A>|Ottiene o imposta il valore del parametro.|  
  
> [!NOTE]
>  I valori di ora minori di zero o maggiori o uguali a 24 ore genereranno un <xref:System.ArgumentException>.  
  
### <a name="creating-parameters"></a>Creazione di parametri  
È possibile creare un oggetto <xref:Microsoft.Data.SqlClient.SqlParameter> usando il relativo costruttore o aggiungendolo a un <xref:Microsoft.Data.SqlClient.SqlCommand>. <xref:Microsoft.Data.SqlClient.SqlCommand.Parameters%2A> raccolta chiamando il metodo `Add` della <xref:Microsoft.Data.SqlClient.SqlParameterCollection>. Il metodo `Add` accetterà come input gli argomenti del costruttore o un oggetto parametro esistente.  
  
Nelle sezioni successive di questo argomento vengono forniti esempi di come specificare i parametri di data e ora.
  
### <a name="date-example"></a>Esempio di data  
Nel frammento di codice seguente viene illustrato come specificare un parametro `date`.  
  
```csharp  
SqlParameter parameter = new SqlParameter();  
parameter.ParameterName = "@Date";  
parameter.SqlDbType = SqlDbType.Date;  
parameter.Value = "2007/12/1";  
```  
  
### <a name="time-example"></a>Esempio di tempo  
Nel frammento di codice seguente viene illustrato come specificare un parametro `time`.  
  
```csharp  
SqlParameter parameter = new SqlParameter();  
parameter.ParameterName = "@time";  
parameter.SqlDbType = SqlDbType.Time;  
parameter.Value = DateTime.Parse("23:59:59").TimeOfDay;  
```  
  
### <a name="datetime2-example"></a>Esempio di datetime2  
Nel frammento di codice seguente viene illustrato come specificare un parametro di `datetime2` con le parti di data e ora.  
  
```csharp  
SqlParameter parameter = new SqlParameter();  
parameter.ParameterName = "@Datetime2";  
parameter.SqlDbType = SqlDbType.DateTime2;  
parameter.Value = DateTime.Parse("1666-09-02 1:00:00");  
```  
  
### <a name="datetimeoffset-example"></a>Esempio relativo a DateTimeOffset  
Nel frammento di codice seguente viene illustrato come specificare un parametro di `DateTimeOffSet` con una data, un'ora e una differenza di fuso orario pari a 0.  
  
```csharp  
SqlParameter parameter = new SqlParameter();  
parameter.ParameterName = "@DateTimeOffSet";  
parameter.SqlDbType = SqlDbType.DateTimeOffSet;  
parameter.Value = DateTimeOffset.Parse("1666-09-02 1:00:00+0");  
```  
  
### <a name="addwithvalue"></a>AddWithValue  
È anche possibile specificare parametri usando il metodo `AddWithValue` di un <xref:Microsoft.Data.SqlClient.SqlCommand>, come illustrato nel frammento di codice seguente. Tuttavia, il metodo `AddWithValue` non consente di specificare il <xref:Microsoft.Data.SqlClient.SqlParameter.DbType%2A> o <xref:Microsoft.Data.SqlClient.SqlParameter.SqlDbType%2A> per il parametro.  
  
```csharp  
command.Parameters.AddWithValue(   
    "@date", DateTimeOffset.Parse("16660902"));  
```  
  
È possibile eseguire il mapping del parametro `@date` a un tipo di dati `date`, `datetime` o `datetime2` nel server. Quando si utilizzano i nuovi tipi di dati di `datetime`, è necessario impostare in modo esplicito la proprietà <xref:System.Data.SqlDbType> del parametro sul tipo di dati dell'istanza. L'utilizzo di <xref:System.Data.SqlDbType.Variant> o la fornitura implicita di valori di parametro può causare problemi di compatibilità con le versioni precedenti dei tipi di dati `datetime` e `smalldatetime`.  
  
Nella tabella seguente vengono illustrate le `SqlDbTypes` derivate da quali tipi CLR:  
  
|Tipo CLR|SqlDbType derivato|  
|--------------|------------------------|  
|DateTime|SqlDbType. DateTime|  
|TimeSpan|SqlDbType. Time|  
|DateTimeOffset|SqlDbType. DateTimeOffset|  
  
## <a name="retrieving-date-and-time-data"></a>Recupero di dati di data e ora  
Nella tabella seguente sono descritti i metodi usati per recuperare i valori di SQL Server 2008 relativi a data e ora.  
  
|Metodo SqlClient|Descrizione|  
|----------------------|-----------------|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetDateTime%2A>|Recupera il valore della colonna specificata come struttura <xref:System.DateTime>.|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetDateTimeOffset%2A>|Recupera il valore della colonna specificata come struttura <xref:System.DateTimeOffset>.|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetProviderSpecificFieldType%2A>|Restituisce il tipo che rappresenta il tipo specifico del provider sottostante per il campo. Restituisce gli stessi tipi di `GetFieldType` per i nuovi tipi di data e ora.|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetProviderSpecificValue%2A>|Recupera il valore della colonna specificata. Restituisce gli stessi tipi di `GetValue` per i nuovi tipi di data e ora.|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetProviderSpecificValues%2A>|Recupera i valori nella matrice specificata.|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlString%2A>|Recupera il valore della colonna come <xref:System.Data.SqlTypes.SqlString>. Si verifica un <xref:System.InvalidCastException> se i dati non possono essere espressi come `SqlString`.|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlValue%2A>|Recupera i dati della colonna come `SqlDbType` predefiniti. Restituisce gli stessi tipi di `GetValue` per i nuovi tipi di data e ora.|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlValues%2A>|Recupera i valori nella matrice specificata.|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetString%2A>|Recupera il valore della colonna come stringa se Type System Version è impostata su SQL Server 2005. Si verifica un <xref:System.InvalidCastException> se i dati non possono essere espressi sotto forma di stringa.|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetTimeSpan%2A>|Recupera il valore della colonna specificata come struttura <xref:System.TimeSpan>.|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetValue%2A>|Recupera il valore della colonna specificata come tipo CLR sottostante.|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetValues%2A>|Recupera i valori di colonna in una matrice.|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetSchemaTable%2A>|Restituisce un <xref:System.Data.DataTable> che descrive i metadati del set di risultati.|  
  
> [!NOTE]
>  I nuovi `SqlDbTypes` di data e ora non sono supportati per il codice in esecuzione in-process nel SQL Server. Se uno di questi tipi viene passato al server, verrà generata un'eccezione.  
  
## <a name="specifying-date-and-time-values-as-literals"></a>Specifica di valori di data e ora come valori letterali  
È possibile specificare i tipi di dati di data e ora usando un'ampia gamma di formati di stringhe letterali diversi, che SQL Server valuta in fase di esecuzione, convertendo tali tipi in strutture di data/ora interne. SQL Server riconosce i dati di data e ora racchiusi tra virgolette singole ('). Gli esempi seguenti illustrano alcuni formati:  
  
- Formati di data alfabetici, ad esempio `'October 15, 2006'`.  
  
- Formati di data numerici, ad esempio `'10/15/2006'`.  
  
- Formati di stringa non separati, ad esempio `'20061015'`, che verrebbero interpretati come 15 ottobre 2006 se si utilizza il formato di data standard ISO.  
  
> [!NOTE]
>  È possibile trovare la documentazione completa per tutti i formati di stringa letterale e altre funzionalità dei tipi di dati di data e ora in documentazione online di SQL Server.  
  
I valori di ora minori di zero o maggiori o uguali a 24 ore genereranno un <xref:System.ArgumentException>.  
  
## <a name="resources-in-sql-server-2008-books-online"></a>Risorse nella documentazione online di SQL Server 2008  
Per ulteriori informazioni sull'utilizzo dei valori di data e ora in SQL Server 2008, vedere le seguenti risorse nella documentazione online di SQL Server 2008.  
  
|Argomento|Descrizione|  
|-----------|-----------------|  
|[Funzioni e tipi di dati di data e ora (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=98360)|Viene fornita una panoramica di tutte le funzioni e i tipi di dati relativi a data e ora di Transact-SQL.|  
|[Uso di dati relativi a data e ora](https://go.microsoft.com/fwlink/?LinkId=98361)|Informazioni sui tipi di dati e le funzioni relativi a data e ora ed esempi per l'uso.|  
|[Tipi di dati (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=98362)|Descrive i tipi di dati di sistema in SQL Server 2008.|  
  
## <a name="next-steps"></a>Passaggi successivi
- [Tipi di dati SQL Server e ADO.NET](sql-server-data-types.md)
