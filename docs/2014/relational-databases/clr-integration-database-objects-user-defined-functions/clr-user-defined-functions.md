---
title: Funzioni CLR definite dall'utente | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- building database objects [CLR integration], user-defined functions
- functions [CLR integration]
- common language runtime [SQL Server], user-defined functions
- database objects [CLR integration], user-defined functions
- user-defined functions [CLR integration]
ms.assetid: 6f7491f1-9a46-4146-ae09-056248634de2
author: rothja
ms.author: jroth
ms.openlocfilehash: ba7a4a983ec0cb36ef0fd79df44491f7f23f7648
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84970771"
---
# <a name="clr-user-defined-functions"></a>Funzioni CLR definite dall'utente
  Le funzioni definite dall'utente sono routine che possono accettare parametri, eseguire calcoli o altre azioni e restituire un risultato. A partire da [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], è possibile scrivere le funzioni definite dall'utente in qualsiasi linguaggio di programmazione [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework, ad esempio [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic .NET o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C#.  
  
 Esistono due tipi di funzioni: scalari, che restituiscono un solo valore, e con valori di tabella, che restituiscono un set di righe.  
  
 Nella tabella seguente vengono elencati gli argomenti disponibili in questa sezione.  
  
 [Funzioni a valori scalari CLR](clr-scalar-valued-functions.md)  
 Vengono descritti i requisiti di implementazione e vengono forniti esempi delle funzioni scalari e con valori di tabella.  
  
 [Funzioni CLR con valori di tabella](clr-table-valued-functions.md)  
 Viene illustrato come implementare e utilizzare funzioni valutate a livello di tabella (TVF) e vengono discusse le differenze tra le funzioni TVF CLR (Common Language Runtime) e [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 [Aggregazioni CLR definite dall'utente](clr-user-defined-aggregates.md)  
 Viene descritto come implementare e utilizzare le aggregazioni definite dall'utente.  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni definite dall'utente](../user-defined-functions/user-defined-functions.md)  
  
  
