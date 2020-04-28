---
title: Introduzione agli updategram (SQLXML)
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
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
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 2c9e709a607d02273c0e2cb0208faf4e9799acf6
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "75252480"
---
# <a name="introduction-to-updategrams-sqlxml-40"></a>Introduzione sugli updategram (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  È possibile modificare (inserire, aggiornare o eliminare) un database in [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] da un documento XML esistente utilizzando un updategram o la funzione OPENXML [!INCLUDE[tsql](../../../includes/tsql-md.md)] .  
  
 La funzione OPENXML modifica un database suddividendo il documento XML esistente e fornendo un set di righe che può essere passato a un'istruzione INSERT, UPDATE o DELETE. Con OPENXML, le operazioni vengono eseguite direttamente sulle tabelle del database. OPENXML rappresenta pertanto la scelta più appropriata ogni volte che un provider di set di righe, ad esempio una tabella, può essere visualizzato come origine.  
  
 Analogamente a OPENXML, un updategram consente di inserire, aggiornare o eliminare dati nel database. Un updategram, tuttavia, agisce sulle viste XML fornite dallo schema XSD (o XDR) con annotazioni, applicando, ad esempio, gli aggiornamenti alla vista XML fornita dallo schema di mapping. Lo schema di mapping, a sua volta, dispone delle informazioni necessarie per eseguire il mapping di elementi e attributi XML alle tabelle e alle colonne di database corrispondenti. L'updategram utilizza queste informazioni di mapping per aggiornare le tabelle e le colonne di database.  
  
> [!NOTE]  
>  In questa documentazione si presuppone che l'utente disponga di una certa familiarità con i modelli e il supporto dello schema di mapping in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Per ulteriori informazioni, vedere [Introduzione agli schemi XSD con Annotazioni &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml/annotated-xsd-schemas/introduction-to-annotated-xsd-schemas-sqlxml-4-0.md). Per le applicazioni legacy che usano XDR, vedere la pagina relativa agli [schemi XDR con Annotazioni &#40;deprecati in SQLXML 4,0&#41;](../../../relational-databases/sqlxml/annotated-xsd-schemas/annotated-xdr-schemas-deprecated-in-sqlxml-4-0.md).  
  
## <a name="required-namespaces-in-the-updategram"></a>Spazi dei nomi necessari nell'updategram  
 Le parole chiave in un updategram, ad esempio ** \<Sync>**, ** \<before>** e ** \<after>**, sono presenti nello spazio dei nomi **urn: schemas-microsoft-com: xml-updategram** . Il prefisso dello spazio dei nomi utilizzato è arbitrario. In questa documentazione il prefisso **attributo updg** indica lo spazio dei nomi dell' **updategram** .  
  
## <a name="reviewing-syntax"></a>Esame della sintassi  
 Un updategram è un modello con ** \<>di sincronizzazione **, ** \<prima>** e ** \<dopo** i blocchi di>che formano la sintassi dell'updategram. Tale sintassi, nella sua forma più semplice, viene illustrata nel codice seguente:  
  
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
  
 **\<prima di>**  
 Identifica lo stato esistente, denominato anche "stato before", dell'istanza del record.  
  
 **\<dopo>**  
 Identifica il nuovo stato in cui devono essere modificati i dati.  
  
 **\<>di sincronizzazione**  
 Contiene i ** \<blocchi before>** e ** \<after>** . Un ** \<** blocco di>di sincronizzazione può contenere più di un set di ** \<prima>** e ** \<dopo>** blocchi. Se è presente più di un set di ** \<prima>** e ** \<dopo>** blocchi, questi blocchi (anche se sono vuoti) devono essere specificati come coppie. Un updategram può inoltre avere più di un ** \<blocco>di sincronizzazione** . Ogni ** \<** blocco del>di sincronizzazione è costituito da un'unità di transazione (il che significa che tutti gli ** \<** elementi del blocco>di sincronizzazione vengono eseguiti o non viene eseguita alcuna operazione). Se si specificano ** \<** più blocchi>di sincronizzazione in un updategram, l'errore di un ** \<blocco>di sincronizzazione** non influisce sugli altri ** \<blocchi>di sincronizzazione** .  
  
 Il fatto che un updategram elimini o inserisca o aggiorni un'istanza di record dipenda dal contenuto del ** \<prima>** e ** \<dopo>** blocchi:  
  
-   Se un'istanza di record viene visualizzata solo nel blocco ** \<before>** senza un'istanza corrispondente nel blocco ** \<after>** , l'updategram esegue un'operazione di eliminazione.  
  
-   Se un'istanza di record viene visualizzata solo nel blocco ** \<after>** senza un'istanza corrispondente nel blocco ** \<before>** , si tratta di un'operazione di inserimento.  
  
-   Se un'istanza di record viene visualizzata nel blocco ** \<before>** e dispone di un'istanza corrispondente nel blocco ** \<after>** , si tratta di un'operazione di aggiornamento. In questo caso, l'updategram aggiorna l'istanza del record ai valori specificati nel blocco ** \<after>** .  
  
## <a name="specifying-a-mapping-schema-in-the-updategram"></a>Definizione di uno schema di mapping nell'updategram  
 In un updategram l'astrazione XML fornita da uno schema di mapping (sono supportati gli schemi XSD e XDR) può essere implicita o esplicita, ovvero un updategram può essere utilizzato con o senza uno schema di mapping specificato. Se non si specifica uno schema di mapping, l'updategram presuppone un mapping implicito (il mapping predefinito), in cui ogni elemento nel blocco ** \<before>** o ** \<dopo>** viene mappato a una tabella e l'attributo o l'elemento figlio di ogni elemento viene mappato a una colonna nel database. Se si specifica in modo esplicito uno schema di mapping, gli elementi e gli attributi nell'updategram deve corrispondere agli elementi e agli attributi nello schema di mapping.  
  
