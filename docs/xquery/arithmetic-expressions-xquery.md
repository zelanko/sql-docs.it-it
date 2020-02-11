---
title: Espressioni aritmetiche (XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- expressions [XQuery], arithmetic
- arithmetic expressions
ms.assetid: 90d675bf-56da-459a-9771-8cd13920a9fc
author: rothja
ms.author: jroth
ms.openlocfilehash: ccbeda01726a3473f8e955676c3ebd62a93fd630
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67985732"
---
# <a name="arithmetic-expressions-xquery"></a>Espressioni aritmetiche (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Sono supportati tutti gli operatori aritmetici, ad eccezione di **Idiv**. Negli esempi seguenti viene illustrato l'utilizzo di base degli operatori aritmetici:  
  
```  
DECLARE @x xml  
SET @x=''  
SELECT @x.query('2 div 2')  
SELECT @x.query('2 * 2')  
```  
  
 Poiché **Idiv** non è supportato, una soluzione consiste nell'usare il costruttore **xs: Integer ()** :  
  
```  
DECLARE @x xml  
SET @x=''  
-- Following will not work  
-- SELECT @x.query('2 idiv 2')  
-- Workaround   
SELECT @x.query('xs:integer(2 div 3)')  
```  
  
 Il tipo risultante da un operatore aritmetico dipende dai tipi dei valori di input. Se gli operandi sono di tipo diverso, all'occorrenza verrà eseguito il cast di uno o entrambi gli operandi a un tipo di base primitivo comune, in base alla gerarchia dei tipi. Per informazioni sulla gerarchia dei tipi, vedere [regole di cast del tipo in XQuery](../xquery/type-casting-rules-in-xquery.md).  
  
 È possibile che i tipi numeric vengano promossi se ai due operandi sono associati tipi di base numerici diversi. Ad esempio, se si aggiunge un **xs: Decimal** a **xs: Double** , il valore decimale verrà prima modificato in un valore Double. Viene quindi eseguita l'addizione, il cui risultato sarà un valore double.  
  
 Viene eseguito il cast dei valori atomici non tipizzati al tipo di base numerico dell'altro operando o a **xs: Double** se anche l'altro operando non è tipizzato.  
  
## <a name="implementation-limitations"></a>Limitazioni di implementazione  
 Limitazioni:  
  
-   Gli argomenti per gli operatori aritmetici devono essere di tipo numerico o **untypedAtomic**.  
  
-   Le operazioni sui valori **xs: integer** generano un valore di tipo **xs: Decimal** anziché **xs: integer**.  
  
  
