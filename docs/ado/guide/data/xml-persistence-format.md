---
title: Formato di persistenza XML | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- XML persistence [ADO], persistence format
ms.assetid: 6e146738-ac4d-47bb-b6cd-d87b2260aead
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 49a3c276aa17d8f2bd7f48296eeecb69ad91d04d
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66718372"
---
# <a name="xml-persistence-format"></a>Formato di persistenza XML
ADO utilizza la codifica UTF-8 per il flusso XML che viene mantenuto.  
  
 Il formato XML ADO viene suddiviso in due sezioni, una sezione schema aggiungendo la sezione di dati. Di seguito è riportato un file XML di esempio per la tabella spedizionieri dal database Northwind. Vengono illustrate varie parti del codice XML di esempio seguente.  
  
## <a name="remarks"></a>Note  
  
```  
<xml xmlns:s="uuid:BDC6E3F0-6DA3-11d1-A2A3-00AA00C14882"   
xmlns:dt="uuid:C2F41010-65B3-11d1-A29F-00AA00C14882"   
xmlns:rs="urn:schemas-microsoft-com:rowset"   
xmlns:z="#RowsetSchema">   
  <s:Schema id="RowsetSchema">   
    <s:ElementType name="row" content="eltOnly" rs:updatable="true">   
      <s:AttributeType name="ShipperID" rs:number="1"   
        rs:basetable="shippers" rs:basecolumn="ShipperID"  
        rs:keycolumn="true">   
        <s:datatype dt:type="int" dt:maxLength="4" rs:precision="10"   
          rs:fixedlength="true" rs:maybenull="false"/>   
      </s:AttributeType>   
      <s:AttributeType name="CompanyName" rs:number="2"   
        rs:nullable="true" rs:write="true" rs:basetable="shippers"   
        rs:basecolumn="CompanyName">   
        <s:datatype dt:type="string" dt:maxLength="40" />   
      </s:AttributeType>   
      <s:AttributeType name="Phone" rs:number="3" rs:nullable="true"   
        rs:write="true" rs:basetable="shippers"   
        rs:basecolumn="Phone">   
        <s:datatype dt:type="string" dt:maxLength="24"/>   
      </s:AttributeType>   
      <s:extends type="rs:rowbase"/>   
    </s:ElementType>   
  </s:Schema>   
  
  <rs:data>   
    <z:row ShipperID="1" CompanyName="Speedy Express"   
      Phone="(503) 555-9831"/>   
    <z:row ShipperID="2" CompanyName="United Package"   
      Phone="(503) 555-3199"/>   
    <z:row ShipperID="3" CompanyName="Federal Shipping"   
      Phone="(503) 555-9931"/>   
  </rs:data>   
</xml>  
```  
  
 Lo schema sono illustrate le dichiarazioni di spazi dei nomi, la sezione dello schema e la sezione di dati. La sezione dello schema contiene le definizioni per riga, ShipperID, CompanyName e telefono.  
  
 Definizioni dello schema conformi per il [specifica W3C XML-Data](http://www.w3.org/TR/1998/NOTE-XML-data/) e può essere convalidato completamente (anche se la convalida non verrà eseguita in Internet Explorer 5). XML-Data è attualmente il formato dello schema supportate solo per la persistenza di Recordset.  
  
 La sezione di dati sono presenti tre righe che contengono informazioni spedizionieri. Per un set di righe vuoto, la sezione di dati può essere vuota, ma il \<rs: dati > tag devono essere presenti. Senza dati, è possibile scrivere semplicemente la sintassi abbreviata tag \<rs: data / >. Qualsiasi tag il prefisso "rs" indica che si tratta dello spazio dei nomi definito dall'urn: schemas-microsoft-com: rowset.  
  
## <a name="see-also"></a>Vedere anche  
 [Persistenza di record in formato XML](../../../ado/guide/data/persisting-records-in-xml-format.md)
