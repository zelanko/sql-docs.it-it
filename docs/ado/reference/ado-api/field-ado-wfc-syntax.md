---
title: Campo (ADO - WFC sintassi) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 02/15/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Field collection [ADO], ADO/WFC syntax
ms.assetid: 7e01cb24-2338-4f92-ad46-8d97248e1a4d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ea2245c3f57b5ad3b14847f15791575afde1043c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63031972"
---
# <a name="field-ado---wfc-syntax"></a>Field (sintassi ADO/WFC)
## <a name="package-commswfcdata"></a>creare un pacchetto com.ms. wfc.  
  
### <a name="methods"></a>Metodi  
  
```  
public void appendChunk(byte[] bytes)  
public void appendChunk(char[] chars)  
public void appendChunk(String chars)  
public byte[] getByteChunk(int len)  
public char[] getCharChunk(int len)  
public String getStringChunk(int len)  
```  
  
### <a name="properties"></a>Proprietà  
  
```  
public int getActualSize()  
public int getAttributes()  
public void setAttributes(int pl)  
public com.ms.com.IUnknown getDataFormat()  
public void setDataFormat(com.ms.com.IUnknown format)  
```  
  
 (Per altre informazioni, vedere la documentazione per l'interfaccia IDataFormat).  
  
```  
public int getDefinedSize()  
public void setDefinedSize(int pl)  
public String getName()  
public int getNumericScale()  
public void setNumericScale(byte pbNumericScale)  
public Variant getOriginalValue()  
public int getPrecision()  
public void setPrecision(byte pbPrecision)  
public int getType()  
public void setType(int pDataType)  
public Variant getUnderlyingValue()  
public Variant getValue()  
public void setValue(Variant value)  
public AdoProperties getProperties()  
```  
  
### <a name="field-accessor-methods"></a>Metodi della funzione di accesso di campo  
 Il [valore](../../../ado/reference/ado-api/value-property-ado.md) proprietà di un [campo](../../../ado/reference/ado-api/field-object.md) oggetto Ottiene o imposta il contenuto di tale oggetto. Il contenuto è rappresentato come una variante, un tipo di oggetto che può essere assegnato un valore e i diversi tipi di dati.  
  
 ADO/WFC implementa il **valore** proprietà con il **getValue** metodo, che restituisce un oggetto VARIANT; e il **setValue** metodo, che utilizza una variante come argomento. Varianti sono altamente efficienti in determinate lingue, ad esempio Microsoft Visual Basic.  
  
 Oltre al **valore** ADO/WFC di proprietà, fornisce *della funzione di accesso* metodi che utilizzano tipi di dati Java per ottenere e impostare il contenuto del **campo** oggetti. La maggior parte di questi metodi ha il formato dei nomi **ottenere**_DataType_ oppure **impostare**_DataType_.  
  
 Esistono due importanti eccezioni: Uno dei **getObject** metodi restituisce un oggetto convertito in una classe specificata. È presente alcun **importante** proprietà; viene invece un' **isNull** proprietà che restituisce un valore booleano che indica se il campo è null.  
  
```  
public native boolean getBoolean();  
public void setBoolean(boolean v)  
public native byte getByte();  
public void setByte(byte v)  
public native byte[] getBytes();  
public void setBytes(byte[] v)  
public native double getDouble();  
public void setDouble(double v)  
public native float getFloat();  
public void setFloat(float v)  
public native int getInt();  
public void setInt(int v)  
public native long getLong();  
public void setLong(long v)  
public native short getShort();  
public void setShort(short v)  
public native String getString();  
public void setString(String v)  
public native boolean isNull();  
public void setNull()  
public Object getObject()  
public Object getObject(Class c)  
public void setObject(Object value)  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Oggetto Field](../../../ado/reference/ado-api/field-object.md)
