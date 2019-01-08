---
title: Recordset gerarchici in XML | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- hierarchical Recordsets [ADO], in XML
ms.assetid: 5d4b11c4-c94f-4910-b99b-5b9abc50d791
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 860732a8d694ee59dae05f76eb9cabe49ebc8c96
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/11/2018
ms.locfileid: "53211255"
---
# <a name="hierarchical-recordsets-in-xml"></a>Recordset gerarchici in XML
ADO consente la persistenza degli oggetti Recordset gerarchici in XML. Con gli oggetti di Recordset gerarchici, il valore di un campo nell'oggetto Recordset padre è un altro oggetto Recordset. Questi campi sono rappresentati come elementi figlio nel flusso XML anziché un attributo.  
  
## <a name="remarks"></a>Note  
 Nell'esempio seguente viene illustrato in questo caso:  
  
```  
Rs.Open "SHAPE {select stor_id, stor_name, state from stores} APPEND ({select stor_id, ord_num, ord_date, qty from sales} AS rsSales RELATE stor_id TO stor_id)", "Provider=MSDataShape;DSN=pubs;Integrated Security=SSPI;"  
```  
  
 Di seguito è riportato il formato XML del set di record persistente:  
  
```  
<xml xmlns:s="uuid:BDC6E3F0-6DA3-11d1-A2A3-00AA00C14882"     xmlns:dt="uuid:C2F41010-65B3-11d1-A29F-00AA00C14882"     xmlns:rs="urn:schemas-microsoft-com:rowset"   
    xmlns:z="#RowsetSchema">   
  <s:Schema id="RowsetSchema">   
    <s:ElementType name="row" content="eltOnly" rs:updatable="true">   
      <s:AttributeType name="stor_id" rs:number="1"   
        rs:writeunknown="true">   
        <s:datatype dt:type="string" dt:maxLength="4"   
          rs:fixedlength="true" rs:maybenull="false"/>   
      </s:AttributeType>   
      <s:AttributeType name="stor_name" rs:number="2" rs:nullable="true"   
        rs:writeunknown="true">   
          <s:datatype dt:type="string" dt:maxLength="40"/>   
      </s:AttributeType>   
      <s:AttributeType name="state" rs:number="3" rs:nullable="true"   
        rs:writeunknown="true">   
        <s:datatype dt:type="string" dt:maxLength="2"   
          rs:fixedlength="true"/>   
      </s:AttributeType>   
      <s:ElementType name="rsSales" content="eltOnly"   
        rs:updatable="true" rs:relation="010000000100000000000000">   
        <s:AttributeType name="stor_id" rs:number="1"   
          rs:writeunknown="true">   
          <s:datatype dt:type="string" dt:maxLength="4"   
            rs:fixedlength="true" rs:maybenull="false"/>   
        </s:AttributeType>   
        <s:AttributeType name="ord_num" rs:number="2"   
          rs:writeunknown="true">   
          <s:datatype dt:type="string" dt:maxLength="20"   
            rs:maybenull="false"/>   
        </s:AttributeType>   
        <s:AttributeType name="ord_date" rs:number="3"   
          rs:writeunknown="true">   
            <s:datatype dt:type="dateTime" dt:maxLength="16"   
              rs:scale="3" rs:precision="23" rs:fixedlength="true"   
              rs:maybenull="false"/>   
        </s:AttributeType>   
        <s:AttributeType name="qty" rs:number="4" rs:writeunknown="true">   
          <s:datatype dt:type="i2" dt:maxLength="2" rs:precision="5"   
            rs:fixedlength="true" rs:maybenull="false"/>   
        </s:AttributeType>   
        <s:extends type="rs:rowbase"/>   
      </s:ElementType>   
      <s:extends type="rs:rowbase"/>   
    </s:ElementType>   
  </s:Schema>   
  <rs:data>   
    <z:row stor_id="6380" stor_name="Eric the Read Books" state="WA">   
      <rsSales stor_id="6380" ord_num="6871"   
        ord_date="1994-09-14T00:00:00" qty="5"/>   
      <rsSales stor_id="6380" ord_num="722a"   
        ord_date="1994-09-13T00:00:00" qty="3"/>   
    </z:row>   
    <z:row stor_id="7066" stor_name="Barnum's" state="CA">   
      <rsSales stor_id="7066" ord_num="A2976"   
        ord_date="1993-05-24T00:00:00" qty="50"/>   
      <rsSales stor_id="7066" ord_num="QA7442.3"   
        ord_date="1994-09-13T00:00:00" qty="75"/>   
    </z:row>   
    <z:row stor_id="7067" stor_name="News & Brews" state="CA">   
      <rsSales stor_id="7067" ord_num="D4482"   
        ord_date="1994-09-14T00:00:00" qty="10"/>   
      <rsSales stor_id="7067" ord_num="P2121"   
        ord_date="1992-06-15T00:00:00" qty="40"/>   
      <rsSales stor_id="7067" ord_num="P2121"   
        ord_date="1992-06-15T00:00:00" qty="20"/>   
      <rsSales stor_id="7067" ord_num="P2121"   
        ord_date="1992-06-15T00:00:00" qty="20"/>   
    </z:row>   
  </rs:data>   
</xml>   
```  
  
 Quando questo viene reso persistente in questo modo, l'esatto ordine delle colonne nell'oggetto Recordset padre non è ovvio. Qualsiasi campo nell'elemento padre può contenere un Recordset figlio. Il Provider di persistenza mantiene tutte le colonne scalari prima di tutto come attributi e quindi le colonne"tutti figlio Recordset" come elementi figlio della riga padre. La posizione ordinale del campo nell'elemento padre Recordset possa essere ottenuto esaminando la definizione dello schema del set di record. Ogni campo ha una proprietà OLE DB, rs: numero, definita nello spazio dei nomi dello schema Recordset che contiene il numero ordinale per il campo.  
  
 I nomi di tutti i campi nell'oggetto Recordset figlio sono concatenati con il nome del campo del Recordset che contiene questo elemento figlio del padre. Questo modo si garantisce che siano presenti conflitti nome nei casi in cui padre e figlio recordset entrambi contenere un campo che viene ottenuto da due tabelle diverse ma avente.  
  
 Durante il salvataggio di recordset gerarchici in XML, è necessario tenere in ADO le seguenti restrizioni:  
  
