---
title: Eliminazione di dati mediante updategram XML (SQLXML 4,0) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- <after> block
- updategrams [SQLXML], deleting data
- <before> block
- mapping-schema attribute
- record deletions [SQLXML]
ms.assetid: 4fb116d7-7652-474a-a567-cb475a20765c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 444ef7d8c95b0cbd41ba3fbb55a6fbeb30870462
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66014873"
---
# <a name="deleting-data-using-xml-updategrams-sqlxml-40"></a>Eliminazione di dati mediante updategram XML (SQLXML 4.0)
  Un updategram indica un'operazione di eliminazione quando un'istanza di record viene visualizzata nel blocco ** \<before>** senza record corrispondenti nel blocco ** \<after>** . In questo caso, l'updategram elimina il record nel ** \<>prima** del blocco dal database.  
  
 Di seguito viene illustrato il formato dell'updategram per un'operazione di eliminazione:  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync [mapping-schema="SampleSchema.xml"]  >  
   <updg:before>  
       <ElementName />  
      [<ElementName .../>... ]  
   </updg:before>  
    [<updg:after>  
    </updg:after>]  
  </updg:sync>  
</ROOT>  
```  
  
 È possibile omettere il ** \<Tag after>** se l'updategram sta eseguendo solo un'operazione di eliminazione. Se non si specifica l'attributo facoltativo `mapping-schema` , l' ** \<elemento ElementName>** specificato nell'updategram esegue il mapping a una tabella di database e gli attributi o gli elementi figlio eseguono il mapping alle colonne della tabella.  
  
 Se un elemento specificato nell'updategram corrisponde a più di una riga nella tabella o non corrisponde ad alcuna riga, l'updategram restituisce un errore e Annulla l'intero ** \<blocco>di sincronizzazione** . Un elemento dell'updategram può eliminare un solo record per volta.  
  
## <a name="examples"></a>Esempi  
 Negli esempi presentati in questa sezione viene utilizzato il mapping predefinito, ovvero non viene specificato alcuno schema di mapping nell'updategram. Per ulteriori esempi di updategram che utilizzano schemi di mapping, vedere [specifica di uno schema di mapping con annotazioni in un Updategram &#40;SQLXML 4,0&#41;](specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md).  
  
 Per creare esempi funzionanti utilizzando gli esempi seguenti, è necessario soddisfare i requisiti specificati nei [requisiti per l'esecuzione di esempi SQLXML](../../sqlxml/requirements-for-running-sqlxml-examples.md).  
  
### <a name="a-deleting-a-record-by-using-an-updategram"></a>R. Eliminazione di un record mediante un updategram  
 Negli updategram seguenti vengono eliminati due record dalla tabella HumanResources.Shift.  
  
 In questi esempi l'updategram non specifica uno schema di mapping, pertanto utilizza il mapping predefinito nel quale il nome dell'elemento esegue il mapping a un nome di tabella e gli attributi o i sottoelementi eseguono il mapping alle colonne.  
  
 Il primo updategram è incentrato sugli attributi e identifica due turni (giorno-sera e sera-notte) nel blocco ** \<before>** . Poiché non esiste un record corrispondente nel blocco ** \<after>** , si tratta di un'operazione di eliminazione.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:sync >  
  <updg:before>  
       <HumanResources.Shift ShiftID="4"  
                        Name="Day-Evening"  
                        StartTime="1900-01-01 11:00:00.000"  
                        EndTime="1900-01-01 19:00:00.000"  
                        ModifiedDate="2004-01-01 00:00:00.000" />  
       <HumanResources.Shift ShiftID="5"  
                        Name="Evening-Night"  
                        StartTime="1900-01-01 19:00:00.000"  
                        EndTime="1900-01-01 03:00:00.000"  
                        ModifiedDate="2004-01-01 00:00:00.000" />  
  </updg:before>  
  <updg:after>  
  </updg:after>  
</updg:sync>  
</ROOT>  
```  
  
##### <a name="to-test-the-updategram"></a>Per testare l'updategram  
  
1.  Completare l'esempio B ("inserimento di più record utilizzando un updategram") nell' [inserimento di dati tramite UPDATEGRAM XML &#40;SQLXML 4,0&#41;](inserting-data-using-xml-updategrams-sqlxml-4-0.md).  
  
2.  Copiare l'updategram precedente nel blocco note e salvarlo come Updategram-RemoveShifts. XML nella stessa cartella utilizzata per completare ("inserimento di più record utilizzando un updategram") nell' [inserimento di dati mediante UPDATEGRAM xml &#40;SQLXML 4,0&#41;](inserting-data-using-xml-updategrams-sqlxml-4-0.md).  
  
3.  Creare e utilizzare lo script di test SQLXML 4.0 (Sqlxml4test.vbs) per eseguire l'updategram.  
  
     Per ulteriori informazioni, vedere [utilizzo di ADO per eseguire query SQLXML 4,0](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Considerazioni sulla sicurezza degli updategram &#40;SQLXML 4,0&#41;](../security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
