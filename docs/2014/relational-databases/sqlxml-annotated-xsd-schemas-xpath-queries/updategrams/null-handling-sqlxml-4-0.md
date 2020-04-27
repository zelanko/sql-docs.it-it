---
title: Gestione dei valori NULL (SQLXML 4,0) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 11f7ca96ca65ae23202b84030140e0eaef945de2
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66014693"
---
# <a name="null-handling-sqlxml-40"></a>Gestione dei valori Null (SQLXML 4.0)
  Nella sintassi XML il valore Null indica un'assenza. Se, ad esempio, il valore di un attributo o di un elemento è NULL, l'attributo o l'elemento è assente dal documento XML. In [!INCLUDE[msCoName](../../../includes/msconame-md.md)] SQLXML l' `updg:nullvalue` attributo consente di specificare null per un valore di elemento o attributo.  
  
 L'updategram seguente, ad esempio, assicura che il valore del **titolo** per un contatto con **ContactID** di 64 sia null e quindi aggiorni il valore del **titolo** a "Mr." per questo contatto.  
  
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
  
 Quando i parametri vengono passati a un updategram, è possibile passare Null come valore del parametro. A tale scopo è necessario specificare l'attributo `nullvalue` nel blocco `<updg:header>`. Per un esempio, vedere [passaggio di parametri agli updategram &#40;SQLXML 4,0&#41;](passing-parameters-to-updategrams-sqlxml-4-0.md).  
  
## <a name="see-also"></a>Vedi anche  
 [Considerazioni sulla sicurezza degli updategram &#40;SQLXML 4,0&#41;](../security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
