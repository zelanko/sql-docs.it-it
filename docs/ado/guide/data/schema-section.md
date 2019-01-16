---
title: Sezione schema | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Schema section [ADO]
ms.assetid: 4ac6e524-2c92-48e8-b871-0a4b5c8fda18
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 45e8e37d8bb85e727771072abda9249b8155076f
ms.sourcegitcommit: bfa10c54e871700de285d7f819095d51ef70d997
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/14/2019
ms.locfileid: "54256196"
---
# <a name="schema-section"></a>Sezione dello schema
La sezione dello schema è obbligatoria. Come illustrato nell'esempio precedente, ADO scrive i metadati dettagliati su ogni colonna per mantenere la semantica dei valori dei dati quanto più possibile per l'aggiornamento. Tuttavia, per caricare il file XML, ADO richiede solo i nomi delle colonne e il set di righe a cui appartengono. Di seguito è riportato un esempio di uno schema minimo:  
  
```  
<xml xmlns:s="uuid:BDC6E3F0-6DA3-11d1-A2A3-00AA00C14882"  
    xmlns:rs="urn:schemas-microsoft-com:rowset"  
    xmlns:z="#RowsetSchema">  
  <s:Schema id="RowsetSchema">  
    <s:ElementType name="row" content="eltOnly">  
      <s:AttributeType name="ShipperID"/>  
      <s:AttributeType name="CompanyName"/>  
      <s:AttributeType name="Phone"/>  
      <s:Extends type="rs:rowbase"/>  
    </s:ElementType>  
  </s:Schema>  
  <rs:data>  
...  
  </rs:data>  
</xml>  
```  
  
 Nell'esempio precedente, ADO considererà i dati come stringhe a lunghezza variabile perché alcuna informazione sul tipo non è inclusa nello schema.  
  
## <a name="creating-aliases-for-column-names"></a>Creazione di alias per i nomi di colonna  
 L'attributo name di rs: consente di creare un alias per un nome di colonna in modo che le informazioni di colonna esposte dal set di righe potrebbe visualizzare un nome descrittivo e un nome più breve può essere usato nella sezione dei dati. Ad esempio, lo schema precedente può essere modificato per eseguire il mapping ShipperID da s1 a s2, CompanyName e numero di telefono per s3 come indicato di seguito:  
  
```  
<s:Schema id="RowsetSchema">   
<s:ElementType name="row" content="eltOnly" rs:updatable="true">   
<s:AttributeType name="s1" rs:name="ShipperID" rs:number="1" ...>   
...  
</s:AttributeType>   
<s:AttributeType name="s2" rs:name="CompanyName" rs:number="2" ...>   
...  
</s:AttributeType>   
<s:AttributeType name="s3" rs:name="Phone" rs:number="3" ...>   
...  
</s:AttributeType>   
...  
</s:ElementType>   
</s:Schema>  
```  
  
 Quindi, nella sezione dei dati, la riga sarebbe utilizzare l'attributo name (non rs: nome) per fare riferimento a tale colonna:  
  
```  
"<row s1="1" s2="Speedy Express" s3="(503) 555-9831"/>  
```  
  
 È necessario creare alias per i nomi delle colonne ogni volta che un nome di colonna non è un attributo valido o un nome di tag in formato XML. Ad esempio, "LastName" deve avere un alias perché i nomi contenenti spazi vuoti sono gli attributi non validi. La riga seguente non verrà gestita correttamente dal parser XML, pertanto è necessario creare un alias per un altro nome che non dispone di uno spazio incorporato.  
  
```  
<row last name="Jones"/>  
```  
  
 Il valore è utilizzato per l'attributo del nome deve essere utilizzato in modo coerente in ogni punto che la colonna viene fatto riferimento nelle sezioni sia lo schema e i dati del documento XML. Nell'esempio seguente illustra l'uso coerente di s1:  
  
```  
<s:Schema id="RowsetSchema">  
  <s:ElementType name="row" content="eltOnly">  
    <s:attribute type="s1"/>  
    <s:attribute type="CompanyName"/>  
    <s:attribute type="s3"/>  
    <s:extends type="rs:rowbase"/>  
  </s:ElementType>  
  <s:AttributeType name="s1" rs:name="ShipperID" rs:number="1"   
    rs:maydefer="true" rs:writeunknown="true">  
    <s:datatype dt:type="i4" dt:maxLength="4" rs:precision="10"   
      rs:fixedlength="true" rs:maybenull="true"/>  
  </s:AttributeType>  
</s:Schema>  
<rs:data>  
  <z:row s1="1" CompanyName="Speedy Express" s3="(503) 555-9831"/>  
</rs:data>  
```  
  
 Analogamente, poiché non esiste alcun alias non definiti per `CompanyName` nell'esempio precedente, `CompanyName` deve essere usato in modo coerente in tutto il documento.  
  
