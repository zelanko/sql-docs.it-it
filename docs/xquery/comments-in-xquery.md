---
title: Commenti in XQuery | Microsoft Docs
description: Informazioni sulla sintassi e sui delimitatori per l'aggiunta di commenti a una query XQuery.
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- comments [XQuery]
- XQuery, comments
ms.assetid: 4d977268-de9d-4bf0-b310-b63f6a0fb0db
author: rothja
ms.author: jroth
ms.openlocfilehash: 67f2ad02eb9486508840f0b731b1d6e705d94f7a
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85726750"
---
# <a name="comments-in-xquery"></a>Commenti in query XQuery
[!INCLUDE [SQL Server Azure SQL Database ](../includes/applies-to-version/sqlserver.md)]

  È possibile aggiungere commenti in una query XQuery. Per aggiungere stringhe di commento, utilizzare i delimitatori "`(:`" e "`:)`". Ad esempio:  
  
```  
declare @x xml  
set @x=''  
SELECT @x.query('  
(: simple query to construct an element :)  
<ProductModel ProductModelID="10" />  
')  
```  
  
 Di seguito è riportato un altro esempio in cui viene specificata una query su una colonna di istruzioni del tipo **XML** :  
  
```  
SELECT Instructions.query('  
(: declare prefix and namespace binding in the prolog. :)  
     declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
  (: Following expression retrieves the <Location> element children of the <root> element. :)  
  /AWMI:root/AWMI:Location  
') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
  
