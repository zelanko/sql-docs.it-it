---
title: Implementazione di SQLGetDiagRec e SQLGetDiagField | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], SqlGetDiagField
- SQLGetDiagField function [ODBC], and SQLGetDiagRec
- SQLGetDiagRec function [ODBC], and SQLGetDiagField
- diagnostic information [ODBC], SqlGetDiagRec
- retrieving diagnostic information [ODBC]
ms.assetid: 11ba1857-b533-4517-8131-a2a8a0154a0a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ab1f808b005afaa91ed93bf8f8ec7a8385c9c945
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62447285"
---
# <a name="implementing-sqlgetdiagrec-and-sqlgetdiagfield"></a>Implementazione di SQLGetDiagRec e SQLGetDiagField
**SQLGetDiagRec** e **SQLGetDiagField** implementate da Gestione Driver e ogni driver. Gestione Driver ogni driver di gestire i record di diagnostica per ogni ambiente, connessione, istruzione e descrittore handle e liberare i record solo quando un'altra funzione viene chiamata con che handle o l'handle viene liberata.  
  
 Sebbene sia gestione Driver e tutti i driver devono determinare il primo record di stato in base ai calcoli di pertinenza nelle [sequenza di record di stato](../../../odbc/reference/develop-app/sequence-of-status-records.md), gestione Driver determina la sequenza finale di record.  
  
 **SQLGetDiagRec** e **SQLGetDiagField** non registra record di diagnostica su se stesse.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Regole di gestione di diagnostica](../../../odbc/reference/develop-app/diagnostic-handling-rules.md)  
  
-   [Ruolo di Gestione driver](../../../odbc/reference/develop-app/role-of-the-driver-manager.md)  
  
-   [Ruolo del driver](../../../odbc/reference/develop-app/role-of-the-driver.md)
