---
title: Considerazioni sulla sicurezza dello Schema (SQLXML 4.0) annotati | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
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
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 6a71852dbd4f25e2055544727fd981718ef524b2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68027010"
---
# <a name="annotated-schema-security-considerations-sqlxml-40"></a>Considerazioni relative alla sicurezza degli schemi con annotazioni (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Di seguito sono riportate alcune linee guida relative alla sicurezza quando si utilizzano gli schemi con annotazioni.  
  
-   Evitare di utilizzare il mapping predefinito negli schemi di mapping. Il mapping predefinito, infatti, espone le informazioni del database (nomi di tabella e di colonna) nel documento XML risultante in quanto, per impostazione predefinita, i nomi di elemento vengono mappati ai nomi di tabella e i nomi di attributo vengono mappati ai nomi di colonna. Pertanto, qualsiasi utente che visualizza il documento XML può accedere anche alle informazioni su tabelle e colonne nel database, ponendo un problema di sicurezza potenziale. Per evitare questo rischio, specificare nomi di elementi e di attributi arbitrari nello schema e utilizzare le annotazioni per mapparli esplicitamente alle tabelle e alle colonne. Per altre informazioni sull'uso di mapping predefinito quando si creano schemi XSD, vedere [predefinito Mapping di elementi e attributi XSD a tabelle e colonne &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-using/default-mapping-of-xsd-elements-and-attributes-to-tables-and-columns-sqlxml-4-0.md).  
  
-   Il mapping esplicito specificato mediante le annotazioni espone le informazioni del database, ad esempio i nomi di tabelle e colonne. È opportuno dunque non rendere pubblici pubblicamente questi schemi.  
  
-   Alcune query, ad esempio quelle specificate sullo schema di mapping con ricorsione (specificato mediante **max-depth** annotazione impostato su un valore più alto) può richiedere più tempo per l'esecuzione. È facoltativamente possibile specificare un limite di timeout impostando la proprietà di timeout del comando (in secondi). Ad esempio:  
  
    ```  
    cn.Open "Provider=SQLOLEDB;Server=localhost;Database=tempdb;Integrated Security=SSPI;Command Properties='Command Time Out=50';"  
    ```  
  
## <a name="see-also"></a>Vedere anche  
 [Schemi XSD con annotazioni in SQLXML 4.0](../../../relational-databases/sqlxml/annotated-xsd-schemas/annotated-xsd-schemas-in-sqlxml-4-0.md)  
  
  
