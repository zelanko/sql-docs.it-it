---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5f43dbf75754a16b3163bbb8e268400f34d372b4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68087812"
---
# <a name="types-of-changes"></a>Tipi di modifiche
Tre tipi di modifiche vengono apportati in ODBC *3.x* (e qualsiasi versione di ODBC). Ognuno di questi riguarda la compatibilità con le versioni precedenti in modo diverso e viene gestita in modo diverso. Queste modifiche sono descritte nella tabella seguente.  
  
|Tipo di modifica|Descrizione|  
|--------------------|-----------------|  
|Nuove funzionalità|Si tratta di funzioni che hanno familiarità con ODBC *3.x*, ad esempio descrittori o associazione out-of-line. Questi sono implementati solo quando l'applicazione e driver, nonché gestione Driver, sono della versione *3.x*, pertanto non viene eseguito alcun tentativo di rendere questi compatibile con le versioni precedenti.|  
|Funzionalità duplicate|Si tratta di funzionalità che esistono in ODBC *2.x* e ODBC *3.x* ma vengono implementati in modi diversi in ognuno. Le funzioni **SQLAllocHandle** e **SQLAllocStmt** sono un esempio. I problemi di compatibilità con le versioni precedenti per queste e altre funzionalità duplicate vengono principalmente gestiti dai mapping di gestione Driver.|  
|Modifiche del comportamento|Si tratta di funzioni che vengono gestiti in modo diverso in ODBC *2.x* e ODBC *3.x*. Un valore datetime **#define** è riportato un esempio. Queste funzionalità vengono gestite da ODBC *3.x* driver basato su un'impostazione dell'attributo di ambiente. (Vedere [modifiche del comportamento](../../../odbc/reference/develop-app/behavioral-changes.md) per altre informazioni.)|
