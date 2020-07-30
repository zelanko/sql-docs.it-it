---
title: Struttura SSVARIANT (provider OLE DB Native Client)
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ddd98b45cf44f840dfc236f8a0a1b5d809db7288
ms.sourcegitcommit: 75f767c7b1ead31f33a870fddab6bef52f99906b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/28/2020
ms.locfileid: "87331975"
---
# <a name="ssvariant-structure-in-sql-server-native-client"></a>Struttura SSVARIANT in SQL Server Native Client
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  La struttura **SSVARIANT** , definita in sqlncli. h, corrisponde a un valore DBTYPE_SQLVARIANT nel [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLEDB di Native Client.  
  
 **SSVARIANT** è un'unione discriminante. A seconda del valore del membro vt, il consumer può determinare il membro da leggere. I valori vt corrispondono ai tipi di dati [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Pertanto, la struttura **SSVARIANT** può contenere qualsiasi tipo SQL Server. Per altre informazioni sulla struttura dei dati per i tipi di OLE DB standard, vedere [Indicatori di tipo](https://go.microsoft.com/fwlink/?LinkId=122171).  
  
## <a name="remarks"></a>Commenti  
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
|bTinyIntVal|DBTYPE_UI1|**BYTE**|**VT_SS_UI1**|Supporta il **tinyint** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo di dati tinyint.|  
|sShortIntVal|DBTYPE_I2|**BREVE**|**VT_SS_I2**|Supporta il **smallint** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo di dati smallint.|  
|lIntVal|DBTYPE_I4|**LUNGO**|**VT_SS_I4**|Supporta il **int** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo di dati int.|  
|llBigIntVal|DBTYPE_I8|**LARGE_INTEGER**|**VT_SS_I8**|Supporta il **bigint** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo di dati bigint.|  
|fltRealVal|DBTYPE_R4|**float**|**VT_SS_R4**|Supporta il **real** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo di dati reale.|  
|dblFloatVal|DBTYPE_R8|**double**|**VT_SS_R8**|Supporta il **float** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo di dati float.|  
|cyMoneyVal|DBTYPE_CY|**LARGE_INTEGER**|**VT_SS_MONEY VT_SS_SMALLMONEY**|Supporta il tipo di dati **money** e **smallmoney**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|fBitVal|DBTYPE_BOOL|**VARIANT_BOOL**|**VT_SS_BIT**|Supporta il **bit** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo di dati bit.|  
|rgbGuidVal|DBTYPE_GUID|**GUID**|**VT_SS_GUID**|Supporta il **uniqueidentifier** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo di dati uniqueidentifier.|  
|numNumericVal|DBTYPE_NUMERIC|**DB_NUMERIC**|**VT_SS_NUMERIC**|Supporta il **numeric** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo di dati numeric.|  
|dDateVal|DBTYPE_DATE|**DBDATE**|**VT_SS_DATE**|Supporta il **date** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo di dati date.|  
|tsDateTimeVal|DBTYPE_DBTIMESTAMP|**DBTIMESTAMP**|**VT_SS_SMALLDATETIME VT_SS_DATETIME VT_SS_DATETIME2**|Supporta i tipi di dati **smalldatetime**, **datetime** e **datetime2**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|Time2Val|DBTYPE_DBTIME2|**DBTIME2**|**VT_SS_TIME2**|Supporta il **time** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo di dati time.<br /><br /> Include i membri indicati di seguito:<br /><br /> *tTime2Val* (**DBTIME2**)<br /><br /> *bScale* (**BYTE**) Specifica la scala per il valore *tTime2Val*.|  
|DateTimeVal|DBTYPE_DBTIMESTAMP|**DBTIMESTAMP**|**VT_SS_DATETIME2**|Supporta il **datetime2** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo di dati datetime2.<br /><br /> Include i membri indicati di seguito:<br /><br /> *tsDataTimeVal* (DBTIMESTAMP)<br /><br /> *bScale* (**BYTE**) Specifica la scala per il valore *tsDataTimeVal*.|  
|DateTimeOffsetVal|DBTYPE_DBTIMESTAMPOFSET|**DBTIMESTAMPOFFSET**|**VT_SS_DATETIMEOFFSET**|Supporta il **datetimeoffset** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo di dati DateTimeOffset.<br /><br /> Include i membri indicati di seguito:<br /><br /> *tsoDateTimeOffsetVal* (**DBTIMESTAMPOFFSET**)<br /><br /> *bScale* (**BYTE**) Specifica la scala per il valore *tsoDateTimeOffsetVal*.|  
|NCharVal|Nessun indicatore del tipo OLE DB corrispondente.|**struct _NCharVal**|**VT_SS_WVARSTRING,**<br /><br /> **VT_SS_WSTRING**|Supporta i tipi di dati **nchar** e **nvarchar**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> Include i membri indicati di seguito:<br /><br /> *sActualLength* (**SHORT**) Specifica la lunghezza effettiva per la stringa a cui punta *pwchNCharVal*. Non include lo zero finale.<br /><br /> *sMaxLength* (**SHORT**) Specifica la lunghezza massima per la stringa a cui punta *pwchNCharVal*.<br /><br /> *pwchNCharVal* (**WCHAR** \*) Puntatore alla stringa.<br /><br /> Membri non usati: *rgbReserved*, *dwReserved* e *pwchReserved*.|  
|CharVal|Nessun indicatore del tipo OLE DB corrispondente.|**struct _CharVal**|**VT_SS_STRING,**<br /><br /> **VT_SS_VARSTRING**|Supporta i tipi di dati **char** e **varchar**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> Include i membri indicati di seguito:<br /><br /> *sActualLength* (**SHORT**) Specifica la lunghezza effettiva per la stringa a cui punta *pchCharVal*. Non include lo zero finale.<br /><br /> *sMaxLength* (**SHORT**) Specifica la lunghezza massima per la stringa a cui punta *pchCharVal*.<br /><br /> *pchCharVal* (**CHAR** \*) Puntatore alla stringa.<br /><br /> Membri non utilizzati:<br /><br /> *rgbReserved*, *dwReserved* e *pwchReserved*.|  
|BinaryVal|Nessun indicatore del tipo OLE DB corrispondente.|**struct _BinaryVal**|**VT_SS_VARBINARY,**<br /><br /> **VT_SS_BINARY**|Supporta i tipi di dati **binary** e **varbinary**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> Include i membri indicati di seguito:<br /><br /> *sActualLength* (**SHORT**) Specifica la lunghezza effettiva per i dati a cui punta *prgbBinaryVal*.<br /><br /> *sMaxLength* (**SHORT**) Specifica la lunghezza massima per i dati a cui punta *prgbBinaryVal*.<br /><br /> *prgbBinaryVal* (**BYTE** \*) Puntatore ai dati binari.<br /><br /> Membro non usato: *dwReserved*.|  
|UnknownType|UNUSED|UNUSED|UNUSED|UNUSED|  
|BLOBType|UNUSED|UNUSED|UNUSED|UNUSED|  
  
## <a name="see-also"></a>Vedere anche  
 [Tipi di dati &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-data-types/data-types-ole-db.md)  
  
  
