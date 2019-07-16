---
title: Programma di formattazione XML sul lato server (SQLXML 4.0) | Microsoft Docs
ms.custom: ''
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
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 70771bcb9256b53f4bb8ca459bd7e3836dfcea5c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68005217"
---
# <a name="server-side-xml-formatting-sqlxml-40"></a>Formattazione XML sul lato server (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  In questo argomento sono incluse informazioni sulla formattazione di documenti XML sul lato server dai set di righe generati da query eseguite su un database in Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 In [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] è possibile archiviare e recuperare documenti XML da e verso tabelle di database. Per recuperare un documento XML, utilizzare l'estensione della query FOR XML in una query SELECT.  
  
 Si supponga ad esempio un'applicazione client esegue un comando sul [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] costituito da quanto segue [!INCLUDE[tsql](../../../includes/tsql-md.md)] query:  
  
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
  
 Per altre informazioni sulla clausola FOR XML, vedere [costruzione XML utilizzando FOR XML](../../../relational-databases/xml/for-xml-sql-server.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Architettura della formattazione XML sul lato Client e lato Server &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml/formatting/architecture-of-client-side-and-server-side-xml-formatting-sqlxml-4-0.md)   
 [Formattazione XML sul lato client &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml/formatting/client-side-xml-formatting-sqlxml-4-0.md)   
 [FOR XML &#40;SQL Server&#41;](../../../relational-databases/xml/for-xml-sql-server.md)  
  
  
