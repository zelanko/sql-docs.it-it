---
title: Formattazione XML sul lato server (SQLXML 4,0) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- FOR XML clause, formatting
- server-side XML formatting
ms.assetid: ae9ea068-0857-4505-a3b2-f53d256b644c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: af44d854ba28e8e8ac3b1a4572bf9b222f20299b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66012207"
---
# <a name="server-side-xml-formatting-sqlxml-40"></a>Formattazione XML sul lato server (SQLXML 4.0)
  In questo argomento sono incluse informazioni sulla formattazione di documenti XML sul lato server dai set di righe generati da query eseguite su un database in Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 In [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] è possibile archiviare e recuperare documenti XML da e verso tabelle di database. Per recuperare un documento XML, utilizzare l'estensione della query FOR XML in una query SELECT.  
  
 Si supponga, ad esempio, che un'applicazione client esegua [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] un comando su costituito [!INCLUDE[tsql](../../../includes/tsql-md.md)] dalla query seguente:  
  
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
  
 Per ulteriori informazioni sulla clausola FOR XML, vedere [costruzione di codice XML mediante for XML](../../xml/for-xml-sql-server.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Architettura della formattazione XML sul lato client e sul lato server &#40;SQLXML 4,0&#41;](architecture-of-client-side-and-server-side-xml-formatting-sqlxml-4-0.md)   
 [Formattazione XML sul lato client &#40;SQLXML 4,0&#41;](client-side-xml-formatting-sqlxml-4-0.md)   
 [FOR XML &#40;SQL Server&#41;](../../xml/for-xml-sql-server.md)  
  
  
