---
title: Annotazioni XSD (SQLXML 4.0) | Documenti di Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- annotated XSD schemas, annotations listed
- XSD schemas [SQLXML], annotations
ms.assetid: c62a6785-8d66-40a2-9c5d-80c73d600a3b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1b9e50cc418ef1fa2076b3207d7d3429694f160a
ms.sourcegitcommit: 45a9d7ffc99502c73f08cb937cbe9e89d9412397
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/22/2019
ms.locfileid: "66013551"
---
# <a name="xsd-annotations-sqlxml-40"></a>Annotazioni XSD (SQLXML 4.0)
  Nella tabella seguente sono elencate le annotazioni XSD introdotte in [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], che vengono confrontate con le annotazioni XDR introdotte in [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)].  
  
|Annotazione XSD|Descrizione|Collegamento all'argomento|Annotazione XDR|  
|--------------------|-----------------|----------------|--------------------|  
|`sql:encode`|Quando viene eseguito il mapping a una colonna BLOB di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di un elemento o un attributo XML, è possibile richiedere un URI di riferimento. L'URI può essere utilizzato in seguito per restituire dati BLOB.|[Richiesta di riferimenti URL a dati BLOB utilizzando sql: encode &#40;SQLXML 4.0&#41;](requesting-url-references-to-blob-data-using-sql-encode-sqlxml-4-0.md)|`url-encode`|  
|`sql:guid`|Consente di specificare se utilizzare un valore GUID generato da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o il valore fornito nell'updategram per la colonna.|[Uso delle annotazioni sql:identity e sql:guid](using-the-sql-identity-and-sql-guid-annotations.md)|Non supportato|  
|`sql:hide`|Nasconde l'elemento o l'attributo specificato nello schema nel documento XML risultante.|[Nascondere gli elementi e gli attributi usando sql:hide](hiding-elements-and-attributes-by-using-sql-hide.md)|Non supportato|  
|`sql:identity`|Può essere specificato in qualsiasi nodo mappato a una colonna di database di tipo IDENTITY. Il valore specificato per questa annotazione definisce il modo in cui viene aggiornata la colonna di tipo IDENTITY corrispondente nel database.|[Uso delle annotazioni sql:identity e sql:guid](using-the-sql-identity-and-sql-guid-annotations.md)|Non supportato|  
|`sql:inverse`|Indica all'updategram la logica per invertire l'interpretazione della relazione padre-figlio che è stata specificata tramite  **\<SQL: Relationship >**.|[Specifica l'attributo SQL: inverse in SQL: Relationship &#40;SQLXML 4.0&#41;](specifying-the-sql-inverse-attribute-on-sql-relationship-sqlxml-4-0.md)|Non supportato|  
|`sql:is-constant`|Crea un elemento XML che non viene mappato ad alcuna tabella. L'elemento viene visualizzato nell'output della query.|[Creazione di elementi costanti tramite sql: costante è &#40;SQLXML 4.0&#41;](creating-constant-elements-using-sql-is-constant-sqlxml-4-0.md)|Uguale|  
|`sql:key-fields`|Consente la specifica di colonne che identificano in modo univoco le righe di una tabella.|[Identificazione delle colonne chiave mediante SQL: Key-i campi &#40;SQLXML 4.0&#41;](identifying-key-columns-using-sql-key-fields-sqlxml-4-0.md)|Uguale|  
|`sql:limit-field`<br /><br /> `sql:limit-value`|Consente di limitare i valori restituiti in base a un valore di limitazione.|[Filtrare valori tramite SQL: limit-field e SQL: limit-valore &#40;SQLXML 4.0&#41;](../sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/annotation-interpretation-sql-limit-field-and-sql-limit-value.md)|Uguale|  
|`sql:mapped`|Consente l'esclusione degli elementi dello schema dal risultato.|[Esclusione di elementi dello Schema dal documento XML risultante tramite sql: il mapping &#40;SQLXML 4.0&#41;](excluding-schema-elements-from-the-xml-document-using-sql-mapped.md)|`map-field`|  
|`sql:max-depth`|Consente di specificare la nidificazione nelle relazioni ricorsive indicate nello schema.|[Specifica del livello di nidificazione nelle relazioni ricorsive con sql:max-depth](specifying-depth-in-recursive-relationships-by-using-sql-max-depth.md)|Non supportato|  
|`sql:overflow-field`|Identifica la colonna di database contenente i dati di overflow.|[Recupero di dati non utilizzati mediante SQL: overflow-campo &#40;SQLXML 4.0&#41;](../sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/annotation-interpretation-sql-overflow-field.md)|Uguale|  
|`sql:prefix`|Consente di creare attributi ID, IDREF e IDREFS XML validi. Consente di anteporre una stringa ai valori di ID, IDREF e IDREFS.|[Creazione di ID valido, IDREF e IDREFS tipo attributi usando SQL: prefix &#40;SQLXML 4.0&#41;](creating-valid-id-idref-and-idrefs-type-attributes-using-sql-prefix-sqlxml-4-0.md)|Uguale|  
|`sql:relationship`|Consente di specificare relazioni tra elementi XML. Per stabilire la relazione, vengono utilizzati gli attributi `parent`, `child`, `parent-key` e `child-key`.|[Specifica di relazioni tramite SQL: Relationship &#40;SQLXML 4.0&#41;](specifying-relationships-using-sql-relationship-sqlxml-4-0.md)|I nomi di attributo sono diversi:<br /><br /> `key-relation`<br /><br /> `foreign-relation`<br /><br /> `key`<br /><br /> `foreign-key`|  
|`sql:use-cdata`|Consente di specificare sezioni CDATA da utilizzare per determinati elementi nel documento XML.|[Creazione di sezioni CDATA mediante SQL: use-cdata &#40;SQLXML 4.0&#41;](creating-cdata-sections-using-sql-use-cdata-sqlxml-4-0.md)|Uguale|  
  
> [!NOTE]  
>  L'attributo XSD `targetNamespace` nativo sostituisce l'annotazione `target-namespace` introdotta nello schema di mapping XDR di [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)].  
  
## <a name="see-also"></a>Vedere anche  
 [Specificare una destinazione Namespace usando l'attributo targetNamespace &#40;SQLXML 4.0&#41;](specifying-a-target-namespace-using-the-targetnamespace-attribute-sqlxml-4-0.md)  
  
  
