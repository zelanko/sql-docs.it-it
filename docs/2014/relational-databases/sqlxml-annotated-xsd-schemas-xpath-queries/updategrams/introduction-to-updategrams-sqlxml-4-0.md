---
title: Introduzione alle Updategram (SQLXML 4.0) | Documenti di Microsoft
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- explicit schema mapping [SQLXML]
- updategrams [SQLXML], mapping schema specifying
- namespaces [SQLXML]
- updategrams [SQLXML], about updategrams
- attribute-centric mapping
- invalid characters [SQLXML]
- element-centric mapping [SQLXML]
- mapping schema [SQLXML], updategrams
- namespaces [SQLXML], updategrams
- executing updategrams [SQLXML]
- implicit schema mapping
ms.assetid: cfe24e82-a645-4f93-ab16-39c21f90cce6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 114bc96623b608cfbb520a9d2f35f23a04310a74
ms.sourcegitcommit: 45a9d7ffc99502c73f08cb937cbe9e89d9412397
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/22/2019
ms.locfileid: "66014796"
---
# <a name="introduction-to-updategrams-sqlxml-40"></a>Introduzione sugli updategram (SQLXML 4.0)
  È possibile modificare (insert, update e delete) in un database di [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] da esistenti documento XML utilizzando un updategram o l'istruzione OPENXML [!INCLUDE[tsql](../../../includes/tsql-md.md)] funzione.  
  
 La funzione OPENXML modifica un database suddividendo il documento XML esistente e fornendo un set di righe che può essere passato a un'istruzione INSERT, UPDATE o DELETE. Con OPENXML, le operazioni vengono eseguite direttamente sulle tabelle del database. OPENXML rappresenta pertanto la scelta più appropriata ogni volte che un provider di set di righe, ad esempio una tabella, può essere visualizzato come origine.  
  
 Analogamente a OPENXML, un updategram consente di inserire, aggiornare o eliminare dati nel database. Un updategram, tuttavia, agisce sulle viste XML fornite dallo schema XSD (o XDR) con annotazioni, applicando, ad esempio, gli aggiornamenti alla vista XML fornita dallo schema di mapping. Lo schema di mapping, a sua volta, dispone delle informazioni necessarie per eseguire il mapping di elementi e attributi XML alle tabelle e alle colonne di database corrispondenti. L'updategram utilizza queste informazioni di mapping per aggiornare le tabelle e le colonne di database.  
  
> [!NOTE]  
>  In questa documentazione si presuppone che l'utente disponga di una certa familiarità con i modelli e il supporto dello schema di mapping in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Per altre informazioni, vedere [Introduzione agli schemi XSD con annotazioni &#40;SQLXML 4.0&#41;](../../sqlxml/annotated-xsd-schemas/introduction-to-annotated-xsd-schemas-sqlxml-4-0.md). Per le applicazioni legacy che utilizzano XDR, vedere [schemi XDR con annotazioni &#40;deprecato in SQLXML 4.0&#41;](../../sqlxml/annotated-xsd-schemas/annotated-xdr-schemas-deprecated-in-sqlxml-4-0.md).  
  
## <a name="required-namespaces-in-the-updategram"></a>Spazi dei nomi necessari nell'updategram  
 Le parole chiave in un updategram, ad esempio  **\<sincronizzazione >**,  **\<prima >**, e  **\<dopo >**, esiste la `urn:schemas-microsoft-com:xml-updategram`dello spazio dei nomi. Il prefisso dello spazio dei nomi utilizzato è arbitrario. In questa documentazione il prefisso `updg` indica lo spazio dei nomi `updategram`.  
  
## <a name="reviewing-syntax"></a>Esame della sintassi  
 Un updategram è un modello con  **\<sincronizzazione >**,  **\<prima >**, e  **\<dopo >** blocchi che costituiscono la sintassi del Updategram. Tale sintassi, nella sua forma più semplice, viene illustrata nel codice seguente:  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync [mapping-schema= "AnnotatedSchemaFile.xml"] >  
    <updg:before>  
        ...  
    </updg:before>  
    <updg:after>  
        ...  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
 Nelle definizioni seguenti viene descritto il ruolo di ogni blocco:  
  
 **\<before>**  
 Identifica lo stato esistente, denominato anche "stato before", dell'istanza del record.  
  
 **\<after>**  
 Identifica il nuovo stato in cui devono essere modificati i dati.  
  
 **\<sync>**  
 Contiene il  **\<prima >** e  **\<dopo >** blocchi. Un  **\<sincronizzazione >** blocco può contenere più di un set di  **\<prima >** e  **\<dopo >** blocchi. Se è presente più di un set di  **\<prima >** e  **\<dopo >** blocchi, questi blocchi (anche se vuote) deve essere specificato come coppie. Inoltre, un updategram può avere più di un  **\<sincronizzazione >** blocco. Ogni  **\<sincronizzazione >** blocco è un'unità di transazione (vale a dire che l'intero contenuto di  **\<sincronizzazione >** blocco viene eseguita o non viene eseguita). Se si specificano più  **\<sincronizzazione >** blocchi in un updategram, il guasto di uno  **\<sincronizzazione >** non influenzano l'altro blocco  **\<sincronizzazione >** blocchi.  
  
 Se un updategram Elimina, inserisce o aggiorna un'istanza del record dipende dal contenuto di  **\<prima >** e  **\<dopo >** blocchi:  
  
