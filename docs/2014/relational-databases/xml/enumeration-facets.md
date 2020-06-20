---
title: Facet di enumerazione | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- enumeration facets
ms.assetid: dec23a79-ddd6-4701-9721-55a2c435a34d
author: rothja
ms.author: jroth
ms.openlocfilehash: fe41085c78077477a495e9cc136c30857938310a
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85048819"
---
# <a name="enumeration-facets"></a>facet di enumerazione
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] rifiuta XML Schema con tipi che dispongono di facet basati su pattern o di enumerazioni che violano tali facet.  
  
## <a name="example"></a>Esempio  
 Ad esempio, lo schema seguente verrebbe rifiutato in quanto il valore di enumerazione fornito include un valore con lettere sia maiuscole che minuscole e inoltre viola il valore di pattern che limita i valori esclusivamente alle lettere minuscole.  
  
```  
CREATE XML SCHEMA COLLECTION MySampleCollection AS '  
<schema xmlns="http://www.w3.org/2001/XMLSchema" targetNamespace="http://ns" xmlns:ns="http://ns">  
    <simpleType name="MyST">  
       <restriction base="string">  
          <pattern value="[a-z]*"/>  
       </restriction>  
    </simpleType>  
  
    <simpleType name="MyST2">  
       <restriction base="ns:MyST">  
           <enumeration value="mYstring"/>  
       </restriction>  
    </simpleType>  
</schema>'  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Requisiti e limitazioni per le raccolte di XML Schema nel server](requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  
