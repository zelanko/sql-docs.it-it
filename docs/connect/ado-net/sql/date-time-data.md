---
title: Dati relativi a data e ora
description: Viene descritto come usare i nuovi tipi di dati relativi a data e ora introdotti in SQL Server 2008.
ms.date: 09/30/2019
dev_langs:
- csharp
ms.assetid: 6f5ff56a-a57e-49d7-8ae9-bbed697e42e3
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: 95c250c0eff6d22bb5bc8b284503156d412d6a45
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "75247814"
---
# <a name="date-and-time-data"></a>Dati relativi a data e ora

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[Scaricare ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

SQL Server 2008 introduce nuovi tipi di dati per la gestione delle informazioni relative a data e ora. I nuovi tipi di dati includono tipi distinti per data e ora e tipi di dati espansi ottimizzati in termini di intervallo, precisione e riconoscimento del fuso orario. Il provider di dati Microsoft SqlClient per SQL Server (<xref:Microsoft.Data.SqlClient>) offre il supporto completo per tutte le nuove funzionalità del motore di database di SQL Server 2008. Per usare queste nuove funzionalità con SqlClient, è necessario installare .NET Framework 3.5 SP1 (o versione successiva) o .NET Core 1.0 (o versione successiva).  
  
Le versioni di SQL Server precedenti a SQL Server 2008 hanno solo due tipi di dati per l'uso dei valori di data e ora: `datetime` e `smalldatetime`. Entrambi questi tipi di dati contengono sia il valore della data che un valore dell'ora e quindi risulta difficile usare solo uno dei due valori. Questi tipi di dati inoltre supportano solo le date che cadono dopo l'introduzione del calendario gregoriano, avvenuta nel 1753 in Inghilterra. Un'altra limitazione è che i tipi di dati più datati non dipendono dal fuso orario e per questo motivo è difficile lavorare con dati che provengono da più fusi orari.  
  
La documentazione completa per i tipi di dati di SQL Server è disponibile nella documentazione online di SQL Server. Vedere [Uso di dati relativi a data e ora](https://go.microsoft.com/fwlink/?LinkID=98361) per gli argomenti di base sui dati per data e ora.
  
## <a name="datetime-data-types-introduced-in-sql-server-2008"></a>Tipi di dati di data e ora introdotti in SQL Server 2008  
 Nella seguente tabella vengono illustrati i nuovi tipi di dati per data e ora.  
  
|Tipo di dati di SQL Server|Descrizione|  
|--------------------------|-----------------|  
|`date`|Il tipo di dati `date` include un intervallo compreso tra il 1 gennaio 01 e il 31 dicembre 9999 con un'accuratezza di 1 giorno. Il valore predefinito è 1 gennaio 1900. La dimensione dello spazio di archiviazione è 3 byte.|  
|`time`|Il tipo di dati `time` archivia i valori solo in base a un formato a 24 ore. Il tipo di dati `time` ha un intervallo compreso tra 00:00:00.0000000 e 23:59:59.9999999 con un'accuratezza di 100 nanosecondi. Il valore predefinito è 00:00:00.0000000 (mezzanotte). Il tipo di dati `time` supporta la precisione in secondi frazionari definita dall'utente e le dimensioni di archiviazione variano da 3 a 6 byte in base alla precisione specificata.|  
|`datetime2`|Il tipo di dati `datetime2` combina l'intervallo e la precisione dei tipi di dati `date` e `time` in un unico tipo di dati.<br /><br /> I valori predefiniti e i formati di valore letterale stringa sono gli stessi definiti nei tipi di dati `date` e `time`.|  
|`datetimeoffset`|Il tipo di dati `datetimeoffset` include tutte le funzionalità di `datetime2`, con l'aggiunta di un offset di fusi orari. L'offset di fusi orari è rappresentato come [+&#124;-] HH:MM. HH è un numero di due cifre, compreso tra 00 e 14, che rappresenta il numero di ore nella differenza di fuso orario. MM è un numero di due cifre, compreso tra 00 e 59, che rappresenta il numero di minuti aggiuntivi della differenza di fuso orario. I formati di ora sono supportati fino a 100 nanosecondi. Il segno + o - obbligatorio indica se la differenza di fuso orario viene aggiunta o sottratta dall'ora UTC (Universal Time Coordinate o ora di Greenwich) per ottenere l'ora locale.|  
  
> [!NOTE]
>  Per altre informazioni sull'uso della parola chiave `Type System Version`, vedere <xref:Microsoft.Data.SqlClient.SqlConnection.ConnectionString%2A>.  
  
## <a name="date-format-and-date-order"></a>Formato data e ordine data  
Il modo in cui SQL Server analizza i valori di data e ora dipende non solo dalla versione del sistema di tipi e dalla versione del server, ma anche dalle impostazioni della lingua predefinita e del formato di data del server. Una stringa di data che funziona per i formati di data di una lingua potrebbe non essere riconoscibile se la query viene eseguita da una connessione che usa un'altra impostazione per la lingua e il formato di data.  
  
L'istruzione Transact-SQL SET LANGUAGE imposta in modo implicito l'oggetto DATEFORMAT che determina l'ordine delle parti della data. È possibile usare l'istruzione Transact-SQL SET DATEFORMAT per una connessione per distinguere i valori di data ordinando le parti della data nell'ordine MDY, DMY, YMD, MYD o DYM.  
  
Se non si specifica alcun oggetto DATEFORMAT per la connessione, SQL Server usa la lingua predefinita associata alla connessione. Ad esempio, una stringa di data "01/02/03" viene interpretata come MDY (2 gennaio 2003) su un server con impostazione della lingua Inglese (Stati Uniti) e come DMY (1 febbraio 2003) su un server con impostazione della lingua Inglese (Regno Unito). L'anno viene determinato usando la regola dell'anno di cambio data di SQL Server, che definisce la data limite per l'assegnazione del valore di secolo. Per altre informazioni, vedere [Opzione two digit year cutoff](https://go.microsoft.com/fwlink/?LinkId=120473) nella documentazione online di SQL Server.  
  
> [!NOTE]
>  Il formato di data YDM non è supportato quando si esegue la conversione da un formato stringa a `date`, `time`, `datetime2` o `datetimeoffset`.  
  
Per altre informazioni sulla modalità di interpretazione dei dati relativi a data e ora in SQL Server, vedere [Uso di dati relativi a data e ora](https://go.microsoft.com/fwlink/?LinkID=98361) nella documentazione online di SQL Server 2008.  
  
## <a name="datetime-data-types-and-parameters"></a>Tipi di dati e parametri di data/ora  
Le enumerazioni riportate di seguito sono state aggiunte a <xref:System.Data.SqlDbType> per supportare i nuovi tipi di dati relativi a data e ora.  
  
- `SqlDbType.Date`  
  
- `SqlDbType.Time`  
  
- `SqlDbType.DateTime2`  
  
- `SqlDbType.DateTimeOffSet`  

È possibile specificare il tipo di dati di un oggetto <xref:Microsoft.Data.SqlClient.SqlParameter> usando una delle enumerazioni <xref:System.Data.SqlDbType> precedenti. 

> [!NOTE]
> Non è possibile impostare la proprietà `DbType` di un `SqlParameter` su `SqlDbType.Date`.

È anche possibile specificare il tipo di un oggetto <xref:Microsoft.Data.SqlClient.SqlParameter> in modo generico impostando la proprietà <xref:Microsoft.Data.SqlClient.SqlParameter.DbType%2A> di un oggetto `SqlParameter` su un particolare valore dell'enumerazione <xref:System.Data.DbType>. I valori di enumerazione seguenti sono stati aggiunti a <xref:System.Data.DbType> per supportare i tipi di dati `datetime2` e `datetimeoffset`:  
  
- DbType.DateTime2  
  
- DbType.DateTimeOffset  
  
Queste nuove enumerazioni integrano le enumerazioni `Date`, `Time` e `DateTime`.  
  
Il tipo di provider di dati Microsoft SqlClient di un oggetto parametro viene dedotto dal tipo .NET del valore dell'oggetto parametro o dall'elemento `DbType` dell'oggetto parametro. Non sono stati introdotti nuovi tipi di dati <xref:System.Data.SqlTypes> per supportare i nuovi tipi di dati di data e ora. Nella tabella seguente sono descritti i mapping tra i tipi di dati per data e ora di SQL Server 2008 e i tipi di dati CLR.  
  
|Tipo di dati di SQL Server|Tipo .NET|System.Data.SqlDbType|System.Data.DbType|  
|--------------------------|-------------------------|---------------------------|------------------------|  
|Data|System.DateTime|Data|Data|  
|time|System.TimeSpan|Tempo|Tempo|  
|datetime2|System.DateTime|DateTime2|DateTime2|  
|datetimeoffset|System.DateTimeOffset|DateTimeOffset|DateTimeOffset|  
|Datetime|System.DateTime|Datetime|Datetime|  
|smalldatetime|System.DateTime|Datetime|Datetime|  
  
### <a name="sqlparameter-properties"></a>Proprietà SqlParameter  
 Nella tabella seguente vengono descritte le proprietà `SqlParameter` pertinenti ai tipi di dati per data e ora.  
  
|Proprietà|Descrizione|  
|--------------|-----------------|  
|<xref:Microsoft.Data.SqlClient.SqlParameter.IsNullable%2A>|Ottiene o imposta un valore che indica se il valore ammette i valori Null. Quando si invia un valore di parametro Null al server, è necessario specificare <xref:System.DBNull> anziché `null` (`Nothing` in Visual Basic). Per altre informazioni sui valori Null di database, vedere [Gestione dei valori Null](handle-null-values.md).|  
|<xref:Microsoft.Data.SqlClient.SqlParameter.Precision%2A>|Ottiene o imposta il numero massimo di cifre usate per rappresentare il valore. Questa impostazione viene ignorata per i tipi di dati relativi a data e ora.|  
|<xref:Microsoft.Data.SqlClient.SqlParameter.Scale%2A>|Ottiene o imposta il numero di posizioni decimali in cui viene risolta la parte del valore relativa all'ora per `Time`, `DateTime2` e `DateTimeOffset`. Il valore predefinito è 0, che indica che la scala effettiva viene dedotta dal valore e inviata al server.|  
|<xref:Microsoft.Data.SqlClient.SqlParameter.Size%2A>|Viene ignorata per i tipi di dati per data e ora.|  
|<xref:Microsoft.Data.SqlClient.SqlParameter.Value%2A>|Ottiene o imposta il valore del parametro.|  
|<xref:Microsoft.Data.SqlClient.SqlParameter.SqlValue%2A>|Ottiene o imposta il valore del parametro.|  
  
> [!NOTE]
>  I valori di ora minori di zero o maggiori o uguali a 24 ore genereranno un <xref:System.ArgumentException>.  
  
### <a name="creating-parameters"></a>Creazione di parametri  
È possibile creare un oggetto <xref:Microsoft.Data.SqlClient.SqlParameter> usando il relativo costruttore o aggiungendolo a una raccolta <xref:Microsoft.Data.SqlClient.SqlCommand>.<xref:Microsoft.Data.SqlClient.SqlCommand.Parameters%2A> chiamando il metodo `Add` di <xref:Microsoft.Data.SqlClient.SqlParameterCollection>. Il metodo `Add` accetterà come input gli argomenti del costruttore o un oggetto parametro esistente.  
  
Le sezioni successive di questo argomento contengono esempi che illustrano come specificare i parametri di data e ora.
  
### <a name="date-example"></a>Esempio di data  
Il frammento di codice seguente illustra come specificare un parametro `date`.  
  
```csharp  
SqlParameter parameter = new SqlParameter();  
parameter.ParameterName = "@Date";  
parameter.SqlDbType = SqlDbType.Date;  
parameter.Value = "2007/12/1";  
```  
  
### <a name="time-example"></a>Esempio di ora  
Il frammento di codice seguente illustra come specificare un parametro `time`.  
  
```csharp  
SqlParameter parameter = new SqlParameter();  
parameter.ParameterName = "@time";  
parameter.SqlDbType = SqlDbType.Time;  
parameter.Value = DateTime.Parse("23:59:59").TimeOfDay;  
```  
  
### <a name="datetime2-example"></a>Esempio di Datetime2  
Il frammento di codice seguente illustra come specificare un parametro `datetime2` con parti sia di data che di ora.  
  
```csharp  
SqlParameter parameter = new SqlParameter();  
parameter.ParameterName = "@Datetime2";  
parameter.SqlDbType = SqlDbType.DateTime2;  
parameter.Value = DateTime.Parse("1666-09-02 1:00:00");  
```  
  
### <a name="datetimeoffset-example"></a>Esempio relativo a DateTimeOffset  
Il frammento di codice seguente illustra come specificare un parametro `DateTimeOffSet` con una data, un'ora e una differenza di fuso orario pari a 0.  
  
```csharp  
SqlParameter parameter = new SqlParameter();  
parameter.ParameterName = "@DateTimeOffSet";  
parameter.SqlDbType = SqlDbType.DateTimeOffSet;  
parameter.Value = DateTimeOffset.Parse("1666-09-02 1:00:00+0");  
```  
  
### <a name="addwithvalue"></a>AddWithValue  
È anche possibile specificare i parametri usando il metodo `AddWithValue` di un <xref:Microsoft.Data.SqlClient.SqlCommand>, come illustrato nel frammento di codice seguente. Tuttavia, il metodo `AddWithValue` non consente di specificare <xref:Microsoft.Data.SqlClient.SqlParameter.DbType%2A> o <xref:Microsoft.Data.SqlClient.SqlParameter.SqlDbType%2A> per il parametro.  
  
```csharp  
command.Parameters.AddWithValue(   
    "@date", DateTimeOffset.Parse("16660902"));  
```  
  
È possibile eseguire il mapping del parametro `@date` a un tipo di dati `date`, `datetime` o `datetime2` nel server. Quando si usano i nuovi tipi di dati `datetime`, è necessario impostare in modo esplicito la proprietà <xref:System.Data.SqlDbType> del parametro sul tipo di dati dell'istanza. L'uso di <xref:System.Data.SqlDbType.Variant> o l'indicazione implicita di valori di parametro può causare problemi di compatibilità con le versioni precedenti per i tipi di dati `datetime` e `smalldatetime`.  
  
Nella tabella seguente sono riportati gli elementi `SqlDbTypes` derivati tipi CLR specifici:  
  
|Tipo CLR|SqlDbType derivato|  
|--------------|------------------------|  
|Datetime|SqlDbType.DateTime|  
|TimeSpan|SqlDbType.Time|  
|DateTimeOffset|SqlDbType.DateTimeOffset|  
  
## <a name="retrieving-date-and-time-data"></a>Recupero dei dati relativi a data e ora  
Nella tabella seguente sono descritti i metodi usati per recuperare i valori di SQL Server 2008 relativi a data e ora.  
  
|Metodo SqlClient|Descrizione|  
|----------------------|-----------------|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetDateTime%2A>|Recupera il valore della colonna specificata come struttura <xref:System.DateTime>.|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetDateTimeOffset%2A>|Recupera il valore della colonna specificata come struttura <xref:System.DateTimeOffset>.|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetProviderSpecificFieldType%2A>|Restituisce il tipo che rappresenta il tipo specifico del provider sottostante per il campo. Restituisce gli stessi tipi di `GetFieldType` per i nuovi tipi di data e ora.|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetProviderSpecificValue%2A>|Recupera il valore della colonna specificata. Restituisce gli stessi tipi di `GetValue` per i nuovi tipi di data e ora.|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetProviderSpecificValues%2A>|Recupera i valori della matrice specificata.|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlString%2A>|Recupera il valore della colonna come <xref:System.Data.SqlTypes.SqlString>. Si verifica un <xref:System.InvalidCastException> se i dati non possono essere espressi come `SqlString`.|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlValue%2A>|Recupera i dati della colonna come `SqlDbType` predefinito. Restituisce gli stessi tipi di `GetValue` per i nuovi tipi di data e ora.|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlValues%2A>|Recupera i valori della matrice specificata.|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetString%2A>|Recupera il valore della colonna come stringa se Type System Version è impostata su SQL Server 2005. Si verifica un <xref:System.InvalidCastException> se non è possibile esprimere i dati come stringa.|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetTimeSpan%2A>|Recupera il valore della colonna specificata come struttura <xref:System.TimeSpan>.|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetValue%2A>|Recupera il valore della colonna specificata come tipo CLR sottostante.|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetValues%2A>|Recupera i valori colonna in una matrice.|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetSchemaTable%2A>|Restituisce un oggetto <xref:System.Data.DataTable> che descrive i metadati del set di risultati.|  
  
> [!NOTE]
>  I nuovi `SqlDbTypes` di data e ora non sono supportati per il codice eseguito In-Process in SQL Server. Se uno di questi tipi viene passato al server, verrà generata un'eccezione.  
  
## <a name="specifying-date-and-time-values-as-literals"></a>Specifica di valori di data e ora come valori letterali  
È possibile specificare i tipi di dati relativi a data e ora usando svariati formati di stringa letterale, che poi SQL Server valuta in fase di esecuzione, convertendoli in strutture di data/ora interne. SQL Server riconosce i dati di data e ora racchiusi tra virgolette singole ('). Negli esempi seguenti sono illustrati alcuni formati:  
  
- Formati di data alfabetici, ad esempio `'October 15, 2006'`.  
  
- Formati di data numerici, ad esempio `'10/15/2006'`.  
  
- Formati di stringa senza separatori, ad esempio `'20061015'`, che vengono interpretati come 15 ottobre 2006 se si usa il formato di data ISO standard.  
  
> [!NOTE]
>  È possibile trovare la documentazione completa per tutti i formati di stringa letterale e altre funzionalità dei tipi di dati per data e ora nella documentazione online di Microsoft SQL Server.  
  
I valori di ora minori di zero o maggiori o uguali a 24 ore genereranno un <xref:System.ArgumentException>.  
  
## <a name="resources-in-sql-server-2008-books-online"></a>Risorse nella documentazione online di Microsoft SQL Server 2008  
Per altre informazioni sull'uso dei valori di data e ora in SQL Server 2008, vedere le seguenti risorse nella documentazione online di SQL Server 2008.  
  
|Argomento|Descrizione|  
|-----------|-----------------|  
|[Funzioni e tipi di dati di data e ora (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=98360)|Viene fornita una panoramica di tutte le funzioni e i tipi di dati relativi a data e ora di Transact-SQL.|  
|[Uso di dati relativi a data e ora](https://go.microsoft.com/fwlink/?LinkId=98361)|Informazioni sui tipi di dati e le funzioni relativi a data e ora ed esempi per l'uso.|  
|[Tipi di dati (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=98362)|Vengono descritti i tipi di dati di sistema di SQL Server 2008.|  
  
## <a name="next-steps"></a>Passaggi successivi
- [Tipi di dati SQL Server e ADO.NET](sql-server-data-types.md)
