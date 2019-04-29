---
title: Rimuovere i tipi definiti dall'utente&#39;s denominato dopo i tipi di dati data e ora riservati | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- time data type [SQL Server], UDTs
- date data type [SQL Server], UDTs
ms.assetid: 48f109af-b1d1-4f03-a7e3-8a0b05ed94e8
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5471788d3e730c9694ea6394b7e3d1fc659eda96
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62855253"
---
# <a name="remove-udt39s-named-after-the-reserved-date-and-time-data-types"></a>Rimuovere i tipi definiti dall'utente&#39;s nominate a tipi di dati riservati data e ora
  È stato rilevato un tipo definito dall'utente denominato in base a un termine riservato per i tipi di dati `date` o `time`.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Descrizione  
 Non è consigliabile utilizzare i termini utilizzati per i tipi di dati come nomi per Common Language Runtime (CLR) o per tipi di dati definiti dall'utente alias.  
  
## <a name="corrective-action"></a>Azione correttiva  
 Rimuovere il tipo definito dall'utente denominato in base al tipo di dati e ricreare il tipo con un nome non riservato.  
  
  
