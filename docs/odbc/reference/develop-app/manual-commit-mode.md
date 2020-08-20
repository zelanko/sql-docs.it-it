---
description: Modalità di commit manuale
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
ms.openlocfilehash: cb576166242078707846e005b958143812fd5901
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499835"
---
# <a name="manual-commit-mode"></a>Modalità di commit manuale
*In modalità di commit manuale,* le applicazioni devono completare in modo esplicito le transazioni chiamando **SQLEndTran** per eseguirne il commit o eseguire il rollback. Si tratta della modalità di transazione normale per la maggior parte dei database relazionali.  
  
 Non è necessario avviare in modo esplicito le transazioni in ODBC. Una transazione viene invece avviata in modo implicito ogni volta che l'applicazione inizia a funzionare nel database. Se l'origine dati richiede l'avvio esplicito della transazione, il driver deve fornirla ogni volta che l'applicazione esegue un'istruzione che richiede una transazione e non è presente alcuna transazione corrente.
