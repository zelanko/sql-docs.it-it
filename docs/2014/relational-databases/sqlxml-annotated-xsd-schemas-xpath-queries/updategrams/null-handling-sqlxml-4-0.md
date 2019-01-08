---
title: NULL (SQLXML 4.0) gestisce | Documenti di Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- updg:nullvalue attribute
- updategrams [SQLXML], null values
- nullvalue attribute
- null values [SQLXML]
ms.assetid: 5e11eebb-d94e-4ce6-a6d0-870225706bc1
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 59110e6686307e9555355fb72fefdbf6099bbc69
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52767323"
---
# <a name="null-handling-sqlxml-40"></a>Gestione dei valori Null (SQLXML 4.0)
  Nella sintassi XML il valore Null indica un'assenza. Se, ad esempio, un valore di attributo o di elemento è Null, tale attributo o elemento è assente nel documento XML. In [!INCLUDE[msCoName](../../../includes/msconame-md.md)] SQLXML l'attributo `updg:nullvalue` consente la specifica di un valore Null per un attributo o un elemento.  
  
 Ad esempio, l'updategram seguente verifica che il **Title** valore per un contatto con **ContactID** 64 sia NULL e quindi aggiorna il **titolo** valore di "Mr." per questo contatto.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync updg:nullvalue="IsNULL"  >  
    <updg:before>  
       <Person.Contact ContactID="64" Title="IsNULL" />  
    </updg:before>  
    <updg:after>  
       <Person.Contact ContactID="64" Title="Mr." />  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
 Quando i parametri vengono passati a un updategram, è possibile passare Null come valore del parametro. A tale scopo è necessario specificare l'attributo `nullvalue` nel blocco `<updg:header>`. Per un esempio, vedere [passaggio di parametri agli updategram &#40;SQLXML 4.0&#41;](passing-parameters-to-updategrams-sqlxml-4-0.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Considerazioni sulla sicurezza degli updategram &#40;SQLXML 4.0&#41;](../security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
