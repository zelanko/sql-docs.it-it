---
description: Utilizzo di stored procedure (MDX)
title: Utilizzo di stored procedure (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 2c9bd8f20ffae61656dd30f139ce12665ff57f4e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476973"
---
# <a name="using-stored-procedures-mdx"></a>Utilizzo di stored procedure (MDX)


  È possibile estendere la funzionalità di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] e delle espressioni MDX scrivendo stored procedure .NET o funzioni .NET definite dall'utente. Per ulteriori informazioni, vedere la pagina relativa alla [programmazione del Server ADOMD.NET](https://docs.microsoft.com/analysis-services/adomd/multidimensional-models-adomd-net-server/adomd-net-server-programming)  
  
 Quando si fa riferimento o si chiama una stored procedure, è necessario specificare il nome della funzione seguito da una coppia di parentesi. Nelle parentesi è possibile includere particolari espressioni, dette argomenti, che consentono di passare dati ai parametri. Quando si chiama una funzione è necessario specificare i valori degli argomenti per tutti i parametri, nella stessa sequenza in cui sono definiti i parametri nella funzione definita dall'utente.  
  
 La query di esempio seguente presuppone che si disponga di un assembly denominato SampleAssembly registrato nel server [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]:  
  
```  
SELECT SampleAssembly.RandomSample([Geography].[State-Province].Members, 5) on ROWS,   
[Date].[Calendar].[Calendar Year] on COLUMNS  
FROM [Adventure Works]  
WHERE [Measures].[Reseller Freight Cost]  
```  
  
> [!NOTE]  
>  La *stored procedure* è la terminologia utilizzata in [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] per questi tipi di funzioni. Le versioni precedenti di hanno [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] chiamato questi tipi di funzioni come *funzioni definite dall'utente*.  
  
## <a name="types-of-stored-procedures"></a>Tipi di stored procedure  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] supporta sia assembly COM che assembly CLR. È preferibile utilizzare gli assembly CLR, perché per tali assembly sono disponibili funzionalità di sicurezza più avanzate. Se nel server è installato Microsoft Office Excel, saranno disponibili anche le funzioni di Excel.  
  
> [!NOTE]  
>  Gli assembly COM creati con Microsoft Visual Basic, Applications Edition (VBA) vengono registrati automaticamente.  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni &#40;sintassi MDX&#41;](../mdx/functions-mdx-syntax.md)  
  
  
