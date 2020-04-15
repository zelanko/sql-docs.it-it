---
title: 'Appendice G: Linee guida per i driver per la compatibilità con le versioni precedenti Documenti Microsoft'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC drivers [ODBC], backward compatibility
- backward compatibility [ODBC], drivers
- compatibility [ODBC], drivers
ms.assetid: 911cd335-f2c0-4d03-9739-1078308a678a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1055f94cb54bba9262f210e5df5f028029aebf5b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81292401"
---
# <a name="appendix-g-driver-guidelines-for-backward-compatibility"></a>Appendice G: Indicazioni per la compatibilità con le versioni precedenti dei driver
In questa appendice vengono fornite informazioni per gli autori di driver che lavorano su ODBC 3. *x* driver che devono supportare ODBC 2. *applicazioni x.* Per ulteriori informazioni sulla compatibilità con le versioni precedenti, vedere [Compatibilità con](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md)le versioni precedenti e conformità agli standard .  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Blocca cursori, cursori scorrevoli e compatibilità con](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md) le versioni precedenti per i driver ODBC 3.x: le nuove funzionalità sono funzionalità esistenti in ODBC 3. *x* e non in ODBC 2. *x*. ODBC 3. *x* driver in genere non devono preoccuparsi di compatibilità con le versioni precedenti con le nuove funzionalità, perché ODBC 2. *x* le applicazioni non le usano mai. Le uniche eccezioni sono le funzionalità correlate a **SQLFetch**, **SQLFetchScroll**, **SQLSetPos**e **SQLExtendedFetch**; Per ulteriori informazioni, vedere , più avanti in questa appendice.  
  
-   [Mapping di funzioni deprecate:](../../../odbc/reference/appendixes/mapping-deprecated-functions.md) le funzionalità duplicate sono funzionalità implementate in modo diverso in ODBC 3. *x* e ODBC 2. *x*. ODBC 3. *x* i driver non devono preoccuparsi della compatibilità con le funzionalità duplicate perché Gestione Driver esegue sempre il mapping ODBC 2. *x* a ODBC 3. *x* quando si chiama un ODBC 3. *driver x.* Pertanto, un ODBC 3. *x* driver vede solo ODBC 3. *x* caratteristiche. Per ulteriori informazioni su questi mapping, vedere , più avanti in questa appendice.  
  
-   [Modifiche comportamentali e Driver ODBC 3.x:](../../../odbc/reference/appendixes/behavioral-changes-and-odbc-3-x-drivers.md) le modifiche di comportamento sono funzionalità gestite in modo diverso in ODBC 3. *x* e ODBC 2. *x*. ODBC 3. *x* i driver devono preoccuparsi delle modifiche di comportamento e agire in risposta all'SQL_ATTR_ODBC_VERSIONattributo di ambiente impostato dall'applicazione.
