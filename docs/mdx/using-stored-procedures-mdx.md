---
title: Utilizzo delle Stored procedure (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 0d4d455ed7bd804f4c2d4ce036c00f85fd94629f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63251576"
---
# <a name="using-stored-procedures-mdx"></a>Utilizzo di stored procedure (MDX)


  È possibile estendere la funzionalità di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] e delle espressioni MDX scrivendo stored procedure .NET o funzioni .NET definite dall'utente. Per altre informazioni, vedere [programmazione Server ADOMD.NET](https://docs.microsoft.com/bi-reference/adomd/multidimensional-models-adomd-net-server/adomd-net-server-programming)  
  
 Quando si fa riferimento o si chiama una stored procedure, è necessario specificare il nome della funzione seguito da una coppia di parentesi. Nelle parentesi è possibile includere particolari espressioni, dette argomenti, che consentono di passare dati ai parametri. Quando si chiama una funzione è necessario specificare i valori degli argomenti per tutti i parametri, nella stessa sequenza in cui sono definiti i parametri nella funzione definita dall'utente.  
  
 La query di esempio seguente presuppone che si disponga di un assembly denominato SampleAssembly registrato nel server [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]:  
  
```  
SELECT SampleAssembly.RandomSample([Geography].[State-Province].Members, 5) on ROWS,   
[Date].[Calendar].[Calendar Year] on COLUMNS  
FROM [Adventure Works]  
WHERE [Measures].[Reseller Freight Cost]  
```  
  
> [!NOTE]  
>  *Stored procedure* è la terminologia usata in [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] per questi tipi di funzioni. Le versioni precedenti di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] chiamato questi tipi di funzioni come *funzioni definite dall'utente*.  
  
## <a name="types-of-stored-procedures"></a>Tipi di stored procedure  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] supporta sia assembly COM che assembly CLR. È preferibile utilizzare gli assembly CLR, perché per tali assembly sono disponibili funzionalità di sicurezza più avanzate. Se nel server è installato Microsoft Office Excel, saranno disponibili anche le funzioni di Excel.  
  
> [!NOTE]  
>  Gli assembly COM creati con Microsoft Visual Basic, Applications Edition (VBA) vengono registrati automaticamente.  
  
## <a name="see-also"></a>Vedere anche  
 [Le funzioni &#40;sintassi MDX&#41;](../mdx/functions-mdx-syntax.md)  
  
  
