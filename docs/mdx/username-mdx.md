---
title: Nome utente (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: f1ebb5dc504b799575b2ccf9e47368e4e6511dac
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68097269"
---
# <a name="username-mdx"></a>UserName (MDX)


  Restituisce il nome utente e di dominio della connessione corrente.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
UserName [ ( ) ]  
```  
  
## <a name="remarks"></a>Osservazioni  
 Il valore restituito è costituito da una stringa con il formato seguente:  
  
 *domain-name\user-name*  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene restituito il nome dell'utente che esegue la query.  
  
```  
WITH MEMBER Measures.x AS UserName  
SELECT Measures.x ON COLUMNS  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;&#41;MDX](../mdx/mdx-function-reference-mdx.md)  
  
  
