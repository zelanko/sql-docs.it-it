---
title: Considerazioni sulla sicurezza dello Schema (SQLXML 4.0) annotati | Microsoft Docs
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
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 6bebdc1f62e95af43ccedf71087a817cff8e502e
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52750013"
---
# <a name="annotated-schema-security-considerations-sqlxml-40"></a>Considerazioni relative alla sicurezza degli schemi con annotazioni (SQLXML 4.0)
  Di seguito sono riportate alcune linee guida relative alla sicurezza quando si utilizzano gli schemi con annotazioni.  
  
-   Evitare di utilizzare il mapping predefinito negli schemi di mapping. Il mapping predefinito, infatti, espone le informazioni del database (nomi di tabella e di colonna) nel documento XML risultante in quanto, per impostazione predefinita, i nomi di elemento vengono mappati ai nomi di tabella e i nomi di attributo vengono mappati ai nomi di colonna. Pertanto, qualsiasi utente che visualizza il documento XML può accedere anche alle informazioni su tabelle e colonne nel database, ponendo un problema di sicurezza potenziale. Per evitare questo rischio, specificare nomi di elementi e di attributi arbitrari nello schema e utilizzare le annotazioni per mapparli esplicitamente alle tabelle e alle colonne. Per altre informazioni sull'uso di mapping predefinito quando si creano schemi XSD, vedere [predefinito Mapping di elementi e attributi XSD a tabelle e colonne &#40;SQLXML 4.0&#41;](../../sqlxml-annotated-xsd-schemas-using/default-mapping-of-xsd-elements-and-attributes-to-tables-and-columns-sqlxml-4-0.md).  
  
-   Il mapping esplicito specificato mediante le annotazioni espone le informazioni del database, ad esempio i nomi di tabelle e colonne. È opportuno dunque non rendere pubblici pubblicamente questi schemi.  
  
-   L'esecuzione di determinate query, ad esempio quelle specificate su uno schema di mapping con ricorsione utilizzando l'annotazione `max-depth` impostata su un valore più elevato, può richiedere tempi più lunghi. È facoltativamente possibile specificare un limite di timeout impostando la proprietà di timeout del comando (in secondi). Ad esempio:  
  
    ```  
    cn.Open "Provider=SQLOLEDB;Server=localhost;Database=tempdb;Integrated Security=SSPI;Command Properties='Command Time Out=50';"  
    ```  
  
## <a name="see-also"></a>Vedere anche  
 [Schemi XSD con annotazioni in SQLXML 4.0](../../sqlxml/annotated-xsd-schemas/annotated-xsd-schemas-in-sqlxml-4-0.md)  
  
  
