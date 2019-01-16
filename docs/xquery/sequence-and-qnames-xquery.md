---
title: Sequenza e QName (XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- sequence [XQuery]
- XQuery, sequence
- QName [XQuery]
- predefined namespaces [XML in SQL Server]
ms.assetid: 3593ac26-dd78-4bf0-bb87-64fbcac5f026
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 0e7c73e33a1f19acb2158ced848c220b2b7af447
ms.sourcegitcommit: bfa10c54e871700de285d7f819095d51ef70d997
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/14/2019
ms.locfileid: "54254156"
---
# <a name="sequence-and-qnames-xquery"></a>Sequenza e QName (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  In questo argomento vengono descritti i concetti fondamentali di XQuery seguenti:  
  
-   Sequenza  
  
-   QName e spazi dei nomi predefiniti  
  
## <a name="sequence"></a>Sequenza  
 In XQuery, il risultato di un'espressione è composto da un elenco di nodi XML e da istanze di tipi atomici XSD. Una singola voce di una sequenza viene definita come un elemento, che può essere:  
  
-   Un nodo, ad esempio un nodo elemento, attributo, di testo, di istruzione di elaborazione, di commento o di documento.  
  
-   Un valore atomico, ad esempio un'istanza di un tipo XSD semplice.  
  
 Ad esempio, la query seguente crea una sequenza di due nodi elemento:  
  
```  
SELECT Instructions.query('  
     <step1> Step 1 description goes here</step1>,  
     <step2> Step 2 description goes here </step2>  
') AS Result  
FROM Production.ProductModel  
WHERE ProductModelID=7;  
  
```  
  
 Questo è il risultato:  
  
```  
<step1> Step 1 description goes here </step1>  
<step2> Step 2 description goes here </step2>   
```  
  
 Nella query precedente, la virgola (`,`) alla fine della sintassi `<step1>` è il costruttore della sequenza ed è obbligatorio. Gli spazi vuoti nei risultati vengono aggiunti solo a scopo illustrativo e sono inseriti in tutti i risultati degli esempi di questa documentazione.  
  
 Di seguito sono riportate informazioni aggiuntive sulle sequenze che è consigliabile conoscere:  
  
-   Se una query restituisce una sequenza che contiene un'altra sequenza, quest'ultima viene convertita in formato flat nel contenitore Sequenza. Ad esempio, la sequenza ((1,2, (3,4,5)),6) viene convertita in formato flat nel modello di dati come (1, 2, 3, 4, 5, 6).  
  
    ```  
    DECLARE @x xml;  
    SET @x = '';  
    SELECT @x.query('(1,2, (3,4,5)),6');  
    ```  
  
-   Una sequenza vuota non contiene alcun elemento ed è rappresentata come "()".  
  
-   Una sequenza con un solo elemento può essere considerata come un valore atomico e viceversa, ovvero (1) = 1.  
  
 In questa implementazione, la sequenza deve essere omogenea, ovvero deve essere una sequenza di valori atomici o di nodi. Ad esempio, le sequenze seguenti sono valide:  
  
```  
DECLARE @x xml;  
SET @x = '';  
-- Expression returns a sequence of 1 text node (singleton).  
SELECT @x.query('1');  
-- Expression returns a sequence of 2 text nodes  
SELECT @x.query('"abc", "xyz"');  
-- Expression returns a sequence of one atomic value. data() returns  
-- typed value of the node.  
SELECT @x.query('data(1)');  
-- Expression returns a sequence of one element node.   
-- In the expression XML construction is used to construct an element.  
SELECT @x.query('<x> {1+2} </x>');  
```  
  
 La query seguente restituisce un errore perché le sequenze eterogenee non sono supportate.  
  
```  
SELECT @x.query('<x>11</x>, 22');  
```  
  
## <a name="qname"></a>QName  
 Ogni identificatore di una query XQuery è un QName, che è composto da un prefisso dello spazio dei nomi e da un nome locale. In questa implementazione, i nomi delle variabili in XQuery sono rappresentati da QName e non possono avere un prefisso.  
  
 Si consideri l'esempio seguente in cui viene specificata una query su una non tipizzati **xml** variabile:  
  
```  
DECLARE @x xml;  
SET @x = '<Root><a>111</a></Root>';  
SELECT @x.query('/Root/a');  
```  
  
 Nell'espressione (`/Root/a`), `Root` e `a` sono QName.  
  
 Nell'esempio seguente viene specificata una query su un oggetto tipizzato **xml** colonna. La query esegue l'iterazione su tutti \<passaggio > elementi nel primo percorso area di produzione.  
  
```  
SELECT Instructions.query('  
   declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
for $Step in /AWMI:root/AWMI:Location[1]/AWMI:step  
      return  
           string($Step)   
') AS Result  
FROM Production.ProductModel  
WHERE ProductModelID=7;  
```  
  
 Nell'espressione della query, si noti quanto segue:  
  
-   `AWMI root`, `AWMI:Location`, `AWMI:step`e `$Step` sono QName. `AWMI` è un prefisso e `root`, `Location` e `Step` sono nomi locali.  
  
-   La variabile `$step` è un QName e non ha un prefisso.  
  
 Gli spazi dei nomi seguenti vengono utilizzati per impostazione predefinita con il supporto XQuery in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
|Prefisso|URI|  
|------------|---------|  
|xs|http://www.w3.org/2001/XMLSchema|  
|xsi|http://www.w3.org/2001/XMLSchema-instance|  
|xdt|http://www.w3.org/2004/07/xpath-datatypes|  
|fn|http://www.w3.org/2004/07/xpath-functions|  
|(nessun prefisso)|`urn:schemas-microsoft-com:xml-sql`|  
|sqltypes|https://schemas.microsoft.com/sqlserver/2004/sqltypes|  
|xml|`http://www.w3.org/XML/1998/namespace`|  
|(nessun prefisso)|`https://schemas.microsoft.com/sqlserver/2004/SOAP`|  
  
 Ogni database creato è il **sys** raccolta di XML schema. Questi schemi sono riservati e pertanto è possibile accedervi da qualsiasi altra raccolta di XML Schema creata dall'utente.  
  
> [!NOTE]  
>  Questa implementazione non supporta il `local` prefisso come descritto nella specifica XQuery in http://www.w3.org/2004/07/xquery-local-functions.  
  
## <a name="see-also"></a>Vedere anche  
 [Nozioni fondamentali su XQuery](../xquery/xquery-basics.md)  
  
  
