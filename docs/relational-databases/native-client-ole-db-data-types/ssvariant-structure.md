---
title: Struttura SSVARIANT | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
f1_keywords:
- SSVARIANT
helpviewer_keywords:
- SSVARIANT struct
ms.assetid: d13c6aa6-bd49-467a-9093-495df8f1e2d9
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2298bbbfcdb4c0245d9b932152c21f39d7e884f0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "73770741"
---
# <a name="ssvariant-structure"></a>Struttura SSVARIANT
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  La struttura **SSVARIANT** , definita in sqlncli. h, corrisponde a un valore DBTYPE_SQLVARIANT nel provider OLEDB di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
 **SSVARIANT** è un'unione discriminante. A seconda del valore del membro vt, il consumer può determinare il membro da leggere. I valori vt corrispondono ai tipi di dati [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Pertanto, la struttura **SSVARIANT** può contenere qualsiasi tipo SQL Server. Per ulteriori informazioni sulla struttura dei dati per i tipi di OLE DB standard, vedere [indicatori di tipo](https://go.microsoft.com/fwlink/?LinkId=122171).  
  
## <a name="remarks"></a>Osservazioni  
 Quando DataTypeCompat==80, diversi sottotipi di **SSVARIANT** diventano stringhe. I valori vt seguenti verranno ad esempio visualizzati in **SSVARIANT** come VT_SS_WVARSTRING:  
  
-   VT_SS_DATETIMEOFFSET  
  
-   VT_SS_DATETIME2  
  
-   VT_SS_TIME2  
  
