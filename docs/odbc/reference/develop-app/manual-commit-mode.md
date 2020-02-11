---
title: Modalità di commit manuale | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68036406"
---
# <a name="manual-commit-mode"></a>Modalità di commit manuale
*In modalità di commit manuale,* le applicazioni devono completare in modo esplicito le transazioni chiamando **SQLEndTran** per eseguirne il commit o eseguire il rollback. Si tratta della modalità di transazione normale per la maggior parte dei database relazionali.  
  
 Non è necessario avviare in modo esplicito le transazioni in ODBC. Una transazione viene invece avviata in modo implicito ogni volta che l'applicazione inizia a funzionare nel database. Se l'origine dati richiede l'avvio esplicito della transazione, il driver deve fornirla ogni volta che l'applicazione esegue un'istruzione che richiede una transazione e non è presente alcuna transazione corrente.
