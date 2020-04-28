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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2a00ff373e374d0940b3e7259eeb01e26b620cae
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81287875"
---
# <a name="manual-commit-mode"></a>Modalità di commit manuale
*In modalità di commit manuale,* le applicazioni devono completare in modo esplicito le transazioni chiamando **SQLEndTran** per eseguirne il commit o eseguire il rollback. Si tratta della modalità di transazione normale per la maggior parte dei database relazionali.  
  
 Non è necessario avviare in modo esplicito le transazioni in ODBC. Una transazione viene invece avviata in modo implicito ogni volta che l'applicazione inizia a funzionare nel database. Se l'origine dati richiede l'avvio esplicito della transazione, il driver deve fornirla ogni volta che l'applicazione esegue un'istruzione che richiede una transazione e non è presente alcuna transazione corrente.