### <a name="implicit-default-mapping"></a>Mapping implicito (predefinito)  
 Nella maggior parte dei casi, un updategram che esegue aggiornamenti semplici può non richiedere uno schema di mapping. In questo caso, l'updategram si basa sullo schema di mapping predefinito.  
  
 Nell'updategram seguente viene illustrato il mapping implicito. In questo esempio l'updategram inserisce un nuovo cliente nella tabella Sales.Customer. Poiché questo updategram utilizza il mapping implicito \<, l'elemento Sales. Customer> viene mappato alla tabella Sales. Customer e gli attributi CustomerID e SalesPersonID vengono mappati alle colonne corrispondenti nella tabella Sales. Customer.  
  
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
  
 Se l'updategram esegue un aggiornamento complesso, ad esempio l'inserimento di record in più tabelle in base alla relazione padre-figlio specificata nello schema di mapping, è necessario specificare in modo esplicito lo schema di mapping utilizzando l'attributo **mapping-schema** sul quale viene eseguito l'updategram.  
  
 Poiché un updategram è un modello, il percorso specificato per lo schema di mapping nell'updategram è relativo al percorso del file di modello (relativo alla posizione di archiviazione dell'updategram). Per ulteriori informazioni, vedere [specifica di uno schema di mapping con annotazioni in un Updategram &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md).  
  
## <a name="element-centric-and-attribute-centric-mapping-in-updategrams"></a>Mapping incentrato sugli elementi e mapping incentrato sugli attributi negli updategram  
 Utilizzando il mapping predefinito, quando lo schema di mapping non viene specificato nell'updategram, gli elementi dell'updategram vengono mappati a tabelle, mentre gli elementi figlio (nel caso di mapping incentrato sugli elementi) e gli attributi (nel caso di mapping incentrato sugli attributi) vengono mappati a colonne.  
  
### <a name="element-centric-mapping"></a>Mapping incentrato sugli elementi  
 In un updategram incentrato sugli elementi, un elemento contiene elementi figlio che indicano le proprietà dell'elemento. Si consideri, ad esempio, l'updategram seguente. L' ** \<elemento Person. Contact>** contiene i ** \<>FirstName **e ** \<LastName>** elementi figlio. Questi elementi figlio sono proprietà dell'elemento ** \<person. Contact>** .  
  
 Poiché questo updategram non specifica uno schema di mapping, l'updategram utilizza il mapping implicito, in cui l' ** \<elemento Person. Contact>** viene mappato alla tabella Person. Contact e i relativi elementi figlio vengono mappati alle colonne FirstName e LastName.  
  
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
 In un mapping incentrato sugli attributi, gli elementi includono attributi. Nell'updategram seguente viene utilizzato il mapping incentrato sugli attributi. In questo esempio l' ** \<elemento Person. Contact>** è costituito dagli attributi **FirstName** e **LastName** . Questi attributi sono le proprietà dell'elemento ** \<person. Contact>** . Come nell'esempio precedente, questo updategram non specifica alcuno schema di mapping, pertanto si basa sul mapping implicito per eseguire il mapping della ** \<persona. Contattare>** elemento alla tabella Person. Contact e gli attributi dell'elemento alle rispettive colonne nella tabella.  
  
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
 È possibile specificare una combinazione di mapping incentrato sugli elementi e mapping incentrato sugli attributi, come illustrato nell'updategram seguente. Si noti che l' ** \<elemento Person. Contact>** contiene sia un attributo sia un elemento figlio. L'updategram si basa inoltre su un mapping implicito. Pertanto, l'attributo **FirstName** e ** \<LastName>** elemento figlio vengono mappati alle colonne corrispondenti nella tabella Person. Contact.  
  
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
  
 Per codificare i caratteri che [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] sono identificatori validi ma non sono identificatori XML validi, usare\_\_' __xHHHH ' come valore di codifica, dove HHHH rappresenta il codice UCS-2 esadecimale a quattro cifre per il carattere nell'ordine del primo bit più significativo. Utilizzando questo schema di codifica, un carattere spazio viene sostituito con x0020 (il codice esadecimale a quattro cifre per uno spazio); in questo modo, il nome della tabella [Order [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Details] in diventa _X005B_ORDER_X0020_DETAILS_X005D\_ in XML.  
  
 Analogamente, potrebbe essere necessario specificare nomi di elementi in tre parti, ad \<esempio [database]. [proprietario]. [Table] >. Poiché i caratteri parentesi quadre ([e]) non sono validi in XML, è necessario \<specificarli\_come _x005B_database_x005D\_. _x005B_owner_x005D\_ . _x005B_table_x005D>,\_ dove _x005B è la codifica per la parentesi quadra aperta ([\_ ) e _x005D è la codifica per la parentesi quadra chiusa (]).  
  
## <a name="executing-updategrams"></a>Esecuzione di updategram  
 Poiché un updategram è un modello, utilizza tutti i meccanismi di elaborazione di un modello. Per SQLXML 4.0, è possibile eseguire un updategram in una delle modalità seguenti:  
  
-   Inviandolo in un comando ADO.  
  
-   Inviandolo come comando OLE DB.  
  
## <a name="see-also"></a>Vedere anche  
 [Considerazioni sulla sicurezza degli updategram &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
