---
title: Utilizzo di annotazioni negli schemi XSD (SQLXML 4,0) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- annotated XSD schemas, about annotated XSD schemas
- annotations [SQLXML]
- relationships [SQLXML]
- relationships [SQLXML], hierarchical relationships
- hierarchical relationships [SQLXML]
- mapping schema [SQLXML], scenarios for using
ms.assetid: 78f318a4-7a36-473b-9852-a4bae6940ce5
author: rothja
ms.author: jroth
ms.openlocfilehash: 5237c5c24b302e0ce1996e03e89b3e01ba6d8f51
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85003007"
---
# <a name="using-annotations-in-xsd-schemas-sqlxml-40"></a>Utilizzo delle annotazioni negli schemi XSD (SQLXML 4.0)
  In [!INCLUDE[msCoName](../../includes/msconame-md.md)] SQLXML 4.0 il linguaggio dello schema XSD supporta le annotazioni in una modalità analoga a quella delle annotazioni introdotte con il linguaggio dello schema XDR (XML-Data Reduced). In XSD sono state introdotte alcune annotazioni aggiuntive che non sono supportate in XDR.  
  
 Queste annotazioni possono essere utilizzate all'interno dello schema XSD per specificare un mapping tra dati XML e dati relazionali, incluso un mapping tra elementi e attributi nello schema XSD e tabelle (viste) e colonne nei database.  
  
 Se non si specificano le annotazioni, viene eseguito il mapping predefinito. Per impostazione predefinita, un elemento XSD con un tipo complesso viene mappato a un nome di tabella (vista) nel database specificato e un elemento o attributo con un tipo semplice viene mappato alla colonna che riporta lo stesso nome dell'elemento o dell'attributo.  
  
 Queste annotazioni possono essere utilizzate anche per specificare le relazioni gerarchiche in XML, rappresentando in questo modo le relazioni nel database, perché uno schema XSD è semplicemente una visualizzazione XML dei dati relazionali.  
  
 In questa sezione vengono descritte le annotazioni che è possibile utilizzare con schemi XSD ed esempi pratici del loro utilizzo.  
  