-   Recordset gerarchici con aggiornamenti in sospeso non possono essere resi persistenti in XML.  
  
-   Un Recordset gerarchico creato con un comando di forma con parametri non può essere persistente (in formato XML o ADTG).  
  
-   ADO Salva attualmente la relazione tra padre e figlio recordset come un oggetto binario di grandi dimensioni (BLOB). I tag XML per descrivere la relazione non sono ancora stati definiti nello spazio dei nomi dello schema del set di righe.  
  
-   Quando viene salvato un Recordset gerarchico, figlio tutti i recordset vengono salvati con essa. Se il Recordset corrente è un elemento figlio di un altro oggetto Recordset, il relativo elemento padre non viene salvato. Figlio tutti i recordset tramite cui formare il sottoalbero del set di record corrente vengono salvate.  
  
 Quando si riapre un Recordset gerarchico dal rispettivo formato XML persistente, è necessario considerare le limitazioni seguenti:  
  
-   Se il record figlio contiene i record per il quale esistono record padre corrispondente, queste righe non vengono scritte nella rappresentazione XML del Recordset gerarchici. Di conseguenza, tali righe andranno perse quando il Recordset è riaperto dalla posizione persistente.  
  
-   Se un record figlio ha dei riferimenti a più di un record padre, quindi alla riapertura del Recordset, il Recordset figlio può contenere i record duplicati. Tuttavia, questi duplicati saranno visibili solo se l'utente interagisce direttamente con il set di righe figlio sottostanti. Se un capitolo viene usato per passare l'oggetto Recordset, ovvero l'unico modo per spostarsi tra ADO, figlio, i duplicati non sono visibili.  
  
## <a name="see-also"></a>Vedere anche  
 [Persistenza di record in formato XML](../../../ado/guide/data/persisting-records-in-xml-format.md)
