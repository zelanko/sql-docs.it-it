---
title: DataTypeEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- DataTypeEnum
helpviewer_keywords:
- DataTypeEnum enumeration [ADO]
ms.assetid: 2c57eca6-9336-4b06-ba10-9fef5926b1d0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 27386894ce6d1d393505d49b4863a0ba9bf3320b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67933229"
---
# <a name="datatypeenum"></a>DataTypeEnum
Specifica il tipo di dati di un [campo](../../../ado/reference/ado-api/field-object.md), [parametro](../../../ado/reference/ado-api/parameter-object.md), o [proprietà](../../../ado/reference/ado-api/property-object-ado.md). Indicatore del tipo OLE DB corrispondente è racchiusa tra parentesi nella colonna Descrizione della tabella seguente.  
  
|Costante|Value|Descrizione|  
|--------------|-----------|-----------------|  
|**AdArray**|0x2000|Un valore del flag, sempre combinato con un'altra costante del tipo di dati, che indica una matrice di altro tipo di dati. Non è applicabile a ADOX.|  
|**adBigInt**|20|Indica un intero con segno a 8 byte (DBTYPE_I8).|  
|**adBinary**|128|Indica un valore binario (DBTYPE_BYTES).|  
|**adBoolean**|11|Indica un **booleana** valore (DBTYPE_BOOL).|  
|**adBSTR**|8|Indica una stringa di caratteri con terminazione null (Unicode) (DBTYPE_BSTR).|  
|**adChapter**|136|Indica un valore a quattro byte capitolo che identifica le righe in un set di righe figlio (DBTYPE_HCHAPTER).|  
|**adChar**|129|Indica un valore di stringa (DBTYPE_STR).|  
|**adCurrency**|6|Indica un valore di valuta (DBTYPE_CY). Valuta è un numero a virgola fissa con quattro cifre a destra del separatore decimale. Questo viene archiviato in un intero con segno a otto byte ridimensionato di 10.000.|  
|**adDate**|7|Indica un valore di data (DBTYPE_DATE). Una data viene archiviata come un valore double, la cui parte intera è il numero di giorni a partire dal 30 dicembre 1899, e la parte frazionaria dei quali rappresenta la frazione del giorno.|  
|**adDBDate**|133|Indica un valore di data (aaaammgg) (DBTYPE_DBDATE).|  
|**adDBTime**|134|Indica un valore di ora (hhmmss) (DBTYPE_DBTIME).|  
|**adDBTimeStamp**|135|Indica un indicatore di data e ora (aaaammgghhmmss più una frazione di miliardesimi) (DBTYPE_DBTIMESTAMP).|  
|**adDecimal**|14|Indica un valore numerico esatto con precisione e scala (DBTYPE_DECIMAL).|  
|**adDouble**|5|Indica un valore a virgola mobile a precisione doppia (DBTYPE_R8).|  
|**adEmpty**|0|Non specifica alcun valore (DBTYPE_EMPTY).|  
|**adError**|10|Indica un codice di errore a 32 bit (DBTYPE_ERROR).|  
|**adFileTime**|64|Indica un valore a 64 bit che rappresenta il numero di intervalli di 100 nanosecondi dal 1 gennaio 1601 (DBTYPE_FILETIME).|  
|**adGUID**|72|Indica un identificatore univoco globale (GUID) (DBTYPE_GUID).|  
|**adIDispatch**|9|Indica un puntatore a un **IDispatch** interfaccia su un oggetto COM (DBTYPE_IDISPATCH).<br /><br /> **Nota** questo tipo di dati non è supportato da ADO. Utilizzo potrebbe provocare risultati imprevisti.|  
|**adInteger**|3|Indica un intero con segno a quattro byte (DBTYPE_I4).|  
|**adIUnknown**|13|Indica un puntatore a un **IUnknown** interfaccia su un oggetto COM (DBTYPE_IUNKNOWN).<br /><br /> **Nota** questo tipo di dati non è supportato da ADO. Utilizzo potrebbe provocare risultati imprevisti.|  
|**adLongVarBinary**|205|Indica un valore binario lungo.|  
|**adLongVarChar**|201|Indica un valore di stringa di lunghezza maggiore.|  
|**adLongVarWChar**|203|Indica un valore di stringa Unicode con terminazione null lungo.|  
|**adNumeric**|131|Indica un valore numerico esatto con precisione e scala (DBTYPE_NUMERIC).|  
|**adPropVariant**|138|Indica un'automazione PROPVARIANT (DBTYPE_PROP_VARIANT).|  
|**adSingle**|4|Indica un valore a virgola mobile a precisione singola (DBTYPE_R4).|  
|**adSmallInt**|2|Indica un intero con segno a due byte (DBTYPE_I2).|  
|**adTinyInt**|16|Indica un intero con segno a 1 byte (DBTYPE_I1).|  
|**adUnsignedBigInt**|21|Indica un intero senza segno a 8 byte (DBTYPE_UI8).|  
|**adUnsignedInt**|19|Indica un intero senza segno a quattro byte (DBTYPE_UI4).|  
|**adUnsignedSmallInt**|18|Indica un intero senza segno a due byte (DBTYPE_UI2).|  
|**adUnsignedTinyInt**|17|Indica un intero senza segno a 1 byte (DBTYPE_UI1).|  
|**adUserDefined**|132|Indica una variabile definita dall'utente (DBTYPE_UDT).|  
|**adVarBinary**|204|Indica un valore binario.|  
|**adVarChar**|200|Indica un valore di stringa.|  
|**adVariant**|12|Indica un'automazione **Variant** (DBTYPE_VARIANT).<br /><br /> **Nota** questo tipo di dati non è supportato da ADO. Utilizzo potrebbe provocare risultati imprevisti.|  
|**adVarNumeric**|139|Indica un valore numerico.|  
|**adVarWChar**|202|Indica una stringa di caratteri Unicode con terminazione null.|  
|**adWChar**|130|Indica una terminazione null stringa di caratteri Unicode (DBTYPE_WSTR).|  
  
