---
title: Mapping dei dati dei parametri CLR | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 9c4697d2dcbad80d1da0fd8ed6c81750ac90695b
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52534120"
---
# <a name="mapping-clr-parameter-data"></a>Mapping dei dati dei parametri CLR
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  La tabella seguente elenca [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipi di dati, i relativi equivalenti in common language runtime (CLR) per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nel **System.Data.SqlTypes** dello spazio dei nomi e gli equivalenti CLR nativi nel [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET framework.  
  
||||  
|-|-|-|  
|**Tipo di dati di SQL Server**|Tipo (in System.Data.SqlTypes o Microsoft.SqlServer.Types)|**Tipo di dati CLR (.NET Framework)**|  
|**bigint**|**SqlInt64**|**Int64, Nullable\<Int64 >**|  
|**binary**|**SqlBytes, SqlBinary**|**Byte[]**|  
|**bit**|**SqlBoolean**|**Booleano, che ammette valori null\<booleano >**|  
|**char**|None|None|  
|**cursor**|None|None|  
|**data**|**SqlDateTime**|**Data/ora, che ammette valori null\<DateTime >**|  
|**datetime**|**SqlDateTime**|**Data/ora, che ammette valori null\<DateTime >**|  
|**datetime2**|None|**Data/ora, che ammette valori null\<DateTime >**|  
|**DATETIMEOFFSET**|**None**|**DateTimeOffset, Nullable\<DateTimeOffset >**|  
|**decimal**|**SqlDecimal**|**Decimal, Nullable\<Decimal >**|  
|**float**|**SqlDouble**|**Double, che ammette valori null\<Double >**|  
|**geography**|**SqlGeography**<br /><br /> **SqlGeography** definito in Microsoft.SqlServer.Types.dll, che viene installato con SQL Server e può essere scaricato dal [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [feature pack di](https://www.microsoft.com/download/details.aspx?id=52676).|None|  
|**geometry**|**SqlGeometry**<br /><br /> **SqlGeometry** definito in Microsoft.SqlServer.Types.dll, che viene installato con SQL Server e può essere scaricato dal [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [feature pack di](https://www.microsoft.com/download/details.aspx?id=52676).|None|  
|**hierarchyid**|**SqlHierarchyId**<br /><br /> **SqlHierarchyId** definito in Microsoft.SqlServer.Types.dll, che viene installato con SQL Server e può essere scaricato dal [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [feature pack di](https://www.microsoft.com/download/details.aspx?id=52676).|None|  
|**image**|None|None|  
|**int**|**SqlInt32**|**Int32, che ammette valori null\<Int32 >**|  
|**money**|**SqlMoney**|**Decimal, Nullable\<Decimal >**|  
|**nchar**|**SqlChars, SqlString**|**String, Char]**|  
|**ntext**|None|None|  
|**numeric**|**SqlDecimal**|**Decimal, Nullable\<Decimal >**|  
|**nvarchar**|**SqlChars, SqlString**<br /><br /> **SQLChars** è una corrispondenza migliore per il trasferimento dei dati e degli accessi, e **SQLString** è una corrispondenza migliore per l'esecuzione di operazioni sulle stringhe.|**String, Char]**|  
|**nvarchar(1, nchar (1)**|**SqlChars, SqlString**|**Char, String, Char [], Nullable\<char >**|  
|**real**|**SqlSingle** (l'intervallo di **SqlSingle**, tuttavia, è più grande **reale**)|**Singolo, ammette valori null\<Single >**|  
|**rowversion**|None|**Byte[]**|  
|**smallint**|**SqlInt16**|**Int16, Nullable\<Int16 >**|  
|**smallmoney**|**SqlMoney**|**Decimal, Nullable\<Decimal >**|  
|**sql_variant**|None|**Oggetto**|  
|**table**|None|None|  
|**text**|None|None|  
|**time**|None|**Intervallo di tempo, che ammette valori null\<TimeSpan >**|  
|**timestamp**|None|None|  
|**tinyint**|**SqlByte**|**Byte, che ammette valori null\<Byte >**|  
|**uniqueidentifier**|**SqlGuid**|**GUID, che ammette valori null\<Guid >**|  
|**Type(UDT) definite dall'utente**|None|La stessa classe associata al tipo definito dall'utente (UDT) nello stesso assembly o un assembly dipendente.|  
|**varbinary**|**SqlBytes, SqlBinary**|**Byte[]**|  
|**varbinary(1), binary(1)**|**SqlBytes, SqlBinary**|**byte, Byte [], Nullable\<byte >**|  
|**varchar**|None|None|  
|**xml**|**SqlXml**|None|  
  
## <a name="automatic-data-type-conversion-with-out-parameters"></a>Conversione automatica dei tipi di dati con parametri Out  
 Un metodo CLR può restituire informazioni al codice o programma chiamante contrassegnando un parametro di input con il **out** modificatore (Microsoft Visual c#) o  **\<out () > ByRef** (Microsoft Visual Basic) Se il parametro di input è un tipo di dati CLR di **System.Data.SqlTypes** dello spazio dei nomi e il programma chiamante specifica equivalente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo di dati come parametro di input, una conversione del tipo viene generato automaticamente Quando il metodo CLR restituisce il tipo di dati.  
  
 Ad esempio, la seguente stored procedure CLR ha un parametro di input **SqlInt32** tipo di dati CLR che è contrassegnato con **out** (c#) o  **\<out () > ByRef** ( Visual Basic):  
  
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
  
 Dopo che l'assembly è compilato e creato nel database, la stored procedure viene creata nella [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con il seguente Transact-SQL, che consente di specificare un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo di dati di **int** come parametro di OUTPUT:  
  
```  
CREATE PROCEDURE PriceSum (@sum int OUTPUT)  
AS EXTERNAL NAME TestStoredProc.StoredProcedures.PriceSum  
```  
  
 Quando CLR stored procedure viene chiamata, il **SqlInt32** tipo di dati viene convertito automaticamente in un **int** tipo di dati e restituito al programma chiamante.  
  
 Non tutti i tipi di dati CLR possono essere convertiti automaticamente nei tipi dei dati [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] equivalenti tramite un parametro out. Nella seguente tabella vengono descritte queste eccezioni.  
  
|||  
|-|-|  
|**Tipo di dati CLR (SQL Server)**|**Tipo di dati di SQL Server**|  
|**Decimale**|SMALLMONEY|  
|**SqlMoney**|SMALLMONEY|  
|**Decimale**|money|  
|**DateTime**|smalldatetime|  
|**SQLDateTime**|smalldatetime|  
  
## <a name="change-history"></a>Cronologia modifiche  
  
|Contenuto aggiornato|  
|---------------------|  
|Aggiunti **SqlGeography**, **SqlGeometry**, e **SqlHierarchyId** tipi alla tabella di mapping.|  
  
## <a name="see-also"></a>Vedere anche  
 [Tipi di dati di SQL Server in .NET Framework](../../relational-databases/clr-integration-database-objects-types-net-framework/sql-server-data-types-in-the-net-framework.md)  
  
  
