---
title: Gestione dei valori NULL (SQLXML)
description: "Informazioni sul modo in cui è possibile specificare gli attributi o gli elementi NULL in un updategram SQLXML 4,0 usando l'attributo attributo updg: NullValue."
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
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
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: b3fac9c5de10981dbb8afff517a106135ccca82f
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97484823"
---
# <a name="null-handling-sqlxml-40"></a>Gestione dei valori Null (SQLXML 4.0)
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
  Nella sintassi XML il valore Null indica un'assenza. Se, ad esempio, il valore di un attributo o di un elemento è NULL, l'attributo o l'elemento è assente dal documento XML. In [!INCLUDE[msCoName](../../../includes/msconame-md.md)] SQLXML, l'attributo **attributo updg: NullValue** consente di specificare null per un valore di elemento o attributo.  
  
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
  
 Quando i parametri vengono passati a un updategram, è possibile passare Null come valore del parametro. Questa operazione viene eseguita specificando l'attributo **NullValue** nel **\<updg:header>** blocco. Per un esempio, vedere [passaggio di parametri agli updategram &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/passing-parameters-to-updategrams-sqlxml-4-0.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Considerazioni sulla sicurezza degli updategram &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