## <a name="data-types"></a>Tipi di dati  
 È possibile applicare un tipo di dati a una colonna con l'attributo dt: Type. Per informazioni esaurienti ai tipi XML consentiti, vedere la sezione tipi di dati del [specifica W3C XML-Data](http://www.w3.org/TR/1998/NOTE-XML-data/). È possibile specificare un tipo di dati in due modi: specificare l'attributo dt: Type direttamente sulla definizione della colonna oppure utilizzare il costrutto s:datatype come un elemento annidato della definizione della colonna. Ad esempio,  
  
```  
<s:AttributeType name="Phone" >  
  <s:datatype dt:type="string"/>  
</s:AttributeType>  
```  
  
 equivale a  
  
```  
<s:AttributeType name="Phone" dt:type="string"/>  
```  
  
 Se si omette l'attributo dt: Type interamente dalla definizione di riga, per impostazione predefinita, il tipo della colonna sarà una stringa di lunghezza variabile.  
  
 Se si dispone di più informazioni tipo semplicemente il nome del tipo (ad esempio, dt: maxLength), rende più leggibile, usare l'elemento figlio s:datatype. Si tratta semplicemente di una convenzione, tuttavia e non è un requisito.  
  
 Gli esempi seguenti illustrano inoltre come includere le informazioni sul tipo nello schema.  
  
```  
<!-- 1. String with no max length -->  
<s:AttributeType name="title_id"/>  
<!-or -->  
<s:AttributeType name="title_id" dt:type="string"/>  
  
<!-- 2. Fixed length string with max length of 6 -->  
<s:AttributeType name="title_id">  
    <s:datatype dt:type="string" dt:maxLength="6" rs:fixedlength="true" />  
</s:AttributeType>  
  
<!-- 3. Variable length string with max length of 6 -->  
<s:AttributeType name="title_id">  
    <s:datatype dt:type="string" dt:maxLength="6" />  
</s:AttributeType>  
  
<!-- 4. Integer -->  
<s:AttributeType name="title_id" dt:type="int"/>  
```  
  
 È un utilizzo meno evidente dell'attributo rs: fixedlength nel secondo esempio. Una colonna con l'attributo rs: fixedlength impostata su true indica che i dati devono avere la lunghezza definita nello schema. In questo caso, un valore valido per title_id è "123456", come è "123". Tuttavia, "123" non è valido perché la sua lunghezza è 3, non 6. Vedere Guida i programmatori OLE DB per una più descrizione della proprietà fixedlength completa.  
  
## <a name="handling-nulls"></a>Gestione dei valori null  
 I valori null vengono gestiti dall'attributo rs: maybenull. Se questo attributo è impostato su true, il contenuto della colonna può contenere un valore null. Inoltre, se la colonna non viene trovata in una riga di dati, l'utente legge i dati dal set di righe verrà visualizzato lo stato null da IRowset::GetData(). Prendere in considerazione le seguenti definizioni delle colonne dalla tabella spedizionieri.  
  
```  
<s:AttributeType name="ShipperID">  
  <s:datatype dt:type="int" dt:maxLength="4"/>  
</s:AttributeType>  
<s:AttributeType name="CompanyName">  
  <s:datatype dt:type="string" dt:maxLength="40" rs:maybenull="true"/>  
</s:AttributeType>  
```  
  
 La definizione consente `CompanyName` sia null, ma `ShipperID` non può contenere un valore null. Se la sezione di dati contiene la riga seguente, il Provider di persistenza imposterebbe lo stato dei dati per il `CompanyName` colonna per la costante di stato OLE DB DBSTATUS_S_ISNULL:  
  
```  
<z:row ShipperID="1"/>  
```  
  
 Se la riga è stata completamente vuota, come indicato di seguito, il Provider di persistenza restituirà uno stato di OLE DB di DBSTATUS_E_UNAVAILABLE per `ShipperID` DBSTATUS_S_ISNULL per CompanyName e.  
  
```  
<z:row/>   
```  
  
 Si noti che una stringa di lunghezza zero non è lo stesso come null.  
  
```  
<z:row ShipperID="1" CompanyName=""/>  
```  
  
 Per la riga precedente, il Provider di persistenza restituirà uno stato di OLE DB di DBSTATUS_S_OK per entrambe le colonne. Il `CompanyName` in questo caso è semplicemente "" (una stringa di lunghezza zero).  
  
 Per altre informazioni su OLE DB costrutti disponibili per l'uso dello schema di un documento XML per OLE DB, vedere la definizione di "urn: schemas-microsoft-com: rowset" e Guida i programmatori OLE DB.  
  
## <a name="see-also"></a>Vedere anche  
 [Persistenza di record in formato XML](../../../ado/guide/data/persisting-records-in-xml-format.md)
