---
title: Struttura SSVARIANT | Microsoft Docs
description: Struttura SSVARIANT nel driver OLE DB per SQL Server
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
f1_keywords:
- SSVARIANT
helpviewer_keywords:
- SSVARIANT struct
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 09ff4af7026ce75a8668db22910e550dc0c72857
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67995165"
---
# <a name="ssvariant-structure"></a>Struttura SSVARIANT
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  La struttura **SSVARIANT** , definita in msoledbsql. h, corrisponde a un valore DBTYPE_SQLVARIANT nel driver OLE DB per SQL Server.  
  
 **SSVARIANT** è un'unione discriminante. A seconda del valore del membro vt, il consumer può determinare il membro da leggere. I valori vt corrispondono ai tipi di dati [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Pertanto, la struttura **SSVARIANT** può contenere qualsiasi tipo SQL Server. Per ulteriori informazioni sulla struttura dei dati per i tipi di OLE DB standard, vedere [indicatori di tipo](https://go.microsoft.com/fwlink/?LinkId=122171).  
  
## <a name="remarks"></a>Remarks  
 Quando DataTypeCompat==80, diversi sottotipi di **SSVARIANT** diventano stringhe. I valori vt seguenti verranno ad esempio visualizzati in **SSVARIANT** come VT_SS_WVARSTRING:  
  
-   VT_SS_DATETIMEOFFSET  
  
-   VT_SS_DATETIME2  
  
-   VT_SS_TIME2  
  
-   VT_SS_DATE  
  
 Quando DateTypeCompat == 0, questi tipi vengono visualizzati nel formato nativo.  
  
 Per ulteriori informazioni su SSPROP_INIT_DATATYPECOMPATIBILITY, vedere [utilizzo delle parole chiave delle stringhe di connessione con Driver OLE DB per SQL Server](../../oledb/applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md).  
  
 Il file msoledbsql.h contiene macro di accesso di tipo Variant che semplificano la risoluzione dei riferimenti ai tipi di membri nella struttura **SSVARIANT**. Un esempio è rappresentato da V_SS_DATETIMEOFFSET, che è possibile utilizzare come indicato di seguito:  
  
```  
memcpy(&V_SS_DATETIMEOFFSET(pssVar).tsoDateTimeOffsetVal, pDTO, cbNative);  
V_SS_DATETIMEOFFSET(pssVar).bScale = bScale;  
```  
  
 Per il set completo di macro di accesso per ogni membro della struttura **SSVARIANT** , fare riferimento al file msoledbsql. h.  
  
 Nella tabella seguente vengono descritti i membri della struttura **SSVARIANT**:  
  
