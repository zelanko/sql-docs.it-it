---
title: Supporto del tipo di dati in SQLXML 4.0 XML | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- SQLXML, xml data type support
- xml data type [SQL Server], SQLXML
ms.assetid: 9a6f5ad8-4a8f-4de7-ac17-81d5ccf78459
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 902fecbc9400149186789877567c7ef93d8c9dc6
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56034652"
---
# <a name="xml-data-type-support-in-sqlxml-40"></a>Supporto del tipo di dati xml in SQLXML 4.0
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  A partire [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] supporta XML tipizzati con dati di **xml** tipo di dati. Questo argomento vengono fornite informazioni sul modo in cui SQLXML 4.0 riconosce istanze del **xml** tipo di dati e implementa il supporto per loro.  
  
## <a name="working-with-xml-data-types"></a>Utilizzo dei tipi di dati xml  
 Per altre informazioni su come usare tabelle SQL che implementano **xml** colonne di tipo di dati vengono forniti gli esempi seguenti:  
  
|Attività|Esempio|Argomento|  
|----------|-------------|-----------|  
|Come eseguire il mapping e includere un **xml** colonna in una vista XML|"Mapping di un elemento XML a una colonna con tipo di dati XML"|[Mapping predefinito degli attributi ed elementi XSD a tabelle e colonne &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/default-mapping-of-xsd-elements-and-attributes-to-tables-and-columns-sqlxml-4-0.md)|  
|Come inserire dati in un' **xml** colonna con updategram|"Inserimento di dati in una colonna con tipo di dati XML"|[Inserimento di dati mediante Updategram XML &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/inserting-data-using-xml-updategrams-sqlxml-4-0.md)|  
|Il caricamento di dati XML in BULK un' **xml** colonna|"Caricamento bulk in colonne con tipo di dati xml"|[Esempi di caricamento Bulk XML &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/xml-bulk-load-examples-sqlxml-4-0.md)|  
  
## <a name="guidelines-and-limitations"></a>Linee guida e limitazioni  
  
-   **\<XSD: qualsiasi >** non può essere mappato a una colonna che include un' **xml** tipo di dati. Supporto in SQLXML per questo scenario viene fornito tramite il **SQL: overflow-campo** annotazione. Un'altra soluzione alternativa consiste nell'eseguire il mapping di un **xml** campo come elemento di tipo di dati **xsd: anyType**. Questa soluzione alternativa viene illustrata nell'esempio "Mapping di un elemento XML a una colonna con tipo di dati XML" citato nella tabella precedente.  
  
-   Query XPath nel contenuto di **xml** colonne di tipo di dati non è supportato.  
  
-   Usando un **xml** colonna di tipo nelle annotazioni in cui non è supportata (ad esempio **SQL: Relationship** e **SQL: Key-campi**) o consentita restituirà [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] errori che non verranno intercettati dai componenti di livello intermedio implementano SQLXML 4.0. Questo problema si verifica in quanto SQLXML non richiede informazioni sul tipo SQL. Questo comportamento è simile al comportamento di SQLXML per altri tipi di dati, ad esempio i tipi BLOB e binary.  
  
-   Mapping **xml** colonne è supportata solo per gli schemi XSD. Gli schemi XDR non supportano il mapping **xml** colonne.  
  
-   SQLXML 4.0 si basa sul supporto dell'analisi XML disponibile in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Un' **xml** colonna può eseguire il mapping come XML tipizzato o non tipizzato. In entrambi i casi, SQLXML 4.0 non convalida i dati XML di input.  Se i dati XML di input non sono validi o corretti, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] lo segnala a SQLXML e propaga qualsiasi informazione pertinente sugli errori restituita dal server all'utente.  
  
-   SQLXML 4.0 si basa sul supporto limitato per i DTD disponibili in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consente a una definizione DTD interna nei **xml** dati di tipo, che può essere usato per fornire i valori predefiniti e sostituire i riferimenti alle entità con il relativo contenuto espanso. SQLXML passa i dati XML "come sono", inclusa la definizione DTD interna, al server. È possibile convertire definizioni DTD in documenti XSD (XML Schema) utilizzando strumenti di terze parti e caricare i dati con schemi XSD inline nel database.  
  
-   SQLXML 4.0 non mantiene istruzioni di elaborazione di dichiarazione XML, ad esempio, in base al comportamento di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Al contrario, la dichiarazione XML viene trattata come una direttiva per il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] parser XML e i relativi attributi (versione, codifica e autonomi) vengono persi dopo aver convertiti i dati per il **xml** tipo di dati. I dati XML vengono archiviati internamente come UCS-2. Tutte le altre istruzioni di elaborazione nell'istanza XML vengono mantenuti. sono consentite nel **xml** colonna e può essere supportato da SQLXML.  
  
## <a name="see-also"></a>Vedere anche  
 [Dati XML &#40;SQL Server&#41;](../../relational-databases/xml/xml-data-sql-server.md)  
  
  
