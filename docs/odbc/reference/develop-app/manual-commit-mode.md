---
title: Modalità di Commit manuale | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- rolling back transactions [ODBC]
- manual-commit mode [ODBC]
- transactions [ODBC], commit modes
- committing transactions [ODBC]
- commit modes [ODBC]
- transactions [ODBC], rolling back
ms.assetid: 9c4b3931-e48b-4960-89a2-5697537e9f51
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7189a0586ba4f62091d5eb209a56931627bc6f7f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68036406"
---
# <a name="manual-commit-mode"></a>Modalità di commit manuale
*In modalità di commit manuale* applicazioni devono completare in modo esplicito le transazioni chiamando **SQLEndTran** per eseguirne il commit o il rollback. Si tratta della modalità di transazione normale per la maggior parte dei database relazionali.  
  
 Le transazioni in ODBC non sono necessario essere avviato in modo esplicito. Al contrario, viene avviata una transazione in modo implicito ogni volta che viene avviata l'applicazione opera nel database. Se l'origine dati è necessario avviare le transazioni esplicite, il driver necessario specificare ogni volta che l'applicazione esegue un'istruzione che richiedono una transazione e Nessuna transazione corrente.
