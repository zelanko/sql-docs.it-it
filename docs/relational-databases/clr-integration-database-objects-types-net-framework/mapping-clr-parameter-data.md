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
ms.openlocfilehash: 530db4d31d3db4773713816f1b68404990997512
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68081310"
---
# <a name="mapping-clr-parameter-data"></a>Mapping dei dati dei parametri CLR
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Nella tabella seguente sono [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] elencati i tipi di dati, gli equivalenti nella Common Language Runtime (CLR [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ) per nello spazio dei nomi **System. Data. SqlTypes** e i relativi equivalenti CLR [!INCLUDE[msCoName](../../includes/msconame-md.md)] nativi nel .NET Framework.  
  
||||  
|-|-|-|  
|**Tipo di dati di SQL Server**|Tipo (in System.Data.SqlTypes o Microsoft.SqlServer.Types)|**Tipo di dati CLR (.NET Framework)**|  
|**bigint**|**SqlInt64**|**Int64, Nullable\<Int64>**|  
|**BINARY**|**SqlBytes, SqlBinary**|**Byte []**|  
|**bit**|**SqlBoolean**|**Booleano,\<valore booleano nullable>**|  
|**char**|nessuno|nessuno|  
|**cursore**|nessuno|nessuno|  
|**date**|**SqlDateTime**|**DateTime, Nullable\<DateTime>**|  
|**datetime**|**SqlDateTime**|**DateTime, Nullable\<DateTime>**|  
|**datetime2**|nessuno|**DateTime, Nullable\<DateTime>**|  
|**DATETIMEOFFSET**|**Nessuno**|**DateTimeOffset, DateTimeOffset\<Nullable>**|  
|**decimal**|**SqlDecimal**|**Decimale\<, Nullable decimale>**|  
|**float**|**SqlDouble**|**Double, Nullable\<Double>**|  
|**geography**|**SqlGeography**<br /><br /> **SqlGeography** è definito in Microsoft. SqlServer. Types. dll, che viene installato con SQL Server e può essere scaricato dal [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [Feature Pack](https://www.microsoft.com/download/details.aspx?id=52676).|nessuno|  
|**geometry**|**SqlGeometry**<br /><br /> **SqlGeometry** è definito in Microsoft. SqlServer. Types. dll, che viene installato con SQL Server e può essere scaricato dal [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [Feature Pack](https://www.microsoft.com/download/details.aspx?id=52676).|nessuno|  
|**hierarchyid**|**SqlHierarchyId**<br /><br /> **SqlHierarchyId** è definito in Microsoft. SqlServer. Types. dll, che viene installato con SQL Server e può essere scaricato dal [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [Feature Pack](https://www.microsoft.com/download/details.aspx?id=52676).|nessuno|  
|**immagine**|nessuno|nessuno|  
|**int**|**SqlInt32**|**Int32, Nullable\<Int32>**|  
|**money**|**SqlMoney**|**Decimale\<, Nullable decimale>**|  
|**nchar**|**SqlChars, SqlString**|**String, Char[]**|  
|**ntext**|nessuno|nessuno|  
|**numerico**|**SqlDecimal**|**Decimale\<, Nullable decimale>**|  
|**nvarchar**|**SqlChars, SqlString**<br /><br /> **SqlChars** rappresenta una corrispondenza migliore per il trasferimento e l'accesso ai dati e **SqlString** rappresenta una corrispondenza migliore per l'esecuzione di operazioni di stringa.|**String, Char[]**|  
|**nvarchar (1), nchar (1)**|**SqlChars, SqlString**|**Char, String, Char [], Nullable\<char>**|  
|**reale**|**SqlSingle** (l'intervallo di **SqlSingle**, tuttavia, è maggiore di **Real**)|**Single, Nullable\<Single>**|  
|**rowversion**|nessuno|**Byte []**|  
|**smallint**|**SqlInt16**|**Int16, Nullable\<Int16>**|  
|**SMALLMONEY**|**SqlMoney**|**Decimale\<, Nullable decimale>**|  
|**sql_variant**|nessuno|**Object**|  
|**tavolo**|nessuno|nessuno|  
|**text**|nessuno|nessuno|  
|**time**|nessuno|**TimeSpan, Nullable\<TimeSpan>**|  
|**timestamp**|nessuno|nessuno|  
|**tinyint**|**SqlByte**|**Byte, Nullable\<byte>**|  
|**uniqueidentifier**|**SqlGuid**|**GUID, GUID\<Nullable>**|  
|**Tipo definito dall'utente (UDT)**|nessuno|La stessa classe associata al tipo definito dall'utente (UDT) nello stesso assembly o un assembly dipendente.|  
|**varbinary**|**SqlBytes, SqlBinary**|**Byte []**|  
|**varbinary (1), Binary (1)**|**SqlBytes, SqlBinary**|**byte, byte [], Nullable\<byte>**|  
|**varchar**|nessuno|nessuno|  
|**XML**|**SqlXml**|nessuno|  
  
## <a name="automatic-data-type-conversion-with-out-parameters"></a>Conversione automatica dei tipi di dati con parametri Out  
 Un metodo CLR può restituire informazioni al codice o al programma chiamante contrassegnando un parametro di input con il modificatore **out** (Microsoft Visual C#) o ** \<out () > ByRef** (Microsoft Visual Basic) se il parametro di input è un tipo di dati CLR nel sistema. lo spazio dei nomi **Data. SqlTypes** e il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] programma chiamante specificano il tipo di dati equivalente come parametro di input. una conversione del tipo viene eseguita automaticamente quando il metodo CLR restituisce il tipo di dati.  
  
 Il stored procedure CLR seguente, ad esempio, include un parametro di input di **SqlInt32** tipo di dati CLR contrassegnato con **out** (C#) o ** \<out () > ByRef** (Visual Basic):  
  
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
  
 Dopo che l'assembly è stato compilato e creato nel database, il stored procedure viene creato [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in con l'istruzione Transact-SQL seguente, che [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] specifica un tipo di dati **int** come parametro di output:  
  
```  
CREATE PROCEDURE PriceSum (@sum int OUTPUT)  
AS EXTERNAL NAME TestStoredProc.StoredProcedures.PriceSum  
```  
  
 Quando viene chiamato il stored procedure CLR, il tipo di dati **SqlInt32** viene convertito automaticamente in un tipo di dati **int** e restituito al programma chiamante.  
  
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
|Aggiunta dei tipi **SqlGeography**, **SqlGeometry**e **SqlHierarchyId** alla tabella di mapping.|  
  
## <a name="see-also"></a>Vedere anche  
 [Tipi di dati di SQL Server in .NET Framework](../../relational-databases/clr-integration-database-objects-types-net-framework/sql-server-data-types-in-the-net-framework.md)  
  
  