-   VT_SS_DATE  
  
 Quando DateTypeCompat == 0, questi tipi vengono visualizzati nel formato nativo.  
  
 Per ulteriori informazioni su SSPROP_INIT_DATATYPECOMPATIBILITY, vedere [utilizzo delle parole chiave delle stringhe di connessione con SQL Server Native Client](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
 Il file sqlncli. h contiene macro di accesso Variant che semplificano la dereferenziazione dei tipi di membro nella struttura **SSVARIANT** . Un esempio è rappresentato da V_SS_DATETIMEOFFSET, che è possibile utilizzare come indicato di seguito:  
  
```  
memcpy(&V_SS_DATETIMEOFFSET(pssVar).tsoDateTimeOffsetVal, pDTO, cbNative);  
V_SS_DATETIMEOFFSET(pssVar).bScale = bScale;  
```  
  
 Per il set completo di macro di accesso per ogni membro della struttura **SSVARIANT** , fare riferimento al file sqlncli. Hi.  
  
 Nella tabella seguente vengono descritti i membri della struttura **SSVARIANT**:  
  
|Membro|Indicatore del tipo OLE DB|Tipo di dati C di OLE DB|valore vt|Commenti|  
|------------|---------------------------|------------------------|--------------|--------------|  
|vt|SSVARTYPE|||Specifica il tipo di valore contenuto nella struttura **SSVARIANT**.|  
|bTinyIntVal|DBTYPE_UI1|**BYTE**|**VT_SS_UI1**|Supporta il tipo di dati **tinyint** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|sShortIntVal|DBTYPE_I2|**BREVE**|**VT_SS_I2**|Supporta il tipo di dati **smallint** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|lIntVal|DBTYPE_I4|**LUNGO**|**VT_SS_I4**|Supporta il tipo di dati **int** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|llBigIntVal|DBTYPE_I8|**LARGE_INTEGER**|**VT_SS_I8**|Supporta il tipo di dati **bigint** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|fltRealVal|DBTYPE_R4|**float**|**VT_SS_R4**|Supporta il tipo di dati **reale** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|dblFloatVal|DBTYPE_R8|**double**|**VT_SS_R8**|Supporta il tipo di dati **float** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|cyMoneyVal|DBTYPE_CY|**LARGE_INTEGER**|**VT_SS_MONEY VT_SS_SMALLMONEY**|Supporta i tipi di dati **Money** e **smallmoney** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|fBitVal|DBTYPE_BOOL|**VARIANT_BOOL**|**VT_SS_BIT**|Supporta il tipo di dati **bit** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|rgbGuidVal|DBTYPE_GUID|**GUID**|**VT_SS_GUID**|Supporta il tipo di dati **uniqueidentifier** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|numNumericVal|DBTYPE_NUMERIC|**DB_NUMERIC**|**VT_SS_NUMERIC**|Supporta il tipo di dati **numeric** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|dDateVal|DBTYPE_DATE|**DBDATE**|**VT_SS_DATE**|Supporta il tipo di dati **date** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|tsDateTimeVal|DBTYPE_DBTIMESTAMP|**DBTIMESTAMP**|**VT_SS_SMALLDATETIME VT_SS_DATETIME VT_SS_DATETIME2**|Supporta i tipi di dati **smalldatetime**, **DateTime**e **datetime2** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|Time2Val|DBTYPE_DBTIME2|**DBTIME2**|**VT_SS_TIME2**|Supporta il tipo di dati **Time** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .<br /><br /> Include i membri indicati di seguito:<br /><br /> *tTime2Val* (**DBTIME2**)<br /><br /> *bScale* (**byte**) specifica la scala per il valore *tTime2Val* .|  
|DateTimeVal|DBTYPE_DBTIMESTAMP|**DBTIMESTAMP**|**VT_SS_DATETIME2**|Supporta il tipo di dati **datetime2** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .<br /><br /> Include i membri indicati di seguito:<br /><br /> *tsDataTimeVal* (DBTIMESTAMP)<br /><br /> *bScale* (**byte**) specifica la scala per il valore *tsDataTimeVal* .|  
|DateTimeOffsetVal|DBTYPE_DBTIMESTAMPOFSET|**DBTIMESTAMPOFFSET**|**VT_SS_DATETIMEOFFSET**|Supporta il tipo di dati **DateTimeOffset** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .<br /><br /> Include i membri indicati di seguito:<br /><br /> *tsoDateTimeOffsetVal* (**DBTIMESTAMPOFFSET**)<br /><br /> *bScale* (**byte**) specifica la scala per il valore *tsoDateTimeOffsetVal* .|  
|NCharVal|Nessun indicatore del tipo OLE DB corrispondente.|**_NCharVal struct**|**VT_SS_WVARSTRING,**<br /><br /> **VT_SS_WSTRING**|Supporta i tipi di dati **nchar** e **nvarchar** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .<br /><br /> Include i membri indicati di seguito:<br /><br /> *sActualLength* (**short**) specifica la lunghezza effettiva per la stringa a cui punta *punta pwchNCharVal* . Non include lo zero finale.<br /><br /> *sMaxLength* (**short**) specifica la lunghezza massima per la stringa a cui punta *punta pwchNCharVal* .<br /><br /> *punta pwchNCharVal* (**WCHAR** \*) puntatore alla stringa.<br /><br /> Membri non utilizzati: *rgbReserved*, *dwReserved*e *pwchReserved*.|  
|CharVal|Nessun indicatore del tipo OLE DB corrispondente.|**_CharVal struct**|**VT_SS_STRING,**<br /><br /> **VT_SS_VARSTRING**|Supporta i tipi di dati **char** e **varchar** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .<br /><br /> Include i membri indicati di seguito:<br /><br /> *sActualLength* (**short**) specifica la lunghezza effettiva per la stringa a cui punta *punta pchCharVal* . Non include lo zero finale.<br /><br /> *sMaxLength* (**short**) specifica la lunghezza massima per la stringa a cui punta *punta pchCharVal* .<br /><br /> *punta pchCharVal* (**char** \*) puntatore alla stringa.<br /><br /> Membri non utilizzati:<br /><br /> *rgbReserved*, *dwReserved*e *pwchReserved*.|  
|BinaryVal|Nessun indicatore del tipo OLE DB corrispondente.|**_BinaryVal struct**|**VT_SS_VARBINARY,**<br /><br /> **VT_SS_BINARY**|Supporta i tipi di dati **Binary** e **varbinary** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .<br /><br /> Include i membri indicati di seguito:<br /><br /> *sActualLength* (**short**) specifica la lunghezza effettiva per i dati a cui punta *punta prgbBinaryVal* .<br /><br /> *sMaxLength* (**short**) specifica la lunghezza massima per i dati a cui punta *punta prgbBinaryVal* .<br /><br /> puntatore *punta prgbBinaryVal* (**byte** \*) ai dati binari.<br /><br /> Membro non usato: *dwReserved*.|  
|UnknownType|UNUSED|UNUSED|UNUSED|UNUSED|  
|BLOBType|UNUSED|UNUSED|UNUSED|UNUSED|  
  
## <a name="see-also"></a>Vedere anche  
 [Tipi di dati &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-data-types/data-types-ole-db.md)  
  
  
