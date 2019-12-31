---
title: Annotazioni XSD (SQLXML)
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- annotated XSD schemas, annotations listed
- XSD schemas [SQLXML], annotations
ms.assetid: c62a6785-8d66-40a2-9c5d-80c73d600a3b
author: MightyPen
ms.author: genemi
ms.reviewer: ''
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: acd1dc15531f2e4830993eed1404db4d7205feef
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/19/2019
ms.locfileid: "75246803"
---
# <a name="xsd-annotations-sqlxml-40"></a>Annotazioni XSD (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Nella tabella seguente sono elencate le annotazioni XSD introdotte in [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], che vengono confrontate con le annotazioni XDR introdotte in [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)].  
  
|Annotazione XSD|Description|Collegamento all'argomento|Annotazione XDR|  
|--------------------|-----------------|----------------|--------------------|  
|**sql:encode**|Quando viene eseguito il mapping a una colonna BLOB di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di un elemento o un attributo XML, è possibile richiedere un URI di riferimento. L'URI può essere utilizzato in seguito per restituire dati BLOB.|[Richiesta di riferimenti URL a dati BLOB tramite SQL: encode &#40;SQLXML 4,0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/requesting-url-references-to-blob-data-using-sql-encode-sqlxml-4-0.md)|**codifica URL**|  
|**SQL: GUID**|Consente di specificare se utilizzare un valore GUID generato da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o il valore fornito nell'updategram per la colonna.|[Utilizzo delle annotazioni sql:identity e sql:guid](../../relational-databases/sqlxml-annotated-xsd-schemas-using/using-the-sql-identity-and-sql-guid-annotations.md)|Non supportate|  
|**sql:hide**|Nasconde l'elemento o l'attributo specificato nello schema nel documento XML risultante.|[Nascondere gli elementi e gli attributi utilizzando sql:hide](../../relational-databases/sqlxml-annotated-xsd-schemas-using/hiding-elements-and-attributes-by-using-sql-hide.md)|Non supportate|  
|**sql:identity**|Può essere specificato in qualsiasi nodo mappato a una colonna di database di tipo IDENTITY. Il valore specificato per questa annotazione definisce il modo in cui viene aggiornata la colonna di tipo IDENTITY corrispondente nel database.|[Utilizzo delle annotazioni sql:identity e sql:guid](../../relational-databases/sqlxml-annotated-xsd-schemas-using/using-the-sql-identity-and-sql-guid-annotations.md)|Non supportate|  
|**sql:inverse**|Indica alla logica dell'updategram di invertire l'interpretazione della relazione padre-figlio specificata tramite ** \<SQL: Relationship>**.|[Specifica dell'attributo SQL: inverse in SQL: Relationship &#40;SQLXML 4,0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/specifying-the-sql-inverse-attribute-on-sql-relationship-sqlxml-4-0.md)|Non supportate|  
|**sql:is-constant**|Crea un elemento XML che non viene mappato ad alcuna tabella. L'elemento viene visualizzato nell'output della query.|[Creazione di elementi costanti tramite SQL: is-constant &#40;SQLXML 4,0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/creating-constant-elements-using-sql-is-constant-sqlxml-4-0.md)|Uguale|  
|**sql:key-fields**|Consente la specifica di colonne che identificano in modo univoco le righe di una tabella.|[Identificazione delle colonne chiave mediante SQL: key-fields &#40;SQLXML 4,0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/identifying-key-columns-using-sql-key-fields-sqlxml-4-0.md)|Uguale|  
|**sql:limit-field**<br /><br /> **sql:limit-value**|Consente di limitare i valori restituiti in base a un valore di limitazione.|[Filtro di valori tramite SQL: limit-field e SQL: Limit-Value &#40;SQLXML 4,0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/filtering-values-using-sql-limit-field-and-sql-limit-value-sqlxml-4-0.md)|Uguale|  
|**sql:mapped**|Consente l'esclusione degli elementi dello schema dal risultato.|[Esclusione di elementi dello schema dal documento XML risultante tramite SQL: mapping &#40;SQLXML 4,0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/excluding-schema-elements-from-the-xml-document-using-sql-mapped.md)|**Mappa-Campo**|  
|**sql:max-depth**|Consente di specificare la nidificazione nelle relazioni ricorsive indicate nello schema.|[Specifica del livello di nidificazione nelle relazioni ricorsive mediante sql:max-depth](../../relational-databases/sqlxml-annotated-xsd-schemas-using/specifying-depth-in-recursive-relationships-by-using-sql-max-depth.md)|Non supportate|  
|**sql:overflow-field**|Identifica la colonna di database contenente i dati di overflow.|[Recupero di dati non utilizzati tramite SQL: overflow-field &#40;SQLXML 4,0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/retrieving-unconsumed-data-using-the-sql-overflow-field-sqlxml-4-0.md)|Uguale|  
|**sql:prefix**|Consente di creare attributi ID, IDREF e IDREFS XML validi. Consente di anteporre una stringa ai valori di ID, IDREF e IDREFS.|[Creazione di attributi di tipo ID, IDREF e IDREFS validi con SQL: prefix &#40;SQLXML 4,0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/creating-valid-id-idref-and-idrefs-type-attributes-using-sql-prefix-sqlxml-4-0.md)|Uguale|  
|**sql:relationship**|Consente di specificare relazioni tra elementi XML. Per stabilire la relazione vengono utilizzati gli attributi **padre**, **figlio**, **chiave primaria**e **chiave figlio** .|[Definizione di relazioni tramite SQL: Relationship &#40;SQLXML 4,0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/specifying-relationships-using-sql-relationship-sqlxml-4-0.md)|I nomi di attributo sono diversi:<br /><br /> **chiave-relazione**<br /><br /> **relazione esterna**<br /><br /> **chiave**<br /><br /> **chiave esterna**|  
|**sql:use-cdata**|Consente di specificare sezioni CDATA da utilizzare per determinati elementi nel documento XML.|[Creazione di sezioni CDATA mediante SQL: Use-CDATA &#40;SQLXML 4,0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/creating-cdata-sections-using-sql-use-cdata-sqlxml-4-0.md)|Uguale|  
  
> [!NOTE]  
>  L'attributo **targetNamespace** nativo XSD sostituisce l'annotazione **dello spazio dei nomi** di destinazione [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] introdotta nello schema di mapping XDR.  
  
## <a name="see-also"></a>Vedere anche  
 [Specifica di uno spazio dei nomi di destinazione mediante l'attributo targetNamespace &#40;SQLXML 4,0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/specifying-a-target-namespace-using-the-targetnamespace-attribute-sqlxml-4-0.md)  
  
  
