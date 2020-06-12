---
title: Supporto del tipo di dati xml in SQLXML 4.0
description: Informazioni su come SQLXML 4,0 riconosce le istanze del tipo di dati XML e implementa il supporto per tale tipo di dati.
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
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: afaee239422b557b53117441f36c79d1180802db
ms.sourcegitcommit: 6593b3b6365283bb76c31102743cdccc175622fe
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/02/2020
ms.locfileid: "84306100"
---
# <a name="xml-data-type-support-in-sqlxml-40"></a>Supporto del tipo di dati xml in SQLXML 4.0
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  A partire da [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] , [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] supporta i dati tipizzati XML utilizzando il tipo di dati **XML** . In questo argomento vengono fornite informazioni sul modo in cui SQLXML 4,0 riconosce le istanze del tipo di dati **XML** e ne implementa il supporto.  
  
## <a name="working-with-xml-data-types"></a>Utilizzo dei tipi di dati xml  
 Per ulteriori informazioni sull'utilizzo delle tabelle SQL che implementano colonne con tipo di dati **XML** , sono disponibili gli esempi seguenti:  
  
|Attività|Esempio|Argomento|  
|----------|-------------|-----------|  
|Come eseguire il mapping e includere una colonna **XML** in una visualizzazione XML|"Mapping di un elemento XML a una colonna con tipo di dati XML"|[Mapping predefinito di elementi e attributi XSD a tabelle e colonne &#40;SQLXML 4,0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/default-mapping-of-xsd-elements-and-attributes-to-tables-and-columns-sqlxml-4-0.md)|  
|Come inserire dati in una colonna **XML** con updategram|"Inserimento di dati in una colonna con tipo di dati XML"|[Inserimento di dati mediante updategram XML &#40;SQLXML 4,0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/inserting-data-using-xml-updategrams-sqlxml-4-0.md)|  
|Caricamento bulk di dati XML in una colonna **XML**|"Caricamento bulk in colonne con tipo di dati xml"|[Esempi di caricamento bulk XML &#40;SQLXML 4,0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/xml-bulk-load-examples-sqlxml-4-0.md)|  
  
## <a name="guidelines-and-limitations"></a>Linee guida e limitazioni  
  
-   **\<xsd:any>** non è possibile eseguire il mapping a una colonna che include un tipo di dati **XML** . Il supporto in SQLXML per questo scenario viene fornito tramite l'annotazione **SQL: overflow-field** . Un'altra soluzione alternativa consiste nel eseguire il mapping di un campo con tipo di dati **XML** come elemento di **xsd: anyType**. Questa soluzione alternativa viene illustrata nell'esempio "Mapping di un elemento XML a una colonna con tipo di dati XML" citato nella tabella precedente.  
  
-   La query XPath nel contenuto delle colonne con tipo di dati **XML** non è supportata.  
  
-   Se si utilizza una colonna con tipo di dati **XML** nelle annotazioni in cui non è supportata (ad esempio, **SQL: Relationship** e **SQL: key-fields**) o consentita, verranno generati [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] errori che non verranno intercettati dai componenti di livello intermedio che implementano SQLXML 4,0. Questo problema si verifica in quanto SQLXML non richiede informazioni sul tipo SQL. Questo comportamento è simile al comportamento di SQLXML per altri tipi di dati, ad esempio i tipi BLOB e binary.  
  
-   Il mapping di colonne **XML** è supportato solo per gli schemi XSD. Gli schemi XDR non supportano il mapping di colonne **XML** .  
  
-   SQLXML 4.0 si basa sul supporto dell'analisi XML disponibile in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. È possibile eseguire il mapping di una colonna **XML** come XML tipizzato o XML non tipizzato. In entrambi i casi, SQLXML 4.0 non convalida i dati XML di input.  Se i dati XML di input non sono validi o corretti, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] lo segnala a SQLXML e propaga qualsiasi informazione pertinente sugli errori restituita dal server all'utente.  
  
-   SQLXML 4.0 si basa sul supporto limitato per i DTD disponibili in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]consente una DTD interna nei dati del tipo di dati **XML** , che può essere utilizzata per fornire valori predefiniti e sostituire i riferimenti alle entità con il relativo contenuto espanso. SQLXML passa i dati XML "come sono", inclusa la definizione DTD interna, al server. È possibile convertire definizioni DTD in documenti XSD (XML Schema) utilizzando strumenti di terze parti e caricare i dati con schemi XSD inline nel database.  
  
-   SQLXML 4,0 non mantiene le istruzioni di elaborazione della dichiarazione XML (ad esempio,) in base al comportamento di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Al contrario, la dichiarazione XML viene considerata come una direttiva per il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] parser XML e i relativi attributi (versione, codifica e autonoma) vengono persi dopo la conversione dei dati nel tipo di dati **XML** . I dati XML vengono archiviati internamente come UCS-2. Tutte le altre istruzioni di elaborazione nell'istanza XML vengono mantenute. sono consentiti nella colonna **XML** e possono essere supportati da SQLXML.  
  
## <a name="see-also"></a>Vedere anche  
 [Dati XML &#40;SQL Server&#41;](../../relational-databases/xml/xml-data-sql-server.md)  
  
  
