---
title: Mapping dei dati dei parametri CLR Documenti Microsoft
description: In questo articolo sono elencati i tipi di dati di Microsoft SQL Server, gli equivalenti in CLR per SQL Server e gli equivalenti CLR nativi in .NET Framework.
ms.custom: ''
ms.date: 08/01/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- SqlBinary data type
- SqlInt16 data type
- SqlMoney data type
- SqlString data type
- SqlSingle data type
- data types [CLR integration]
- SqlInt64 data type
- SqlDateTime data type
- SqlXml data type
- SqlBoolean data type
- SqlDecimal data type
- SqlBytes data type
- mapping data types [CLR integration]
- SqlChars data type
- SqlInt32 data type
ms.assetid: 89b43ee9-b9ad-4281-a4bf-c7c8d116daa2
author: rothja
ms.author: jroth
ms.openlocfilehash: 360a94229b107e9f24bb2a769157c75cdeb3c143
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/16/2020
ms.locfileid: "81488461"
---
# <a name="mapping-clr-parameter-data"></a>Mapping dei dati dei parametri CLR
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Nella tabella [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] seguente sono elencati i tipi di dati, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] i relativi equivalenti in Common Language Runtime (CLR) per lo spazio dei nomi **System.Data.SqlTypes** e i relativi equivalenti CLR nativi in [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework.  
  
||||  
|-|-|-|  
|**Tipo di dati di SQL ServerSQL Server data type**|Tipo (in System.Data.SqlTypes o Microsoft.SqlServer.Types)|**Tipo di dati CLR (.NET Framework)**|  
|**bigint**|**SqlInt64**|**Int64,>\<Int64 nullableInt64>**|  
|**binary**|**SqlBytes, SqlBinary**|**Byte[]**|  
|**bit**|**SqlBoolean**|**Valore booleano,>booleano nullableBoolean, Nullable\<Boolean>**|  
|**char**|nessuno|nessuno|  
|**cursor**|nessuno|nessuno|  
|**date**|**Sqldatetime**|**DateTime,>\<Nullable DateTime**|  
|**datetime**|**Sqldatetime**|**DateTime,>\<Nullable DateTime**|  
|**datetime2**|nessuno|**DateTime,>\<Nullable DateTime**|  
|**Datetimeoffset**|**Nessuno**|**DateTimeOffset,>\<Nullable DateTimeOffset**|  
|**decimal**|**Sqldecimal**|**>decimali\<nullable Decimal**|  
|**float**|**SqlDouble**|**Doppio, nullable\<Double>**|  
|**Geografia**|**SqlGeography**<br /><br /> **SqlGeography** è definito in Microsoft.SqlServer.Types.dll, che viene installato con [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] SQL Server e può essere scaricato dal [Feature Pack](https://www.microsoft.com/download/details.aspx?id=52676).|nessuno|  
|**Geometria**|**SqlGeometry**<br /><br /> **SqlGeometry** è definito in Microsoft.SqlServer.Types.dll, installato con SQL Server [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e può essere scaricato dal [Feature Pack.](https://www.microsoft.com/download/details.aspx?id=52676)|nessuno|  
|**hierarchyid**|**SqlHierarchyId**<br /><br /> **SqlHierarchyId** è definito in Microsoft.SqlServer.Types.dll, installato con SQL Server [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e può essere scaricato dal [Feature Pack.](https://www.microsoft.com/download/details.aspx?id=52676)|nessuno|  
|**image**|nessuno|nessuno|  
|**int**|**SqlInt32**|**Int32, int32 nullable\<int32>**|  
|**money**|**Sqlmoney**|**>decimali\<nullable Decimal**|  
|**nchar**|**SqlChars, SqlString**|**String, Char[]**|  
|**ntext**|nessuno|nessuno|  
|**numeric**|**Sqldecimal**|**>decimali\<nullable Decimal**|  
|**nvarchar**|**SqlChars, SqlString**<br /><br /> **SQLChars** è una corrispondenza migliore per il trasferimento e l'accesso ai dati e SQLString è una corrispondenza migliore per l'esecuzione di operazioni String.SQLChars is a better match for data transfer and access, and **SQLString** is a better match for performing String operations.|**String, Char[]**|  
|**nvarchar(1), nchar(1)**|**SqlChars, SqlString**|**Char, String, Char[],\<nullable char>**|  
|**real**|**SqlSingle** (l'intervallo di **SqlSingle**, tuttavia, è maggiore di **real**)|**Singolo, nullable\<Single>**|  
|**rowversion**|nessuno|**Byte[]**|  
|**smallint**|**SqlInt16**|**Int16,>\<Int16 nullableInt16Int16>**|  
|**smallmoney**|**Sqlmoney**|**>decimali\<nullable Decimal**|  
|**sql_variant**|nessuno|**Oggetto**|  
|**tabella**|nessuno|nessuno|  
|**text**|nessuno|nessuno|  
|**time**|nessuno|**TimeSpan,>\<Nullable TimeSpan**|  
|**timestamp**|nessuno|nessuno|  
|**tinyint**|**SqlByte**|**Byte, byte\<nullable>**|  
|**uniqueidentifier**|**Sqlguid**|**Guid, Nullable\<Guid>**|  
|**Tipo definito dall'utente (UDT)**|nessuno|La stessa classe associata al tipo definito dall'utente (UDT) nello stesso assembly o un assembly dipendente.|  
|**varbinary**|**SqlBytes, SqlBinary**|**Byte[]**|  
|**varbinary(1), binary(1)**|**SqlBytes, SqlBinary**|**byte, Byte[],\<byte nullable>**|  
|**varchar**|nessuno|nessuno|  
|**xml**|**Sqlxml**|nessuno|  
  
## <a name="automatic-data-type-conversion-with-out-parameters"></a>Conversione automatica dei tipi di dati con parametri Out  
 Un metodo CLR può restituire informazioni al codice o al programma chiamante contrassegnando un parametro di input con il modificatore **out** (Microsoft Visual C) o ** \<Out()> ByRef** (Microsoft Visual Basic) Se il parametro di input è un tipo di dati CLR nello spazio dei nomi **System.Data.SqlTypes** e il programma chiamante specifica il tipo di dati equivalente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] come parametro di input, viene eseguita automaticamente una conversione del tipo quando il metodo CLR restituisce il tipo di dati.  
  
 Ad esempio, la seguente stored procedure CLR dispone di un parametro di input del tipo di dati CLR **SqlInt32** contrassegnato con **out** (C) o ** \<Out()> ByRef** (Visual Basic):  
  
```csharp  
[Microsoft.SqlServer.Server.SqlProcedure]  
public static void PriceSum(out SqlInt32 value)  
{ ... }  
```  
  
```vb  
\<Microsoft.SqlServer.Server.SqlProcedure> _  
Public Shared Sub PriceSum( \<Out()> ByRef value As SqlInt32)  
...  
End Sub  
```  
  
 Dopo aver compilato e creato l'assembly nel database, la stored procedure viene creata con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] il transact-SQLTransact-SQL seguente, che specifica un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo di dati **int** come parametro OUTPUT:  
  
```  
CREATE PROCEDURE PriceSum (@sum int OUTPUT)  
AS EXTERNAL NAME TestStoredProc.StoredProcedures.PriceSum  
```  
  
 Quando viene chiamata la stored procedure CLR, il tipo di dati **SqlInt32** viene convertito automaticamente in un tipo di dati **int** e restituito al programma chiamante.  
  
 Non tutti i tipi di dati CLR possono essere convertiti automaticamente nei tipi dei dati [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] equivalenti tramite un parametro out. Nella seguente tabella vengono descritte queste eccezioni.  
  
|||  
|-|-|  
|**Tipo di dati CLR (SQL Server)**|**Tipo di dati di SQL ServerSQL Server data type**|  
|**Decimale**|SMALLMONEY|  
|**Sqlmoney**|SMALLMONEY|  
|**Decimal**|money|  
|**Datetime**|smalldatetime|  
|**Sqldatetime**|smalldatetime|  
  
## <a name="change-history"></a>Cronologia modifiche  
  
|Contenuto aggiornato|  
|---------------------|  
|Aggiunti i tipi **SqlGeography**, **SqlGeometry**e **SqlHierarchyId** alla tabella di mapping.|  
  
## <a name="see-also"></a>Vedere anche  
 [Tipi di dati di SQL Server in .NET Framework](../../relational-databases/clr-integration-database-objects-types-net-framework/sql-server-data-types-in-the-net-framework.md)  
  
  
