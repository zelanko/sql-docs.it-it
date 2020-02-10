---
title: Considerazioni sulla sicurezza per XML (SQLXML 4,0) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- NESTED mode
- client-side XML formatting
- FOR XML clause, security
- server-side XML formatting
- AUTO mode
- security [SQLXML], FOR XML
ms.assetid: facba279-df93-475b-ad43-0043dc5bae03
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 34172dcb60e5f2729d8810f697ef975f042f5233
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66010535"
---
# <a name="for-xml-security-considerations-sqlxml-40"></a>Considerazioni sulla sicurezza per FOR XML (SQLXML 4.0)
  La modalità FOR XML AUTO genera una gerarchia XML in cui viene eseguito il mapping dei nomi di elemento ai nomi di tabella e dei nomi di attributo ai nomi di colonna. In questo modo vengono esposte le informazioni sulle colonne e sulle tabelle di database. È possibile nascondere le informazioni del database quando si utilizza la modalità AUTO (formattazione sul lato server) specificando gli alias di colonne e di tabelle nella query. Questi alias vengono restituiti nel documento XML risultante come nomi di elemento e di attributo.  
  
 Nella query seguente ad esempio viene specificata la modalità AUTO; pertanto, la formattazione XML viene eseguita nel server:  
  
```  
SELECT C.FirstName as F,C.LastName as L   
FROM Person.Contact C   
FOR XML AUTO  
```  
  
 Nel documento XML risultante vengono utilizzati gli alias per i nomi di elemento e di attributo:  
  
```  
<?xml version="1.0" encoding="utf-8" ?>   
<root>  
  <C F="Nancy" L="Fuller" />   
  <CE F="Andrew" L="Peacock" />   
  <C F="Janet" L="Leverling" />   
  ...  
</root>  
```  
  
 Quando si utilizza la modalità NESTED (formattazione sul lato client), gli alias vengono restituiti solo per gli attributi nel documento XML risultante. I nomi delle tabelle di base vengono restituiti sempre come nomi di elemento. Ad esempio, nella query seguente viene specificata la modalità NESTED.  
  
```  
SELECT C.FirstName as F,C.LastName as L   
FROM Person.Contact C   
FOR XML AUTO  
```  
  
 Nel documento XML risultante i nomi delle tabelle di base vengono restituiti come nomi di elemento e gli alias di tabella non vengono utilizzati:  
  
```  
<?xml version="1.0" encoding="utf-8" ?>   
<root>  
  <Person.Contact F="Nancy" L="Fuller" />   
  <Person.Contact F="Andrew" L="Peacock" />   
  <Person.Contact F="Janet" L="Leverling" />   
       ...  
</root>  
```  
  
  
