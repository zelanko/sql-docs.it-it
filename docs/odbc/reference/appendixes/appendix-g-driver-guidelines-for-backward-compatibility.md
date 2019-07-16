---
title: 'Appendice G: Linee guida di driver per la compatibilità con le versioni precedenti | Microsoft Docs'
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2a07e936617100c56f8fa873df1b490e1d61e3f3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67909948"
---
# <a name="appendix-g-driver-guidelines-for-backward-compatibility"></a>Appendice G: Linee guida per la compatibilità con le versioni precedenti dei driver
Questa appendice vengono fornite informazioni per gli sviluppatori di driver lavorando ODBC 3. *x* i driver necessari per il supporto di ODBC 2. *x* applicazioni. Per altre informazioni sulla compatibilità con le versioni precedenti, vedere [garantire la compatibilità e conformità agli standard](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md).  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Cursori rettangolari, cursori scorrevoli e compatibilità con le versioni precedenti per driver ODBC 3.x](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md) -nuove funzionalità sono le funzionalità disponibili in ODBC 3. *x* e non in ODBC 2. *x*. ODBC 3. *x* i driver in genere non sono necessario preoccuparsi della compatibilità con le nuove funzionalità perché l'API ODBC 2. *x* mai usano le applicazioni. L'unica eccezioni sono le funzionalità relative alla **SQLFetch**, **SQLFetchScroll**, **SQLSetPos**, e **SQLExtendedFetch**; per altre informazioni informazioni, vedere più avanti in questa appendice.  
  
-   [Mapping di funzioni deprecate](../../../odbc/reference/appendixes/mapping-deprecated-functions.md) -funzionalità duplicate sono implementati in modo diverso in ODBC 3. *x* e ODBC 2. *x*. ODBC 3. *x* i driver non sono necessario preoccuparsi della compatibilità con le versioni precedenti con funzionalità duplicate perché è sempre mappata gestione Driver ODBC 2. *x* le funzionalità da ODBC 3. *x* funzionalità quando si chiama un'applicazione ODBC 3. *x* driver. Di conseguenza, un database ODBC 3. *x* driver vede solo ODBC 3. *x* funzionalità. Per altre informazioni su tali mapping, vedere più avanti in questa appendice.  
  
-   [Modifiche del comportamento e driver ODBC 3.x](../../../odbc/reference/appendixes/behavioral-changes-and-odbc-3-x-drivers.md) -le modifiche di comportamento sono funzionalità che vengono gestite in modo diverso in ODBC 3. *x* e ODBC 2. *x*. ODBC 3. *x* driver necessario preoccuparsi di modifiche del comportamento e agire in risposta all'attributo SQL_ATTR_ODBC_VERSION ambiente impostata dall'applicazione.