|Membro|Indicatore del tipo OLE DB|Tipo di dati C di OLE DB|valore vt|Commenti|  
|------------|---------------------------|------------------------|--------------|--------------|  
|vt|SSVARTYPE|||Specifica il tipo di valore contenuto nella struttura **SSVARIANT**.|  
|bTinyIntVal|DBTYPE_UI1|**BYTE**|**VT_SS_UI1**|Supporta il tipo di dati **tinyint** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .|  
|sShortIntVal|DBTYPE_I2|**SHORT**|**VT_SS_I2**|Supporta il tipo di dati **smallint** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .|  
|lIntVal|DBTYPE_I4|**LONG**|**VT_SS_I4**|Supporta il tipo di dati **int** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .|  
|llBigIntVal|DBTYPE_I8|**LARGE_INTEGER**|**VT_SS_I8**|Supporta il tipo di dati **bigint** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .|  
|fltRealVal|DBTYPE_R4|**float**|**VT_SS_R4**|Supporta il tipo di dati **reale** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .|  
|dblFloatVal|DBTYPE_R8|**double**|**VT_SS_R8**|Supporta il tipo di dati **float** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .|  
|cyMoneyVal|DBTYPE_CY|**LARGE_INTEGER**|**VT_SS_MONEY VT_SS_SMALLMONEY**|Supporta i tipi di dati **Money** e **smallmoney** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .|  
|fBitVal|DBTYPE_BOOL|**VARIANT_BOOL**|**VT_SS_BIT**|Supporta il tipo di dati **bit** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .|  
|rgbGuidVal|DBTYPE_GUID|**GUID**|**VT_SS_GUID**|Supporta il tipo di dati **uniqueidentifier** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .|  
|numNumericVal|DBTYPE_NUMERIC|**DB_NUMERIC**|**VT_SS_NUMERIC**|Supporta il tipo di dati **numeric** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .|  
|dDateVal|DBTYPE_DATE|**DBDATE**|**VT_SS_DATE**|Supporta il tipo di dati **date**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|tsDateTimeVal|DBTYPE_DBTIMESTAMP|**DBTIMESTAMP**|**VT_SS_SMALLDATETIME VT_SS_DATETIME VT_SS_DATETIME2**|Supporta i tipi di dati **smalldatetime**, **DateTime**e **datetime2** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .|  
|Time2Val|DBTYPE_DBTIME2|**DBTIME2**|**VT_SS_TIME2**|Supporta il tipo di dati **Time** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .<br /><br /> Include i membri indicati di seguito:<br /><br /> *tTime2Val* (**DBTIME2**)<br /><br /> *bScale* (**Byte**) Specifica la scala per il valore *tTime2Val* .|  
|DateTimeVal|DBTYPE_DBTIMESTAMP|**DBTIMESTAMP**|**VT_SS_DATETIME2**|Supporta il tipo di dati **datetime2** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .<br /><br /> Include i membri indicati di seguito:<br /><br /> *tsDataTimeVal* (DBTIMESTAMP)<br /><br /> *bScale* (**Byte**) Specifica la scala per il valore *tsDataTimeVal* .|  
|DateTimeOffsetVal|DBTYPE_DBTIMESTAMPOFSET|**DBTIMESTAMPOFFSET**|**VT_SS_DATETIMEOFFSET**|Supporta il tipo di dati **DateTimeOffset** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .<br /><br /> Include i membri indicati di seguito:<br /><br /> *tsoDateTimeOffsetVal* (**DBTIMESTAMPOFFSET**)<br /><br /> *bScale* (**Byte**) Specifica la scala per il valore *tsoDateTimeOffsetVal* .|  
|NCharVal|Nessun indicatore del tipo OLE DB corrispondente.|**struct _NCharVal**|**VT_SS_WVARSTRING,**<br /><br /> **VT_SS_WSTRING**|Supporta i tipi di dati **nchar** e **nvarchar** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .<br /><br /> Include i membri indicati di seguito:<br /><br /> *sActualLength* (**Breve**) Specifica la lunghezza effettiva per la stringa a cui punta *punta pwchNCharVal* . Non include lo zero finale.<br /><br /> *sMaxLength* (**Breve**) Specifica la lunghezza massima per la stringa a cui punta *punta pwchNCharVal* .<br /><br /> *punta pwchNCharVal* (**WCHAR** \*) puntatore alla stringa.<br /><br /> Membri non utilizzati: *rgbReserved*, *dwReserved*e *pwchReserved*.|  
|CharVal|Nessun indicatore del tipo OLE DB corrispondente.|**struct _CharVal**|**VT_SS_STRING,**<br /><br /> **VT_SS_VARSTRING**|Supporta i tipi di dati **char** e **varchar** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .<br /><br /> Include i membri indicati di seguito:<br /><br /> *sActualLength* (**Breve**) Specifica la lunghezza effettiva per la stringa a cui punta *punta pchCharVal* . Non include lo zero finale.<br /><br /> *sMaxLength* (**Breve**) Specifica la lunghezza massima per la stringa a cui punta *punta pchCharVal* .<br /><br /> *punta pchCharVal* (**Char** \*) puntatore alla stringa.<br /><br /> Membri non utilizzati:<br /><br /> *rgbReserved*, *dwReserved*e *pwchReserved*.|  
|BinaryVal|Nessun indicatore del tipo OLE DB corrispondente.|**struct _BinaryVal**|**VT_SS_VARBINARY,**<br /><br /> **VT_SS_BINARY**|Supporta i tipi di dati **Binary** e **varbinary** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .<br /><br /> Include i membri indicati di seguito:<br /><br /> *sActualLength* (**Breve**) Specifica la lunghezza effettiva per i dati a cui punta *punta prgbBinaryVal* .<br /><br /> *sMaxLength* (**Breve**) Specifica la lunghezza massima per i dati a cui punta *punta prgbBinaryVal* .<br /><br /> *punta prgbBinaryVal* Puntatore (**byte** \*) ai dati binari.<br /><br /> Membro non usato: *dwReserved*.|  
|UnknownType|UNUSED|UNUSED|UNUSED|UNUSED|  
|BLOBType|UNUSED|UNUSED|UNUSED|UNUSED|  
  
## <a name="see-also"></a>Vedere anche  
 [Tipi &#40;di dati OLE DB&#41;](../../oledb/ole-db-data-types/data-types-ole-db.md)  
  
  
