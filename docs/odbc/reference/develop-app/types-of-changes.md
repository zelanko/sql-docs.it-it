---
title: Tipi di modifiche Documenti Microsoft
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
ms.openlocfilehash: f44adb59aa9b0f25475a76a97fe3670de0228c08
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301606"
---
# <a name="types-of-changes"></a>Tipi di modifiche
In ODBC *3.x* (e in qualsiasi versione di ODBC) vengono apportate tre tipi di modifiche. Ognuno di questi influisce sulla compatibilità con le versioni precedenti in modo diverso e viene gestito in modo diverso. Queste modifiche sono descritte nella tabella seguente.  
  
|Tipo di modifica|Descrizione|  
|--------------------|-----------------|  
|Nuove funzionalità|Si tratta di funzionalità nuove di ODBC *3.x,* ad esempio l'associazione out-of-line o i descrittori. Questi vengono implementati solo quando l'applicazione e il driver, così come Gestione Driver, sono della versione *3.x*, quindi non vi è alcun tentativo di rendere questi retro compatibili.|  
|Funzioni duplicate|Si tratta di funzionalità che esistono in ODBC *2.x* e ODBC *3.x* ma sono implementate in modi diversi in ciascuno di essi. Le funzioni **SQLAllocHandle** e **SQLAllocStmt** sono un esempio. Problemi di compatibilità con le versioni precedenti per queste e altre funzionalità duplicate vengono gestite principalmente dai mapping in Gestione Driver.|  
|Modifiche funzionali|Si tratta di funzionalità che vengono gestite in modo diverso in ODBC *2.x* e ODBC *3.x*. Un **#define** datetime è un esempio. Queste funzionalità vengono gestite dal driver ODBC *3.x* in base a un'impostazione dell'attributo di ambiente. Per ulteriori informazioni, vedere [Modifiche comportamentali.](../../../odbc/reference/develop-app/behavioral-changes.md)|
