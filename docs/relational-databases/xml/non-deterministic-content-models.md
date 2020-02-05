---
title: Modelli di contenuto non deterministici | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- non-deterministic content models
- content models [XML in SQL Server]
ms.assetid: 9d4513e7-dd19-4491-b7c7-28bc7c2f8589
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4de53a22bb650098db48619bef26efe543dd9ebd
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "68137429"
---
# <a name="non-deterministic-content-models"></a>modelli di contenuto non deterministici
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Prima di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 1 (SP1), gli elementi XML Schema che contenevano modelli di contenuto non deterministici venivano rifiutati in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 A partire da [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP1, i modelli di contenuto non deterministici vengono accettati se i vincoli di occorrenza sono 0, 1 o senza vincoli.  
  
## <a name="example-non-deterministic-content-model-rejected"></a>Esempio: modello di contenuto non deterministico rifiutato  
 Nello schema dell'esempio viene illustrato il tentativo di creare un elemento XML Schema con un modello di contenuto non deterministico. Il codice ha esito negativo poiché non è possibile determinare se l'elemento `<root>` debba avere una sequenza di due elementi `<a>` oppure se l'elemento `<root>` debba averne due, ognuna con un elemento `<a>` .  
  
```  
CREATE XML SCHEMA COLLECTION MyCollection AS '  
<schema xmlns="http://www.w3.org/2001/XMLSchema">  
    <element name="root">  
        <complexType>  
            <sequence minOccurs="1" maxOccurs="2">  
                <element name="a" type="string" minOccurs="1" maxOccurs="2"/>  
            </sequence>  
        </complexType>  
    </element>  
</schema>  
'  
GO  
```  
  
 È possibile correggere lo schema spostando il vincolo di occorrenza in una posizione univoca, ad esempio, il vincolo può essere spostato nella particella contenente la sequenza:  
  
```  
<sequence minOccurs="1" maxOccurs="4">  
    <element name="a" type="string" minOccurs="1" maxOccurs="1"/>  
</sequence>  
```  
  
 In alternativa, il vincolo può essere spostato sull'elemento contenuto:  
  
```  
<sequence minOccurs="1" maxOccurs="1">  
     <element name="a" type="string" minOccurs="1" maxOccurs="4"/>  
</sequence>  
```  
  
## <a name="example-non-deterministic-content-model-accepted"></a>Esempio: modello di contenuto non deterministico rifiutato  
 Lo schema seguente verrebbe rifiutato nelle versioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] precedenti a [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP1.  
  
```  
CREATE XML SCHEMA COLLECTION MyCollection AS '  
<schema xmlns="http://www.w3.org/2001/XMLSchema">  
    <element name="root">  
        <complexType>  
            <sequence minOccurs="0" maxOccurs="unbounded">  
                <element name="a" type="string" minOccurs="0" maxOccurs="1"/>  
                <element name="b" type="string" minOccurs="1" maxOccurs="unbounded"/>  
            </sequence>  
        </complexType>  
    </element>  
</schema>  
'  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Requisiti e limitazioni per le raccolte di XML Schema nel server](../../relational-databases/xml/requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  
