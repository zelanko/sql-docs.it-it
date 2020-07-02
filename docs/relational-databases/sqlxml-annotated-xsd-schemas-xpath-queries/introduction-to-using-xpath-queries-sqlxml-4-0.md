---
title: Introduzione all'utilizzo di query XPath (SQLXML)
description: Informazioni di base sull'utilizzo di query XPath in SQLXML 4,0.
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- XPath queries [SQLXML], about XPath queries
- W3C XPath specification
- XPath queries [SQLXML], functionality
ms.assetid: 01050a8e-0ccc-4a02-a4eb-b48be5c3f4f3
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 544a8741557c222577f124014d6a04a9d066add1
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85649764"
---
# <a name="introduction-to-using-xpath-queries-sqlxml-40"></a>Introduzione all'utilizzo di query XPath (SQLXML 4.0)
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  Una query XPath (XML Path Language) può essere specificata come parte di un URL o all'interno di un modello. La struttura del frammento risultante viene determinata dallo schema di mapping mentre i valori vengono recuperati dal database. Questo processo è concettualmente simile alla creazione di viste mediante l'istruzione CREATE VIEW e alla scrittura di query SQL relative a tali viste.  
  
> [!NOTE]  
>  Per comprendere le query XPath in SQLXML 4.0, è necessario avere familiarità con le viste XML e con concetti correlati quali i modelli e lo schema di mapping. Per ulteriori informazioni, vedere [Introduzione agli schemi XSD con Annotazioni &#40;SQLXML 4,0&#41;](../../relational-databases/sqlxml/annotated-xsd-schemas/introduction-to-annotated-xsd-schemas-sqlxml-4-0.md)e lo standard XPath definito dalla World Wide Web Consortium (W3C).  
  
 Un documento XML è costituito da nodi, quali un nodo di elemento, un nodo di attributo, un nodo di testo e così via. Si consideri, ad esempio, il documento XML seguente:  
  
```  
<root>  
  <Customer cid= "C1" name="Janine" city="Issaquah">  
      <Order oid="O1" date="1/20/1996" amount="3.5" />  
      <Order oid="O2" date="4/30/1997" amount="13.4">Customer was  
          very satisfied</Order>  
   </Customer>  
   <Customer cid="C2" name="Ursula" city="Oelde" >  
      <Order oid="O3" date="7/14/1999" amount="100" note="Wrap it blue white red">  
          <Urgency>Important</Urgency>  
      </Order>  
      <Order oid="O4" date="1/20/1996" amount="10000"/>  
   </Customer>  
</root>  
```  
  
 In questo documento, **\<Customer>** è un nodo di elemento, **CID** è un nodo di attributo e **"important"** è un nodo di testo.  
  
 XPath è un linguaggio di navigazione grafica utilizzato per selezionare un set di nodi da un documento XML. Ogni operatore XPath consente di selezionare un set di nodi in base a un set di nodi selezionato da un operatore XPath precedente. Dato un set di **\<Customer>** nodi, ad esempio, XPath può selezionare tutti **\<Order>** i nodi con il valore dell'attributo **date** **"7/14/1999"**. Il set di nodi risultante contiene tutti gli ordini con data 7/14/1999.  
  
 Il linguaggio XPath è definito dal World Wide Web Consortium (W3C) come linguaggio di navigazione standard. SQLXML 4,0 implementa un subset della specifica XPath W3C, disponibile in http://www.w3.org/TR/1999/PR-xpath-19991008.html .  
  
 Di seguito vengono elencate alcune delle differenze principali tra l'implementazione di XPath del W3C e l'implementazione di SQLXML 4.0.  
  
-   **Query radice**  
  
     SQLXML 4.0 non supporta la query radice (/). Ogni query XPath deve iniziare a un livello superiore dello **\<ElementType>** schema.  
  
-   **Segnalazione di errori**  
  
     La specifica XPath del W3C non definisce condizioni di errore. Le query XPath che non consentono di selezionare nodi restituiscono un set di nodi vuoto. In SQLXML 4.0 una query può restituire diversi tipi di messaggio di errore.  
  
-   **Ordine del documento**  
  
     In SQLXML 4.0 l'ordine dei documenti non è sempre definito. Pertanto, i predicati numerici e gli assi che usano l'ordine del documento (ad esempio, il **codice seguente**) non sono implementati.  
  
     La mancanza di un ordine dei documenti indica inoltre che il valore di stringa di un nodo può essere valutato solo se il nodo in questione è mappato a una singola colonna in una singola riga. Non è possibile convertire in stringa un elemento con elementi figlio o un nodo IDREFS o NMTOKENS.  
  
    > [!NOTE]  
    >  In alcuni casi, l'annotazione o le chiavi dei **campi chiave** dall'annotazione della **relazione** possono determinare un ordine deterministico dei documenti. Tuttavia, questo non è l'uso principale di queste annotazioni per ulteriori informazioni, vedere [identificazione delle colonne chiave mediante SQL: key-fields &#40;sqlxml 4,0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/identifying-key-columns-using-sql-key-fields-sqlxml-4-0.md) e [specifica di relazioni con sql: relationship &#40;SQLXML 4,0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/specifying-relationships-using-sql-relationship-sqlxml-4-0.md).  
  
-   **Tipi di dati**  
  
     SQLXML 4,0 presenta limitazioni nell'implementazione dei tipi di dati **stringa**, **numero**e **booleano** XPath. Per ulteriori informazioni, vedere [tipi di dati XPath &#40;SQLXML 4,0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/xpath-data-types-sqlxml-4-0.md).  
  
-   **Query di prodotto incrociato**  
  
     SQLXML 4.0 non supporta query XPath di prodotto incrociato, quale `Customers[Order/@OrderDate=Order/@ShipDate]`. In questa query vengono selezionati tutti gli elementi Customer con un elemento Order per il quale OrderDate è uguale a ShipDate di un elemento Order qualsiasi.  
  
     SQLXML 4.0 non supporta invece query come `Customer[Order[@OrderDate=@ShippedDate]]`, in cui vengono selezionati gli elementi Customer con elemento Order per il quale OrderDate è uguale al relativo elemento ShipDate.  
  
-   **Gestione degli errori e sicurezza**  
  
     A seconda dello schema e dell'espressione di query XPath utilizzati, è possibile che gli errori [!INCLUDE[tsql](../../includes/tsql-md.md)] vengano esposti agli utenti in determinate condizioni.  
  
 Nelle tabelle delle sezioni seguenti vengono forniti dettagli su come l'implementazione nelle aree indicate delle query XPath in SQLXML 4.0 sia diversa da quella definita nella specifica del W3C.  
  
## <a name="supported-functionality"></a>Funzionalità supportata  
 Nella tabella seguente vengono mostrate le caratteristiche del linguaggio XPath implementate in SQLXML 4.0.  
  
|Funzionalità|Elemento|Collegamento a query di esempio|  
|-------------|----------|----------------------------|  
|Assi|**attributi**, **figlio**, **padre**e assi **autonomi**|[Specifica di assi in query XPath &#40;SQLXML 4,0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/specifying-axes-in-xpath-queries-sqlxml-4-0.md)|  
|Predicati con valori booleani, tra i quali sono inclusi predicati successivi e nidificati||[Specifica di operatori aritmetici nelle query XPath &#40;SQLXML 4,0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/specifying-arithmetic-operators-in-xpath-queries-sqlxml-4-0.md)|  
|Tutti gli operatori relazionali|=,! =, <, \<=, > , >=|[Specifica di operatori relazionali nelle query XPath &#40;SQLXML 4,0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/specifying-relational-operators-in-xpath-queries-sqlxml-4-0.md)|  
|Operatori aritmetici|+, -, *, div|[Specifica di operatori aritmetici nelle query XPath &#40;SQLXML 4,0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/specifying-arithmetic-operators-in-xpath-queries-sqlxml-4-0.md)|  
|Funzioni di conversione esplicita|**numero ()**, **stringa ()**, **booleano ()**|[Specifica di funzioni di conversione esplicita nelle query XPath &#40;SQLXML 4,0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/specifying-explicit-conversion-functions-in-xpath-queries-sqlxml-4-0.md)|  
|operatori booleani|AND, OR|[Specifica di operatori booleani in query XPath &#40;SQLXML 4,0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/specifying-boolean-operators-in-xpath-queries-sqlxml-4-0.md)|  
|funzioni booleane|**true ()**, **false ()**, **Not ()**|[Specifica di funzioni booleane in query XPath &#40;SQLXML 4,0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/specifying-boolean-functions-in-xpath-queries-sqlxml-4-0.md)|  
|variabili XPath||[Specifica di variabili XPath in query XPath &#40;SQLXML 4,0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/specifying-xpath-variables-in-xpath-queries-sqlxml-4-0.md)|  
  
## <a name="unsupported-functionality"></a>Funzionalità non supportata  
 Nella tabella seguente vengono mostrate le caratteristiche del linguaggio XPath non implementate in SQLXML 4.0.  
  
|Funzionalità|Elemento|  
|-------------|----------|  
|Assi|**predecessore**, **predecessore-or-self**, **descendant**, **descendant-or-self (//)**, **seguente**, **seguente-elemento di pari livello**, **spazio dei nomi**, **precedente**, **precedente-di pari livello**|  
|Predicati con valori numerici||  
|Operatori aritmetici|mod|  
|Funzioni nodo|**predecessore**, **predecessore-or-self**, **descendant**, **descendant-or-self (//)**, **seguente**, **seguente-elemento di pari livello**, **spazio dei nomi**, **precedente**, **precedente-di pari livello**|  
|Funzioni per i valori stringa|**String ()**, **Concat ()**, **starts-with ()**, **Contains ()**, **substring-before ()**, **substring-after ()**, **substring ()**, **String-length ()**, **Normalize ()**, **translate ()**|  
|funzioni booleane|**lang ()**|  
|Funzioni numeriche|**Sum ()**, **Floor ()**, **Ceiling ()**, **round ()**|  
|Operatore Union|&#124;|  
  
 Quando si specificano query XPath in un modello, si noti il comportamento seguente:  
  
-   XPath può contenere caratteri quali < o & con significati speciali in XML (e il modello è un documento XML). È necessario utilizzare caratteri di escape per questi caratteri utilizzando la codifica XML & o specificare XPath nell'URL.  
  
## <a name="see-also"></a>Vedere anche  
 [Utilizzo di query XPath in SQLXML 4.0](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/using-xpath-queries-in-sqlxml-4-0.md)  
  
  
