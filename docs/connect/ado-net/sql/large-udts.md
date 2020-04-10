---
title: Tipi definiti dall'utente di grandi dimensioni
description: Descrive come recuperare i dati dai tipi definiti dall'utente con valori di grandi dimensioni introdotti in SQL Server 2008.
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: 420ae24e-762b-4e09-b4c3-2112c470ee49
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-kaywon
ms.openlocfilehash: 06abbc88d80dffba14a48d82561dd4db1a2eb68e
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/08/2020
ms.locfileid: "80924331"
---
# <a name="large-udts"></a>Tipi definiti dall'utente di grandi dimensioni

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

I tipi definiti dall'utente (UDT) consentono agli sviluppatori di estendere il sistema di tipi scalare del server archiviando oggetti Common Language Runtime (CLR) in un database di SQL Server. I tipi definiti dall'utente possono contenere più elementi e avere comportamenti che, a differenza dei tradizionali tipi di dati alias, sono costituiti da un solo tipo di dati di sistema di SQL Server.  
  
In precedenza, i tipi definiti dall'utente erano limitati a una dimensione massima di 8 kilobyte. In SQL Server 2008 questa limitazione è stata rimossa per i tipi definiti dall'utente con il formato <xref:Microsoft.Data.SqlClient.Server.Format.UserDefined>.  
  
