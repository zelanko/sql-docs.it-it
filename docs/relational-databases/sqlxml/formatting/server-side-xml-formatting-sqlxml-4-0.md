---
title: Formattazione XML sul lato server (SQLXML)
description: Informazioni sulla formattazione XML sul lato server dei documenti generati dalle query SQLXML 4,0 eseguite su un database Microsoft SQL Server.
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- FOR XML clause, formatting
- server-side XML formatting
ms.assetid: ae9ea068-0857-4505-a3b2-f53d256b644c
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: be657e9fa17be6c6ea2b0441d852f51efa6882be
ms.sourcegitcommit: 5c7634b007f6808c87094174b80376cb20545d5f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84882148"
---
# <a name="server-side-xml-formatting-sqlxml-40"></a>Formattazione XML sul lato server (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  In questo argomento sono incluse informazioni sulla formattazione di documenti XML sul lato server dai set di righe generati da query eseguite su un database in Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 In [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] è possibile archiviare e recuperare documenti XML da e verso tabelle di database. Per recuperare un documento XML, utilizzare l'estensione della query FOR XML in una query SELECT.  
  
 Si supponga, ad esempio, che un'applicazione client esegua un comando su [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] costituito dalla [!INCLUDE[tsql](../../../includes/tsql-md.md)] query seguente:  
  
```  
SELECT FirstName, LastName  
FROM   Person.Contact  
FOR XML AUTO  
```  
  
 Il server esegue la query in due passaggi. Il server esegue innanzitutto l'istruzione SELECT seguente:  
  
```  
SELECT FirstName, LastName  
FROM   Person.Contact  
```  
  
 Il server applica quindi la trasformazione FOR XML al set di righe generato. Il documento XML risultante viene quindi inviato al client come set di righe a una colonna. In questa documentazione questo processo viene definito formattazione XML sul lato server.  
  
 Sul lato server è possibile specificare le modalità seguenti con una clausola FOR XML:  
  
-   RAW  
  
-   AUTO  
  
-   EXPLICIT  
  
 Per ulteriori informazioni sulla clausola FOR XML, vedere [costruzione di codice XML mediante for XML](../../../relational-databases/xml/for-xml-sql-server.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Architettura della formattazione XML sul lato client e sul lato server &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml/formatting/architecture-of-client-side-and-server-side-xml-formatting-sqlxml-4-0.md)   
 [Formattazione XML sul lato client &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml/formatting/client-side-xml-formatting-sqlxml-4-0.md)   
 [FOR XML &#40;SQL Server&#41;](../../../relational-databases/xml/for-xml-sql-server.md)  
  
  