-   Se un'istanza del record viene visualizzata solo nel  **\<prima >** blocco con alcuna istanza corrispondente nel  **\<dopo >** blocco, updategram esegue un'operazione di eliminazione.  
  
-   Se un'istanza del record viene visualizzata solo nella  **\<dopo >** blocco con alcuna istanza corrispondente nel  **\<prima >** blocco, è un'operazione di inserimento.  
  
-   Se è presente un'istanza di record di  **\<prima >** blocco e non è un'istanza corrispondente il  **\<dopo >** blocco, è un'operazione di aggiornamento. In questo caso, updategram Aggiorna l'istanza del record per i valori specificati nella  **\<dopo >** blocco.  
  
## <a name="specifying-a-mapping-schema-in-the-updategram"></a>Definizione di uno schema di mapping nell'updategram  
 In un updategram l'astrazione XML fornita da uno schema di mapping (sono supportati gli schemi XSD e XDR) può essere implicita o esplicita, ovvero un updategram può essere utilizzato con o senza uno schema di mapping specificato. Se non si specifica uno schema di mapping, updategram presuppone un mapping implicito (il mapping predefinito), dove ogni elemento di  **\<prima >** blocco o  **\<dopo >** blocco associato a una tabella e l'elemento figlio di ciascun elemento o attributo associato a una colonna del database. Se si specifica in modo esplicito uno schema di mapping, gli elementi e gli attributi nell'updategram deve corrispondere agli elementi e agli attributi nello schema di mapping.  
  
### <a name="implicit-default-mapping"></a>Mapping implicito (predefinito)  
 Nella maggior parte dei casi, un updategram che esegue aggiornamenti semplici può non richiedere uno schema di mapping. In questo caso, l'updategram si basa sullo schema di mapping predefinito.  
  
 Nell'updategram seguente viene illustrato il mapping implicito. In questo esempio l'updategram inserisce un nuovo cliente nella tabella Sales.Customer. Poiché questo updategram utilizza mapping implicito, la \<Sales. Customer > elemento viene associato alla tabella Sales. Customer e gli attributi CustomerID e SalesPersonID il mapping alle colonne corrispondenti della tabella Sales. Customer.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:sync >  
<updg:before>  
</updg:before>  
<updg:after>  
    <Sales.Customer CustomerID="1" SalesPersonID="277" />  
    </updg:after>  
</updg:sync>  
</ROOT>  
```  
  
### <a name="explicit-mapping"></a>Mapping esplicito  
 Se si specifica uno schema di mapping (XSD o XDR), l'updategram utilizza lo schema per determinare le tabelle e le colonne di database che devono essere aggiornate.  
  
 Se l'updategram esegue un aggiornamento complesso, ad esempio l'inserimento di record in più tabelle sulla base della relazione padre-figlio specificata nello schema di mapping, è necessario fornire in modo esplicito lo schema di mapping tramite l'attributo `mapping-schema` sui cui viene eseguito l'updategram.  
  
 Poiché un updategram è un modello, il percorso specificato per lo schema di mapping nell'updategram è relativo al percorso del file di modello (relativo alla posizione di archiviazione dell'updategram). Per ulteriori informazioni, vedere [l'impostazione di uno Schema di Mapping annotati in un Updategram &#40;SQLXML 4.0&#41;](specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md).  
  
## <a name="element-centric-and-attribute-centric-mapping-in-updategrams"></a>Mapping incentrato sugli elementi e mapping incentrato sugli attributi negli updategram  
 Utilizzando il mapping predefinito, quando lo schema di mapping non viene specificato nell'updategram, gli elementi dell'updategram vengono mappati a tabelle, mentre gli elementi figlio (nel caso di mapping incentrato sugli elementi) e gli attributi (nel caso di mapping incentrato sugli attributi) vengono mappati a colonne.  
  
### <a name="element-centric-mapping"></a>Mapping incentrato sugli elementi  
 In un updategram incentrato sugli elementi, un elemento contiene elementi figlio che indicano le proprietà dell'elemento. Si consideri, ad esempio, l'updategram seguente. Il  **\<Person. Contact >** elemento contiene il  **\<nome >** e  **\<LastName >** gli elementi figlio. Gli elementi figlio sono proprietà del  **\<Person. Contact >** elemento.  
  
 Poiché questo updategram non viene specificato uno schema di mapping, updategram utilizza mapping implicito, dove il  **\<Person. Contact >** elemento associa la tabella Person. Contact e relativi elementi figlio della mappa per nome e Colonne LastName.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:sync >  
  <updg:after>  
    <Person.Contact>  
       <FirstName>Catherine</FirstName>  
       <LastName>Abel</LastName>  
    </Person.Contact>  
  </updg:after>  
</updg:sync>  
</ROOT>  
```  
  
