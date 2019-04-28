---
title: Proprietà dei membri (MDX) definito dall'utente | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- custom member properties [MDX]
ms.assetid: b64cc581-e784-42c4-bec8-932abd687423
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 97f7a61772b93c78173f3eca8ad38fca1ade671a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62699740"
---
# <a name="user-defined-member-properties-mdx"></a>Proprietà dei membri definite dall'utente (MDX)
  Le proprietà dei membri definite dall'utente possono essere aggiunte a uno specifico livello denominato di una dimensione come relazioni tra attributi. Le proprietà dei membri definite dall'utente non possono essere aggiunte al livello `(All)` di una gerarchia né alla gerarchia stessa.  
  
## <a name="creating-user-defined-member-properties"></a>Creazione delle proprietà dei membri definite dall'utente  
 Le proprietà dei membri definite dall'utente possono essere aggiunte a dimensioni o cubi basati su server tramite l'interfaccia utente o a livello di programmazione:  
  
-   Per aggiungere proprietà dei membri definite dall'utente tramite l'interfaccia utente, usare Progettazione dimensioni in [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]. Per altre informazioni, vedere [Definire relazioni tra attributi](../attribute-relationships-define.md).  
  
-   Per aggiungere proprietà dei membri definite dall'utente a livello di programmazione, è possibile utilizzare AMO (Analysis Manager Objects) o una combinazione di XMLA (XML for Analysis) e ASSL (Analysis Services Scripting Language). Per altre informazioni, vedere [Relazioni tra attributi](../../multidimensional-models-olap-logical-dimension-objects/attribute-relationships.md).  
  
## <a name="retrieving-user-defined-member-properties"></a>Recupero delle proprietà dei membri definite dall'utente  
 È possibile recuperare le proprietà membro definite dall'utente usando il `PROPERTIES` parola chiave o il [proprietà](/sql/mdx/properties-mdx) (funzione).  
  
### <a name="using-the-properties-keyword-to-retrieve-user-defined-member-properties"></a>Utilizzo della parola chiave PROPERTIES per il recupero delle proprietà dei membri definite dall'utente  
 La sintassi da utilizzare per il recupero delle proprietà dei membri definite dall'utente è simile a quella utilizzata per il recupero delle proprietà intrinseche dei membri dei livelli, come illustrato di seguito:  
  
 `DIMENSION PROPERTIES [Dimension.]Level.<Custom_Member_Property>`  
  
 La parola chiave `PROPERTIES` compare dopo l'espressione set che specifica l'asse. Nella query MDX seguente, ad esempio, la parola chiave `PROPERTIES` recupera le proprietà membro definite dall'utente `List Price` e `Dealer Price` e viene visualizzata dopo l'espressione set che identifica i prodotti venduti a gennaio:  
  
```  
SELECT   
   CROSSJOIN([Ship Date].[Calendar].[Calendar Year].Members,   
             [Measures].[Sales Amount]) ON COLUMNS,  
   NON EMPTY Product.Product.MEMBERS  
   DIMENSION PROPERTIES   
              Product.Product.[List Price],  
              Product.Product.[Dealer Price]  ON ROWS  
FROM [Adventure Works]  
WHERE ([Date].[Month of Year].[January])   
```  
  
### <a name="using-the-properties-function-to-retrieve-user-defined-member-properties"></a>Utilizzo della funzione Properties per il recupero delle proprietà dei membri definite dall'utente  
 In alternativa, per accedere alle proprietà personalizzate dei membri è possibile utilizzare la funzione `Properties`. Nella query MDX seguente viene ad esempio utilizzata la parola chiave `WITH` per creare un membro calcolato costituito dalla proprietà `List Price` di un membro:  
  
```  
WITH   
   MEMBER [Measures].[Product List Price] AS  
   [Product].[Product].CurrentMember.Properties("List Price")  
SELECT   
   [Measures].[Product List Price] on COLUMNS,  
   [Product].[Product].MEMBERS  ON Rows  
FROM [Adventure Works]  
```  
  
 Per altre informazioni sulla compilazione di membri calcolati, vedere [Compilazione di membri calcolati in MDX &#40;MDX&#41;](mdx-calculated-members-building-calculated-members.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Utilizzo delle proprietà dei membri &#40;MDX&#41;](mdx-member-properties.md)   
 [Properties &#40;MDX&#41;](/sql/mdx/properties-mdx)  
  
  
