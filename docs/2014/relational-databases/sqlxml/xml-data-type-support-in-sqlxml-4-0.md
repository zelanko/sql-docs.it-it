---
title: Supporto del tipo di dati in SQLXML 4.0 XML | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- SQLXML, xml data type support
- xml data type [SQL Server], SQLXML
ms.assetid: 9a6f5ad8-4a8f-4de7-ac17-81d5ccf78459
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 1a0fa49a1dac16ed366c66c72f7d800ccc4aed8e
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52750621"
---
# <a name="xml-data-type-support-in-sqlxml-40"></a>Supporto del tipo di dati xml in SQLXML 4.0
  A partire [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] supporta XML tipizzati con dati di `xml` tipo di dati. In questo argomento viene descritto il modo in cui SQLXML 4.0 riconosce istanze del tipo di dati `xml` e ne implementa il supporto.  
  
## <a name="working-with-xml-data-types"></a>Utilizzo dei tipi di dati xml  
 Per una migliore comprensione dell'utilizzo di tabelle SQL che implementano colonne con tipo di dati `xml`, vengono forniti gli esempi seguenti:  
  
|Attività|Esempio|Argomento|  
|----------|-------------|-----------|  
|Come eseguire il mapping e includere una colonna `xml` in una vista XML|"Mapping di un elemento XML a una colonna con tipo di dati XML"|[Mapping predefinito degli attributi ed elementi XSD a tabelle e colonne &#40;SQLXML 4.0&#41;](../sqlxml-annotated-xsd-schemas-using/default-mapping-of-xsd-elements-and-attributes-to-tables-and-columns-sqlxml-4-0.md)|  
|Come inserire dati in una colonna `xml` con updategram|"Inserimento di dati in una colonna con tipo di dati XML"|[Inserimento di dati mediante Updategram XML &#40;SQLXML 4.0&#41;](../sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/inserting-data-using-xml-updategrams-sqlxml-4-0.md)|  
|Caricamento bulk di dati XML in una colonna `xml`|"Caricamento bulk in colonne con tipo di dati xml"|[Esempi di caricamento Bulk XML &#40;SQLXML 4.0&#41;](../sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/xml-bulk-load-examples-sqlxml-4-0.md)|  
  
## <a name="guidelines-and-limitations"></a>Linee guida e limitazioni  
  
-   **\<XSD: qualsiasi >** non può essere mappato a una colonna che include un `xml` tipo di dati. Il supporto in SQLXML per questo scenario viene fornito tramite l'annotazione `sql:overflow-field`. Una soluzione alternativa consiste nell'eseguire il mapping di un campo con tipo di dati `xml` come elemento di `xsd:anyType`. Questa soluzione alternativa viene illustrata nell'esempio "Mapping di un elemento XML a una colonna con tipo di dati XML" citato nella tabella precedente.  
  
-   Le query XPath nel contenuto di colonne con tipo di dati `xml` non sono supportate.  
  
-   L'utilizzo di una colonna con tipo di dati `xml` in annotazioni in cui la colonna è supportata, ad esempio in `sql:relationship` e `sql:key-fields`, o consentita restituirà errori di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che non verranno intercettati dai componenti di livello intermedio che implementano SQLXML 4.0. Questo problema si verifica in quanto SQLXML non richiede informazioni sul tipo SQL. Questo comportamento è simile al comportamento di SQLXML per altri tipi di dati, ad esempio i tipi BLOB e binary.  
  
-   Il mapping di colonne `xml` è supportato solo per gli schemi XSD. Gli schemi XDR non supportano il mapping di colonne `xml`.  
  
-   SQLXML 4.0 si basa sul supporto dell'analisi XML disponibile in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. È possibile eseguire il mapping di una colonna `xml` come XML tipizzato o XML non tipizzato. In entrambi i casi, SQLXML 4.0 non convalida i dati XML di input.  Se i dati XML di input non sono validi o corretti, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] lo segnala a SQLXML e propaga qualsiasi informazione pertinente sugli errori restituita dal server all'utente.  
  
-   SQLXML 4.0 si basa sul supporto limitato per i DTD disponibili in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consente una definizione DTD interna nei dati di tipo `xml`, che può essere utilizzata per fornire valori predefiniti e sostituire i riferimenti a entità con il relativo contenuto espanso. SQLXML passa i dati XML "come sono", inclusa la definizione DTD interna, al server. È possibile convertire definizioni DTD in documenti XSD (XML Schema) utilizzando strumenti di terze parti e caricare i dati con schemi XSD inline nel database.  
  
-   SQLXML 4.0 non mantiene istruzioni di elaborazione di dichiarazione XML, ad esempio, in base al comportamento di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Al contrario, la dichiarazione XML viene considerata una direttiva al parser XML di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e i relativi attributi (versione, codifica e autonomia) andranno perduti in seguito alla conversione dei dati nel tipo di dati `xml`. I dati XML vengono archiviati internamente come UCS-2. Tutte le altre istruzioni di elaborazione nell'istanza XML vengono mantenute, sono consentite nella colonna `xml` e possono essere supportate in SQLXML.  
  
## <a name="see-also"></a>Vedere anche  
 [Dati XML &#40;SQL Server&#41;](../xml/xml-data-sql-server.md)  
  
  
