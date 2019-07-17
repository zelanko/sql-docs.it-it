---
title: Istruzione REFRESH CUBE (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 957609573c206b7c3492789c369d0fb2be2398a3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68038157"
---
# <a name="mdx-data-definition---refresh-cube"></a>Definizione dei dati MDX - REFRESH CUBE


  Aggiorna la cache del client per un cubo.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
REFRESH CUBECube_Name   
```  
  
## <a name="arguments"></a>Argomenti  
 *Cube_Name*  
 Espressione stringa valida che specifica il nome di un cubo.  
  
## <a name="remarks"></a>Note  
 Per le applicazioni client connesse a un'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], questa istruzione determina la memoria nella cache dell'applicazione client deve essere sincronizzato con il server. Nonostante il rilevamento e l'aggiornamento vengano in genere eseguiti in modo automatico, l'intervallo di tempo prima che ciò si verifichi dipende dalle impostazioni della stringa di connessione client. L'istruzione REFRESH CUBE determina l'aggiornamento immediato dei dati.  
  
 Per le applicazioni client connesse a un cubo locale, con l'istruzione REFRESH CUBE il file del cubo locale viene ricompilato.  
  
> [!IMPORTANT]  
>  I set denominati archiviati nel server non vengono aggiornati.  
  
## <a name="see-also"></a>Vedere anche  
 [Istruzioni di definizione dei dati MDX &#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