## <a name="adowfc-equivalent"></a>Equivalente di ADO o WFC  
 Package: **com.ms.wfc.data**  
  
|Costante|  
|--------------|  
|AdoEnums.DataType.ARRAY|  
|AdoEnums.DataType.BIGINT|  
|AdoEnums.DataType.BINARY|  
|AdoEnums.DataType.BOOLEAN|  
|AdoEnums.DataType.BSTR|  
|AdoEnums.DataType.CHAPTER|  
|AdoEnums.DataType.CHAR|  
|AdoEnums.DataType.CURRENCY|  
|AdoEnums.DataType.DATE|  
|AdoEnums.DataType.DBDATE|  
|AdoEnums.DataType.DBTIME|  
|AdoEnums.DataType.DBTIMESTAMP|  
|AdoEnums.DataType.DECIMAL|  
|AdoEnums.DataType.DOUBLE|  
|AdoEnums.DataType.EMPTY|  
|AdoEnums.DataType.ERROR|  
|AdoEnums.DataType.FILETIME|  
|AdoEnums.DataType.GUID|  
|AdoEnums.DataType.IDISPATCH|  
|AdoEnums.DataType.INTEGER|  
|AdoEnums.DataType.IUNKNOWN|  
|AdoEnums.DataType.LONGVARBINARY|  
|AdoEnums.DataType.LONGVARCHAR|  
|AdoEnums.DataType.LONGVARWCHAR|  
|AdoEnums.DataType.NUMERIC|  
|AdoEnums.DataType.PROPVARIANT|  
|AdoEnums.DataType.SINGLE|  
|AdoEnums.DataType.SMALLINT|  
|AdoEnums.DataType.TINYINT|  
|AdoEnums.DataType.UNSIGNEDBIGINT|  
|AdoEnums.DataType.UNSIGNEDINT|  
|AdoEnums.DataType.UNSIGNEDSMALLINT|  
|AdoEnums.DataType.UNSIGNEDTINYINT|  
|AdoEnums.DataType.USERDEFINED|  
|AdoEnums.DataType.VARBINARY|  
|AdoEnums.DataType.VARCHAR|  
|AdoEnums.DataType.VARIANT|  
|AdoEnums.DataType.VARNUMERIC|  
|AdoEnums.DataType.VARWCHAR|  
|AdoEnums.DataType.WCHAR|  
  
## <a name="applies-to"></a>Si applica a  
  
|||  
|-|-|  
|[Metodo Append (ADO)](../../../ado/reference/ado-api/append-method-ado.md)|[Metodo CreateParameter (ADO)](../../../ado/reference/ado-api/createparameter-method-ado.md)|  
|[Metodo CreateRecordset (Servizi Desktop remoto)](../../../ado/reference/rds-api/createrecordset-method-rds.md)|[Proprietà Type (ADO)](../../../ado/reference/ado-api/type-property-ado.md)|
