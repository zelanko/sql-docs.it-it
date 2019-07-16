---
title: Riferimento al linguaggio XQuery (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
helpviewer_keywords:
- XQuery
- XQuery, about XQuery
- xml data type [SQL Server], XQuery
- XML [SQL Server], XQuery
- queries [XML in SQL Server], XQuery
ms.assetid: 8a69344f-2990-4357-8160-cb26aac95b91
author: rothja
ms.author: jroth
ms.openlocfilehash: 87edbeaac26ca1c332efe981901cbf0bc57fed30
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67945961"
---
# <a name="xquery-language-reference-sql-server"></a>Riferimento al linguaggio XQuery (SQL Server)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[tsql](../includes/tsql-md.md)] supporta un subset del linguaggio XQuery utilizzato per l'esecuzione di query di **xml** tipo di dati. Questa implementazione di XQuery è allineata con le specifiche Working Draft di XQuery del luglio 2004. Il linguaggio è sviluppato da WC3 (World Wide Web Consortium), con la partecipazione di tutti i principali fornitori di database e di Microsoft. Poiché le specifiche W3C sono soggette a modifiche prima di diventare raccomandazioni ufficiali, questa implementazione può essere diversa dalla raccomandazione W3C finale. In questo argomento vengono descritte la semantica e la sintassi del subset di XQuery supportato in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
 Per altre informazioni, vedere la [specifica del linguaggio XQuery 1.0 W3C](https://go.microsoft.com/fwlink/?LinkId=48846).  
  
 Il linguaggio XQuery consente di eseguire query su dati XML strutturati e semistrutturati. Con il **xml** supporto viene fornito nel tipo di dati di [!INCLUDE[ssDE](../includes/ssde-md.md)], i documenti possono essere archiviati in un database e quindi eseguire una query utilizzando XQuery.  
  
 Il linguaggio XQuery è basato sul linguaggio di query XPath esistente e supporta inoltre miglioramenti per le iterazioni e l'ordinamento, nonché la possibilità di costruire il codice XML necessario. XQuery opera sul modello di dati XQuery. Si tratta di un modello di astrazione dei documenti XML e i risultati XQuery possono essere tipizzati o non tipizzati. Le informazioni sui tipi sono basate sui tipi definiti nelle specifiche W3C per il linguaggio XML Schema. Se non sono disponibili informazioni di tipizzazione, XQuery gestisce i dati come non tipizzati, analogamente al modo in cui XPath versione 1.0 gestisce i dati XML.  
  
 Per eseguire un'istanza XML archiviata in una variabile o colonna di una query **xml** tipo, utilizzare il [metodi con tipo di dati xml](../t-sql/xml/xml-data-type-methods.md). Ad esempio, è possibile dichiarare una variabile di **xml** digitare ed eseguire una query usando la **query ()** metodo il **xml** tipo di dati.  
  
```sql
DECLARE @x xml  
SET @x = '<ROOT><a>111</a></ROOT>'  
SELECT @x.query('/ROOT/a')  
```  
  
 Nell'esempio seguente, la query viene specificata sulla colonna Instructions della **xml** tipo nella tabella ProductModel nel database AdventureWorks.  
  
```sql
SELECT Instructions.query('declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";           
    /AWMI:root/AWMI:Location[@LocationID=10]  
') as Result   
FROM  Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 L'espressione XQuery include la dichiarazione dello spazio dei nomi, `declare namespace``AWMI=...`, l'espressione di query e `/AWMI:root/AWMI:Location[@LocationID=10]`.  
  
 Si noti che la query XQuery viene specificata sulla colonna Instructions della **xml** tipo. Il [metodo query ()](../t-sql/xml/query-method-xml-data-type.md) dei dati xml tipo viene usato per specificare la query XQuery.  
  
 Nella tabella seguente sono elencati gli argomenti correlati utili per comprendere l'implementazione di XQuery in [!INCLUDE[ssDE](../includes/ssde-md.md)].  
  
|Argomento|Descrizione|  
|-----------|-----------------|  
|[Dati XML &#40;SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)|Descrive il supporto per la **xml**tipo di dati di [!INCLUDE[ssDE](../includes/ssde-md.md)] e i metodi utilizzabili su questo tipo di dati. Il **xml** form in cui vengono eseguite le espressioni XQuery del modello di dati XQuery di input del tipo di dati.|  
|[Raccolte di XML Schema &#40;SQL Server&#41;](../relational-databases/xml/xml-schema-collections-sql-server.md)|Descrive le procedure per tipizzare le istanze XML archiviate in un database, Ciò significa che è possibile associare una raccolta di XML schema con il **xml** colonna di tipo. Tutte le istanze archiviate nella colonna vengono convalidate e tipizzate rispetto allo schema della raccolta e forniscono le informazioni sul tipo per XQuery.|  
|||  
  
> [!NOTE]  
>  L'organizzazione di questa sezione è basata sulle specifiche W3C (World Wide Web Consortium ) per XQuery. Alcuni dei diagrammi disponibili in questa sezione provengono da questa specifica. In questa sezione l'implementazione Microsoft di XQuery viene confrontata alla specifica W3C, vengono descritte le differenze fra Microsoft XQuery e la specifica W3C e vengono illustrate le caratteristiche W3C non supportate. La specifica W3C è disponibile all'indirizzo [ http://www.w3.org/TR/2004/WD-xquery-20040723 ](https://go.microsoft.com/fwlink/?LinkId=48846).  
  
## <a name="in-this-section"></a>In questa sezione  
  
|Argomento|Descrizione|  
|-----------|-----------------|  
|[Nozioni fondamentali su XQuery](../xquery/xquery-basics.md)|Contiene una panoramica di base sui concetti relativi a XQuery, valutazione dell'espressione (contesto statico e dinamico), atomizzazione, valore booleano effettivo, sistema di tipi XQuery, corrispondenza del tipo di sequenza e gestione degli errori.|  
|[Espressioni XQuery](../xquery/xquery-expressions.md)|Descrive le espressioni primarie XQuery, espressioni di percorso, espressioni di sequenza, espressioni di confronto aritmetico e logiche, costruzione XQuery, espressione FLWOR, espressioni condizionali e quantificate e diverse espressioni TypeSequence.|  
|[Moduli e prologhi &#40;XQuery&#41;](../xquery/modules-and-prologs-xquery.md)|Descrive il prologo della XQuery.|  
|[Funzioni XQuery per il tipo di dati XML](../xquery/xquery-functions-against-the-xml-data-type.md)|Contiene un elenco delle funzioni XQuery supportate.|  
|[Operatori di XQuery per il tipo di dati xml](../xquery/xquery-operators-against-the-xml-data-type.md)|Descrive gli operatori XQuery supportati.|  
|[Query XQuery di esempio aggiuntive per il tipo di dati xml](../xquery/additional-sample-xqueries-against-the-xml-data-type.md)|Contiene altri esempi di XQuery.|  
  
## <a name="see-also"></a>Vedere anche  
 [Dati XML &#40;SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)   
 [Raccolte di XML Schema &#40;SQL Server&#41;](../relational-databases/xml/xml-schema-collections-sql-server.md)   
 [Esempi di importazione ed esportazione bulk di documenti XML &#40;SQL Server&#41;](../relational-databases/import-export/examples-of-bulk-import-and-export-of-xml-documents-sql-server.md)  
  
  