### <a name="attribute-centric-mapping"></a>mapping incentrato sugli attributi  
 In un mapping incentrato sugli attributi, gli elementi includono attributi. Nell'updategram seguente viene utilizzato il mapping incentrato sugli attributi. In questo esempio, il  **\<Person. Contact >** elemento costituito il **FirstName** e **LastName** gli attributi. Questi attributi sono proprietà del  **\<Person. Contact >** elemento. Come nell'esempio precedente, questa updategram specifica nessuno schema di mapping, in modo da cui dipende la mappatura implicita per eseguire il mapping di  **\<Person. Contact >** elemento per la tabella Person. Contact e gli attributi dell'elemento per il rispettive colonne della tabella.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:sync >  
  <updg:before>  
  </updg:before>  
  <updg:after>  
    <Person.Contact FirstName="Catherine" LastName="Abel" />  
  </updg:after>  
</updg:sync>  
</ROOT>  
```  
  
### <a name="using-both-element-centric-and-attribute-centric-mapping"></a>Utilizzo di una combinazione di mapping incentrato sugli elementi e mapping incentrato sugli attributi  
 È possibile specificare una combinazione di mapping incentrato sugli elementi e mapping incentrato sugli attributi, come illustrato nell'updategram seguente. Si noti che il  **\<Person. Contact >** elemento contiene sia un attributo e un elemento figlio. L'updategram si basa inoltre su un mapping implicito. In questo modo, il **FirstName** attributo e il  **\<LastName >** mapping alle colonne corrispondenti della tabella Person. Contact dell'elemento figlio.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:sync >  
  <updg:before>  
  </updg:before>  
  <updg:after>  
    <Person.Contact FirstName="Catherine" >  
       <LastName>Abel</LastName>  
    </Person.Contact>  
  </updg:after>  
</updg:sync>  
</ROOT>  
```  
  
## <a name="working-with-characters-valid-in-sql-server-but-not-valid-in-xml"></a>Utilizzo di caratteri validi in SQL Server ma non validi in XML  
 In [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] i nomi di tabella possono includere uno spazio. Questo tipo di nome di tabella, tuttavia, non è valido in XML.  
  
 Per codificare i caratteri validi [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] identificatori ma non sono identificatori XML validi, usare ' __xHHHH\_\_' come valore di codifica, dove HHHH rappresenta il codice UCS-2 esadecimale a quattro cifre per il carattere in più ordine del primo bit significativo. Utilizzando questa schema di codifica, un carattere di spazio viene sostituito da x0020 (il a quattro cifre esadecimale codice per il carattere spazio); di conseguenza, il nome della tabella [Dettagli ordine] in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] diventa _x005B_Order_x0020_Details_x005D\_ in XML.  
  
 Analogamente, potrebbe essere necessario specificare i nomi di elemento in tre parti, ad esempio \<[database]. [ proprietario]. [tabella] >. Poiché i caratteri parentesi quadra ([e]) non sono validi in XML, è necessario specificare questo elemento come \<_x005B_database_x005D\_._x005B_owner_x005D\_._x005B_table_x005D\_>, dove _x005B\_ è la codifica per la parentesi quadra aperta ([) e _x005D\_ la codifica per la parentesi quadra chiusa (]).  
  
## <a name="executing-updategrams"></a>Esecuzione di updategram  
 Poiché un updategram è un modello, utilizza tutti i meccanismi di elaborazione di un modello. Per SQLXML 4.0, è possibile eseguire un updategram in una delle modalità seguenti:  
  
-   Inviandolo in un comando ADO.  
  
-   Inviandolo come comando OLE DB.  
  
## <a name="see-also"></a>Vedere anche  
 [Considerazioni sulla sicurezza degli updategram &#40;SQLXML 4.0&#41;](../security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