> [!NOTE]  
>  In tutti gli esempi di questa sezione sono specificate query XPath semplici sullo schema XSD con annotazioni descritto in ogni esempio. Si presuppone che l'utente abbia già acquisito familiarità con il linguaggio XPath.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
 [Annotazioni XSD &#40;SQLXML 4,0&#41;](xsd-annotations-sqlxml-4-0.md)  
 Vengono elencate le annotazioni che è possibile utilizzare con gli schemi XSD, le relative descrizioni e le annotazioni equivalenti per XDR.  
  
 [Mapping predefinito di elementi e attributi XSD a tabelle e colonne &#40;SQLXML 4,0&#41;](default-mapping-of-xsd-elements-and-attributes-to-tables-and-columns-sqlxml-4-0.md)  
 Viene illustrato il mapping predefinito e vengono forniti esempi di attività relative al mapping predefinito.  
  
 [Mapping esplicito di attributi e elementi XSD a tabelle e colonne &#40;SQLXML 4,0&#41;](explicit-mapping-xsd-elements-and-attributes-to-tables-and-columns.md)  
 Viene illustrato il mapping esplicito con le annotazioni `sql:relation` e `sql:field` e vengono forniti esempi.  
  
 [Definizione di relazioni tramite SQL: Relationship &#40;SQLXML 4,0&#41;](specifying-relationships-using-sql-relationship-sqlxml-4-0.md)  
 Viene descritta l'annotazione `sql:relationship` e vengono forniti esempi.  
  
 [Specifica dell'attributo SQL: inverse in SQL: Relationship &#40;SQLXML 4,0&#41;](specifying-the-sql-inverse-attribute-on-sql-relationship-sqlxml-4-0.md)  
 Viene descritta l'annotazione `sql:inverse`.  
  
 [Creazione di elementi costanti tramite SQL: is-constant &#40;SQLXML 4,0&#41;](creating-constant-elements-using-sql-is-constant-sqlxml-4-0.md)  
 Viene descritta l'annotazione `sql:is-constant` e vengono forniti esempi.  
  
 [Esclusione di elementi dello schema dal documento XML risultante tramite SQL: mapping &#40;SQLXML 4,0&#41;](excluding-schema-elements-from-the-xml-document-using-sql-mapped.md)  
 Viene descritta l'annotazione `sql:mapped` e vengono forniti esempi.  
  
 [Filtro di valori tramite SQL: limit-field e SQL: Limit-Value &#40;SQLXML 4,0&#41;](../sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/annotation-interpretation-sql-limit-field-and-sql-limit-value.md)  
 Vengono descritte le annotazioni `sql:limit-field` e `sql:limit-value` e vengono forniti esempi.  
  
 [Identificazione delle colonne chiave mediante SQL: key-fields &#40;SQLXML 4,0&#41;](identifying-key-columns-using-sql-key-fields-sqlxml-4-0.md)  
 Viene descritta l'annotazione `sql:key-fields` e vengono forniti esempi.  
  
 [Specifica di uno spazio dei nomi di destinazione mediante l'attributo targetNamespace &#40;SQLXML 4,0&#41;](specifying-a-target-namespace-using-the-targetnamespace-attribute-sqlxml-4-0.md)  
 Descrive e fornisce esempi dell'attributo **targetNamespace** .  
  
 [Creazione di attributi di tipo ID, IDREF e IDREFS validi con SQL: prefix &#40;SQLXML 4,0&#41;](creating-valid-id-idref-and-idrefs-type-attributes-using-sql-prefix-sqlxml-4-0.md)  
 Viene descritta l'annotazione `sql:prefix` e vengono forniti esempi.  
  
 [Coercizioni dei tipi di dati e l'annotazione sql: DataType &#40;SQLXML 4,0&#41;](data-type-coercions-and-the-sql-datatype-annotation-sqlxml-4-0.md)  
 Viene descritta l'annotazione `sql:datatype` e vengono forniti esempi.  
  
 [Mapping dei tipi di dati XSD ai tipi di dati XPath &#40;SQLXML 4,0&#41;](../sqlxml-annotated-xsd-schemas-xpath-queries/xpath-data-types-sqlxml-4-0.md)  
 Viene fornita una tabella in cui i tipi di dati XSD, XDR e XPath vengono messi a confronto e le relative conversioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vengono elencate.  
  
 [Creazione di sezioni CDATA mediante SQL: Use-CDATA &#40;SQLXML 4,0&#41;](creating-cdata-sections-using-sql-use-cdata-sqlxml-4-0.md)  
 Viene descritta l'annotazione `sql:use-data` e vengono forniti esempi.  
  
 [Richiesta di riferimenti URL a dati BLOB tramite SQL: encode &#40;SQLXML 4,0&#41;](requesting-url-references-to-blob-data-using-sql-encode-sqlxml-4-0.md)  
 Viene descritta l'annotazione `sql:encode` e vengono forniti esempi.  
  
 [Recupero di dati non utilizzati tramite SQL: overflow-field &#40;SQLXML 4,0&#41;](../sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/annotation-interpretation-sql-overflow-field.md)  
 Viene descritta l'annotazione `sql:overflow-field` e vengono forniti esempi.  
  
 [Nascondere gli elementi e gli attributi utilizzando sql:hide](hiding-elements-and-attributes-by-using-sql-hide.md)  
 Viene descritta l'annotazione `sql:hide` e vengono forniti esempi.  
  
 [Utilizzo delle annotazioni sql:identity e sql:guid](using-the-sql-identity-and-sql-guid-annotations.md)  
 Vengono descritte le annotazioni `sql:identity` e `sql:guid` e vengono forniti esempi.  
  
 [Specifica del livello di nidificazione nelle relazioni ricorsive mediante sql:max-depth](specifying-depth-in-recursive-relationships-by-using-sql-max-depth.md)  
 Viene descritta l'annotazione `sql:max-depth` e vengono forniti esempi.  
  
## <a name="see-also"></a>Vedere anche  
 [Considerazioni sulla sicurezza dello schema con annotazioni &#40;SQLXML 4,0&#41;](../sqlxml-annotated-xsd-schemas-xpath-queries/security/annotated-schema-security-considerations-sqlxml-4-0.md)  
  
  
