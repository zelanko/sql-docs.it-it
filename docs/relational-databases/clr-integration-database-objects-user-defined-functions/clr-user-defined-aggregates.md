---
title: Funzioni di aggregazione CLR definite dall'utente | Microsoft Docs
description: SQL Server integrazione con CLR consente di creare funzioni di aggregazione personalizzate nel codice gestito, che eseguono un calcolo su un set di valori e restituiscono un valore.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
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
ms.openlocfilehash: 6775e9f4bda98f970fd5cdb666fb0bfdb8c1ac10
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85727867"
---
# <a name="clr-user-defined-aggregates"></a>Aggregazioni CLR definite dall'utente
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Le funzioni di aggregazione eseguono un calcolo su un set di valori e restituiscono un singolo valore. Tradizionalmente, [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ha supportato solo funzioni di aggregazione predefinite, ad esempio **Sum** o **Max**, che operano su un set di valori scalari di input e generano un singolo valore di aggregazione da tale set. L'integrazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con il CLR [!INCLUDE[msCoName](../../includes/msconame-md.md)] di .NET Framework consente ora agli sviluppatori di creare funzioni di aggregazione personalizzate in codice gestito e di rendere accessibili queste funzioni a [!INCLUDE[tsql](../../includes/tsql-md.md)] o all'altro codice gestito.  
  
 Nella tabella seguente vengono elencati gli argomenti disponibili in questa sezione.  
  
 [Requisiti per le aggregazioni CLR definite dall'utente](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-aggregates-requirements.md)  
 Viene fornita una panoramica dei requisiti per l'implementazione di funzioni di aggregazione CLR definite dall'utente.  
  
 [Chiamata di funzioni di aggregazione CLR definite dall'utente](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-aggregate-invoking-functions.md)  
 Viene illustrato come richiamare aggregazioni definite dall'utente.  
  
  
