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
ms.openlocfilehash: a4b602d5ff4a94d2888395e6a62f03553fb50f98
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68216370"
---
# <a name="implementing-sqlgetdiagrec-and-sqlgetdiagfield"></a>Implementazione di SQLGetDiagRec e SQLGetDiagField
**SQLGetDiagRec** e **SQLGetDiagField** vengono implementati da Gestione driver e da ogni driver. Gestione driver e ogni driver conservano i record di diagnostica per ogni handle di ambiente, connessione, istruzione e descrittore e li liberano solo quando un'altra funzione viene chiamata con tale handle oppure l'handle viene liberato.  
  
 Anche se Gestione driver e ogni driver devono determinare il primo record di stato in base alle classificazioni in [sequenza dei record di stato](../../../odbc/reference/develop-app/sequence-of-status-records.md), gestione driver determina la sequenza finale di record.  
  
 **SQLGetDiagRec** e **SQLGetDiagField** non pubblicano i record di diagnostica.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Regole di gestione di diagnostica](../../../odbc/reference/develop-app/diagnostic-handling-rules.md)  
  
-   [Ruolo di Gestione driver](../../../odbc/reference/develop-app/role-of-the-driver-manager.md)  
  
-   [Ruolo del driver](../../../odbc/reference/develop-app/role-of-the-driver.md)
