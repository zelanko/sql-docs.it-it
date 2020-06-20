---
title: Funzioni di aggregazione CLR definite dall'utente | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- aggregate functions [CLR integration]
- custom aggregates [CLR integration]
- calculations [CLR integration]
- user-defined functions [CLR integration]
ms.assetid: bad9b7e8-5967-4afa-8dc8-6d840faf9372
author: rothja
ms.author: jroth
ms.openlocfilehash: d1ef5d07fe082d0eeb2c3484d6e99572d8fc80e5
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84954621"
---
# <a name="clr-user-defined-aggregates"></a>Aggregazioni CLR definite dall'utente
  Le funzioni di aggregazione eseguono un calcolo su un set di valori e restituiscono un singolo valore. Tradizionalmente, [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ha supportato solo funzioni di aggregazione predefinite, ad esempio `SUM` o `MAX` , che operano su un set di valori scalari di input e generano un singolo valore di aggregazione da tale set. L'integrazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con il CLR [!INCLUDE[msCoName](../../includes/msconame-md.md)] di .NET Framework consente ora agli sviluppatori di creare funzioni di aggregazione personalizzate in codice gestito e di rendere accessibili queste funzioni a [!INCLUDE[tsql](../../includes/tsql-md.md)] o all'altro codice gestito.  
  
 Nella tabella seguente vengono elencati gli argomenti disponibili in questa sezione.  
  
 [Requisiti per le aggregazioni CLR definite dall'utente](clr-user-defined-aggregates-requirements.md)  
 Viene fornita una panoramica dei requisiti per l'implementazione di funzioni di aggregazione CLR definite dall'utente.  
  
 [Chiamata di funzioni di aggregazione CLR definite dall'utente](clr-user-defined-aggregate-invoking-functions.md)  
 Viene illustrato come richiamare aggregazioni definite dall'utente.  
  
  