Per la documentazione completa relativa ai tipi definiti dall'utente, vedere [Tipi CLR definiti dall'utente](https://go.microsoft.com/fwlink/?LinkId=98366) nella documentazione online di SQL Server.
  
## <a name="retrieving-udt-schemas-using-getschema"></a>Recupero di schemi UDT con GetSchema  
Il metodo <xref:Microsoft.Data.SqlClient.SqlConnection.GetSchema%2A> di <xref:Microsoft.Data.SqlClient.SqlConnection> restituisce le informazioni sullo schema del database in un <xref:System.Data.DataTable>.
  
### <a name="getschematable-column-values-for-udts"></a>Valori colonna GetSchemaTable per i tipi definiti dall'utente  
Il metodo <xref:Microsoft.Data.SqlClient.SqlDataReader.GetSchemaTable%2A> di un <xref:Microsoft.Data.SqlClient.SqlDataReader> restituisce un <xref:System.Data.DataTable> che descrive i metadati della colonna. Nella tabella seguente vengono descritte le differenze tra SQL Server 2005 e SQL Server 2008 riguardo ai metadati delle colonne per i tipi definiti dall'utente di grandi dimensioni.  
  
|Colonna SqlDataReader|SQL Server 2005|SQL Server 2008 e versioni successive|  
|--------------------------|---------------------|-------------------------------|  
|`ColumnSize`|Variabile|Variabile|  
|`NumericPrecision`|255|255|  
|`NumericScale`|255|255|  
|`DataType`|`Byte[]`|Istanza UDT|  
|`ProviderSpecificDataType`|`SqlTypes.SqlBinary`|Istanza UDT|  
|`ProviderType`|21 (`SqlDbType.VarBinary`)|29 (`SqlDbType.Udt`)|  
|`NonVersionedProviderType`|29 (`SqlDbType.Udt`)|29 (`SqlDbType.Udt`)|  
|`DataTypeName`|`SqlDbType.VarBinary`|Nome in tre parti specificato come *Database.SchemaName.TypeName*.|  
|`IsLong`|Variabile|Variabile|  
  
## <a name="sqldatareader-considerations"></a>Considerazioni su SqlDataReader  
<xref:Microsoft.Data.SqlClient.SqlDataReader> è stato esteso a partire da SQL Server 2008 per supportare il recupero di valori UDT di grandi dimensioni. La modalità di elaborazione dei valori UDT di grandi dimensioni da parte di un <xref:Microsoft.Data.SqlClient.SqlDataReader> dipende dalla versione di SQL Server in uso, nonché dall'elemento `Type System Version` specificato nella stringa di connessione. Per altre informazioni, vedere <xref:Microsoft.Data.SqlClient.SqlConnection.ConnectionString%2A>.  
  
I metodi seguenti di <xref:Microsoft.Data.SqlClient.SqlDataReader> restituiranno un <xref:System.Data.SqlTypes.SqlBinary> anziché un tipo definito dall'utente quando `Type System Version` è impostato su SQL Server 2005:  
  
- <xref:Microsoft.Data.SqlClient.SqlDataReader.GetProviderSpecificFieldType%2A>  
  
- <xref:Microsoft.Data.SqlClient.SqlDataReader.GetProviderSpecificValue%2A>  
  
- <xref:Microsoft.Data.SqlClient.SqlDataReader.GetProviderSpecificValues%2A>  
  
- <xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlValue%2A>  
  
- <xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlValues%2A>  
  
I metodi seguenti restituiranno una matrice di `Byte[]` anziché un tipo definito dall'utente quando `Type System Version` è impostato su SQL Server 2005:  
  
- <xref:Microsoft.Data.SqlClient.SqlDataReader.GetValue%2A>  
  
- <xref:Microsoft.Data.SqlClient.SqlDataReader.GetValues%2A>  
  
Si noti che non viene eseguita alcuna conversione per la versione corrente di ADO.NET.  
  
## <a name="specifying-sqlparameters"></a>Specifica di SqlParameter  
Le proprietà <xref:Microsoft.Data.SqlClient.SqlParameter> seguenti sono state estese per funzionare con i tipi definiti dall'utente di grandi dimensioni.  
  
|Proprietà SqlParameter|Descrizione|  
|---------------------------|-----------------|  
|<xref:Microsoft.Data.SqlClient.SqlParameter.Value%2A>|Ottiene o imposta un oggetto che rappresenta il valore del parametro. Il valore predefinito è Null. La proprietà può essere `SqlBinary`, `Byte[]` o un oggetto gestito.|  
|<xref:Microsoft.Data.SqlClient.SqlParameter.SqlValue%2A>|Ottiene o imposta un oggetto che rappresenta il valore del parametro. Il valore predefinito è Null. La proprietà può essere `SqlBinary`, `Byte[]` o un oggetto gestito.|  
|<xref:Microsoft.Data.SqlClient.SqlParameter.Size%2A>|Ottiene o imposta la dimensione del valore del parametro da risolvere. Il valore predefinito è 0. La proprietà può essere un numero intero che rappresenta la dimensione del valore del parametro. Per gli UDT di grandi dimensioni, può trattarsi delle dimensioni effettive dell'UDT oppure di -1 per i tipi sconosciuti.|  
  
## <a name="retrieving-data-example"></a>Esempio di recupero dati  
Il frammento di codice seguente illustra come recuperare dati UDT di grandi dimensioni. La variabile `connectionString` presuppone una connessione valida a un database SQL Server e la variabile `commandString` presuppone un'istruzione SELECT valida con la colonna chiave primaria elencata per prima.  
  
```csharp  
using (SqlConnection connection = new SqlConnection(   
    connectionString, commandString))  
{  
  connection.Open();  
  SqlCommand command = new SqlCommand(commandString);  
  SqlDataReader reader = command.ExecuteReader();  
  while (reader.Read())  
  {  
    // Retrieve the value of the Primary Key column.  
    int id = reader.GetInt32(0);  
  
    // Retrieve the value of the UDT.  
    LargeUDT udt = (LargeUDT)reader[1];  
  
    // You can also use GetSqlValue and GetValue.  
    // LargeUDT udt = (LargeUDT)reader.GetSqlValue(1);  
    // LargeUDT udt = (LargeUDT)reader.GetValue(1);  
  
    Console.WriteLine(  
     "ID={0} LargeUDT={1}", id, udt);  
  }  
reader.close  
}  
```  
  
## <a name="next-steps"></a>Passaggi successivi
- [Dati binari e con valori di grandi dimensioni di SQL Server](sql-server-binary-large-value-data.md)
 