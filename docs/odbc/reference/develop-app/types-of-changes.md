---
description: Tipi di modifiche
title: Tipi di modifiche | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- compatibility [ODBC], types of changes
- backward compatibility [ODBC], types of changes
ms.assetid: 6a7db81a-20aa-4915-aed8-429711a36f49
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 46866c49a36711a8072895deb816a9d9110f5035
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476305"
---
# <a name="types-of-changes"></a>Tipi di modifiche
In ODBC *3. x* e in qualsiasi versione di ODBC vengono apportate tre tipi di modifiche. Ognuna di queste influiscono sulla compatibilità con le versioni precedenti e viene gestita in modo diverso. Queste modifiche sono descritte nella tabella seguente.  
  
|Tipo di modifica|Descrizione|  
|--------------------|-----------------|  
|Nuove funzionalità|Si tratta di funzionalità nuove di ODBC *3. x*, ad esempio l'associazione out-of-line o i descrittori. Queste sono implementate solo quando l'applicazione e il driver, nonché la gestione driver, sono della versione *3. x*, quindi non è possibile apportare queste compatibilità con le versioni precedenti.|  
|Funzionalità duplicate|Si tratta di funzionalità esistenti in ODBC *2. x* e ODBC *3. x* , ma sono implementate in modi diversi in ciascuno di essi. Le funzioni **SQLAllocHandle** e **SQLAllocStmt** sono un esempio. I problemi di compatibilità con le versioni precedenti per queste e altre funzionalità duplicate vengono principalmente gestiti dai mapping in Gestione driver.|  
|Modifiche funzionali|Si tratta di funzionalità gestite in modo diverso in ODBC *2. x* e ODBC *3. x*. Un **#define** DateTime è un esempio. Queste funzionalità vengono gestite dal driver ODBC *3. x* in base a un'impostazione dell'attributo Environment. Per ulteriori informazioni, vedere [modifiche del comportamento](../../../odbc/reference/develop-app/behavioral-changes.md) .|
