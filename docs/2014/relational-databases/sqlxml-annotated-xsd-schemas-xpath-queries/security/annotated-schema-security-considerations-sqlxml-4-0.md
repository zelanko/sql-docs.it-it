---
title: Considerazioni sulla sicurezza dello schema con annotazioni (SQLXML 4,0) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- mapping schema [SQLXML], security
- annotated XDR schemas, security
- XDR schemas [SQLXML], security
- annotations [SQLXML]
- annotated XSD schemas, security
- SQLXML, annotated XSD schemas
- SQLXML, annotated XDR schemas
- security [SQLXML], annotated schemas
- XSD schemas [SQLXML], security
ms.assetid: 7d7e44dc-b6d3-4e0f-95c7-8f99930c94f2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 635c5c433f583ecad9f8dda1e35e4c981742212e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66010584"
---
# <a name="annotated-schema-security-considerations-sqlxml-40"></a>Considerazioni relative alla sicurezza degli schemi con annotazioni (SQLXML 4.0)
  Di seguito sono riportate alcune linee guida relative alla sicurezza quando si utilizzano gli schemi con annotazioni.  
  
-   Evitare di utilizzare il mapping predefinito negli schemi di mapping. Il mapping predefinito, infatti, espone le informazioni del database (nomi di tabella e di colonna) nel documento XML risultante in quanto, per impostazione predefinita, i nomi di elemento vengono mappati ai nomi di tabella e i nomi di attributo vengono mappati ai nomi di colonna. Pertanto, qualsiasi utente che visualizza il documento XML può accedere anche alle informazioni su tabelle e colonne nel database, ponendo un problema di sicurezza potenziale. Per evitare questo rischio, specificare nomi di elementi e di attributi arbitrari nello schema e utilizzare le annotazioni per mapparli esplicitamente alle tabelle e alle colonne. Per ulteriori informazioni sull'utilizzo del mapping predefinito durante la creazione di schemi XSD, vedere [mapping predefinito di elementi e attributi XSD a tabelle e colonne &#40;SQLXML 4,0&#41;](../../sqlxml-annotated-xsd-schemas-using/default-mapping-of-xsd-elements-and-attributes-to-tables-and-columns-sqlxml-4-0.md).  
  
-   Il mapping esplicito specificato mediante le annotazioni espone le informazioni del database, ad esempio i nomi di tabelle e colonne. È opportuno dunque non rendere pubblici pubblicamente questi schemi.  
  
-   L'esecuzione di determinate query, ad esempio quelle specificate su uno schema di mapping con ricorsione utilizzando l'annotazione `max-depth` impostata su un valore più elevato, può richiedere tempi più lunghi. È possibile specificare facoltativamente un limite di timeout impostando la proprietà timeout comando (in secondi). Ad esempio:  
  
    ```  
    cn.Open "Provider=SQLOLEDB;Server=localhost;Database=tempdb;Integrated Security=SSPI;Command Properties='Command Time Out=50';"  
    ```  
  
## <a name="see-also"></a>Vedi anche  
 [Schemi XSD con annotazioni in SQLXML 4.0](../../sqlxml/annotated-xsd-schemas/annotated-xsd-schemas-in-sqlxml-4-0.md)  
  
  
