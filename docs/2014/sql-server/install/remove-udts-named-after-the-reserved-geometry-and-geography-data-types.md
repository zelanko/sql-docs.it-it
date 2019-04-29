---
title: Rimuovere i tipi definiti dall'utente denominata tipi di dati GEOMETRY e GEOGRAPHY riservati | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- geometry data type [SQL Server], UDTs
- geography data type [SQL Server], UDTs
ms.assetid: a167ce3a-50b4-4e77-a884-adb23b586c72
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f93b179da229793c65db452e4f38bb1f08fbfad1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62855880"
---
# <a name="remove-udts-named-after-the-reserved-geometry-and-geography-data-types"></a>Rimuovere i tipi definiti dall'utente (UDT) denominati in base ai tipi di dati GEOMETRY e GEOGRAPHY riservati
  È stato rilevato un tipo definito dall'utente denominato in base a un termine riservato per i tipi di dati `geometry` o `geography`. I tipi di dati `geometry` e `geography` fanno parte della nuova funzionalità dei dati spaziali.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Descrizione  
 I termini utilizzati per i tipi di dati spaziali non devono essere utilizzati come nomi per Common Language Runtime (CLR) o per tipi di dati definiti dall'utente alias.  
  
## <a name="corrective-action"></a>Azione correttiva  
 Rimuovere il tipo definito dall'utente denominato in base al tipo di dati e ricreare il tipo con un nome non riservato.  
  
## <a name="external-resources"></a>Risorse esterne  
 [Creazione di un tipo definito dall'utente](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types.md)  
  
 [Panoramica dei tipi di dati spaziali](../../relational-databases/spatial/spatial-data-types-overview.md)  
  
  
