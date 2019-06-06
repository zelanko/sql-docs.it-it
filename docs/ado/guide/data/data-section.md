---
title: Sezione di dati | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data section [ADO]
ms.assetid: 43dc42a8-7057-48e6-93d6-880d5c5c51a4
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 76cd14b8ee1c5a55e0312993090bfaf098c7e219
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66702133"
---
# <a name="data-section"></a>Sezione di dati
La sezione di dati definisce i dati del set di righe con uno qualsiasi degli aggiornamenti, le operazioni di inserimento o eliminazione in sospeso. La sezione di dati può contenere zero o più righe. Può contenere solo i dati da un set di righe in cui la riga è definita dallo schema. Inoltre, come illustrato in precedenza, le colonne senza dati possono essere omessa. Se un attributo o un sottoelemento viene usato nella sezione dei dati e tale costrutto non è stato definito nella sezione schema, viene ignorata automaticamente.  
  
## <a name="string"></a>String  
 I caratteri XML riservati nei dati di testo devono essere sostituiti con entità di carattere appropriato. Ad esempio, nel nome della società "Garage di Joe", la virgoletta singola devono essere sostituita da un'entità. La riga effettiva sarebbe simile al seguente:  
  
```  
<z:row CompanyName="Joe's Garage"/>  
```  
  
 I seguenti caratteri sono riservati in XML e devono essere sostituiti da entità carattere: {"," &,\<, >}.  
  
## <a name="binary"></a>Binario  
 Dati binari sono con codificata hex (vale a dire, un byte viene mappato a due caratteri, un carattere per nibble).  
  
## <a name="datetime"></a>DateTime  
 Il formato VT_DATE variant non è direttamente supportato dai tipi di dati XML-Data. Il formato corretto per le date con il componente di data e ora è aaaa-mm-ggThh.  
  
 Per altre informazioni su formati della data specificata da XML, vedere la [specifica W3C XML-Data](https://go.microsoft.com/fwlink/?LinkId=5692).  
  
 Quando la specifica di dati XML definisce due tipi di dati equivalenti (ad esempio, i4 = = int), ADO verrà scrive il nome descrittivo ma leggere in entrambi.  
  
## <a name="managing-pending-changes"></a>La gestione delle modifiche in sospeso  
 Un set di record possono essere aperti nell'immediato o in modalità di aggiornamento batch. Quando vengono aperti in modalità di aggiornamento batch con cursori sul lato client, tutte le modifiche apportate al set di record sono in stato di attesa fino a quando non viene chiamato il metodo UpdateBatch. Le modifiche in sospeso vengono inoltre mantenuti quando viene salvato il Recordset. Nel codice XML, sono rappresentati dall'utilizzo degli elementi "update" definita nell'urn: schemas-microsoft-com: rowset. Inoltre, se un set di righe possono essere aggiornati, le proprietà aggiornabili deve essere impostata true nella definizione della riga. Ad esempio, per definire che la tabella spedizionieri contiene modifiche in sospeso, la definizione di riga verrebbe aspetto sono simili alle seguenti.  
  
```  
<s:ElementType name="row" content="eltOnly" updatable="true">  
  <s:attribute type="ShipperID"/>  
  <s:attribute type="CompanyName"/>  
  <s:attribute type="Phone"/>  
  <s:extends type="rs:rowbase"/>  
</s:ElementType>  
```  
  
 Ciò indica al Provider di persistenza di dati sui dispositivi surface in modo che ADO può costruire un oggetto Recordset aggiornabile.  
  
 I dati di esempio seguente viene illustrato come gli inserimenti, le modifiche ed eliminazioni esaminare il file persistente.  
  
```  
<rs:data>  
  <z:row ShipperID="2" CompanyName="United Package"   
    Phone="(503) 555-3199"/>  
<rs:update>  
  <rs:original>  
    <z:row ShipperID="3" CompanyName="Federal Shipping"   
      Phone="(503) 555-9931"/>  
  </rs:original>  
  <z:row Phone="(503) 552-7134"/>  
</rs:update>  
<rs:insert>  
  <z:row ShipperID="12" CompanyName="Lightning Shipping"   
    Phone="(505) 111-2222"/>  
  <z:row ShipperID="13" CompanyName="Thunder Overnight"   
    Phone="(505) 111-2222"/>  
  <z:row ShipperID="14" CompanyName="Blue Angel Air Delivery"   
    Phone="(505) 111-2222"/>  
</rs:insert>  
<rs:delete>  
  <z:row ShipperID="1" CompanyName="Speedy Express" Phone="(503) 555-9831"/>  
</rs:delete>  
</rs:data>  
```  
  
 Un aggiornamento contiene sempre i dati della riga originale intero seguiti da dati della riga modificata. La riga modificata può contenere tutte le colonne o solo le colonne che sono stati effettivamente modificati. Nell'esempio precedente, non viene modificata la riga relativa spedizioniere 2 e solo la colonna telefono è stato modificato i valori per 3 spedizioniere e pertanto è l'unica colonna inclusa nella riga modificata. Le righe inserite per spedizionieri 12, 13 e 14 sono suddivisi in batch insieme rs: Inserisci in un tag. Si noti che le righe eliminate possono anche essere raggruppate, sebbene non illustrato nell'esempio precedente.  
  
## <a name="see-also"></a>Vedere anche  
 [Persistenza di record in formato XML](../../../ado/guide/data/persisting-records-in-xml-format.md)
