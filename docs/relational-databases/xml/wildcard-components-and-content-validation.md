---
title: Componenti jolly e convalida del contenuto | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- wildcard components [XML]
- content validation [XML]
ms.assetid: ffa7d974-3645-446c-8425-f0b22b6b060a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ba4e15016ca7b6ae3094b575ee87a1c7508b8aac
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "68096959"
---
# <a name="wildcard-components-and-content-validation"></a>Componenti jolly e convalida del contenuto
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  I componenti jolly vengono utilizzati per consentire una maggiore flessibilità riguardo agli elementi che è possibile includere in un modello di contenuto. Tali componenti vengono supportati nel linguaggio XSD nei modi seguenti:  
  
-   Elemento componenti jolly. Sono rappresentati dall'elemento **\<xsd:any>** .  
  
-   Attributo componenti jolly. Sono rappresentati dall'elemento **\<xsd:anyAttribute>** .  
  
 Entrambi gli elementi dei caratteri jolly, **\<xsd:any>** e **\<xsd:anyAttribute>** , supportano l'uso di un attributo **processContents**. Questo attributo consente di specificare un valore che indica il modo in cui le applicazioni XML gestiscono la convalida del contenuto di documenti associato a tali elementi dei caratteri jolly. Valori diversi e relativo effetto:  
  
-   Il valore **strict** specifica che viene eseguita la convalida completa del contenuto.  
  
-   Il valore **skip** specifica che non viene eseguita la convalida del contenuto.  
  
-   Il valore **lax** specifica che viene eseguita solo la convalida di elementi e attributi per i quali sono disponibili definizioni di schemi.  
  
## <a name="lax-validation-and-xsanytype-elements"></a>Elementi della convalida lax e del tipo xs:anyType  
 La specifica di XML Schema utilizza la convalida **lax** per elementi del tipo **anyType** . Poiché [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] non supportava la convalida di tipo lax, per gli elementi di tipo **anyType**veniva applicata la convalida di tipo strict. A partire da [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], la convalida lax è supportata. Il contenuto degli elementi del tipo **anyType** sarà convalidato utilizzando la convalida lax.  
  
 L'esempio seguente illustra la convalida lax. L'elemento schema `e` è del tipo **anyType** . L'esempio crea variabili **xml** tipizzate e illustra la convalida lax dell'elemento di tipo **anyType** .  
  
```  
CREATE XML SCHEMA COLLECTION SC AS '  
<schema xmlns="http://www.w3.org/2001/XMLSchema"   
        targetNamespace="http://ns">  
   <element name="e" type="anyType"/>  
   <element name="a" type="byte"/>  
   <element name="b" type="string"/>  
 </schema>'  
GO  
```  
  
 L'esempio seguente è corretto in quanto la convalida di `<e>` ha esito positivo:  
  
```  
DECLARE @var XML(SC)  
SET @var = '<e xmlns="http://ns"><a>1</a><b>data</b></e>'  
GO  
```  
  
 L'esempio seguente ha esito positivo. L'istanza è accettata, anche se non è definito alcun elemento `<c>` nello schema:  
  
```  
DECLARE @var XML(SC)  
SET @var = '<e xmlns="http://ns"><a>1</a><c>Wrong</c><b>data</b></e>'  
GO  
```  
  
 L'istanza XML nell'esempio seguente è rifiutata, perché la definizione dell'elemento `<a>` non consente un valore della stringa.  
  
```  
DECLARE @var XML(SC)  
SET @var = '<e xmlns="http://ns"><a>Wrong</a><b>data</b></e>'  
SELECT @var  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Requisiti e limitazioni per le raccolte di XML Schema nel server](../../relational-databases/xml/requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  
