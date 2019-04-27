---
title: Limitazioni dell'istruzione UPDATE | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- UPDATE statement limitations [ODBC]
- ODBC SQL grammar, UPDATE statement limitations
ms.assetid: 14700aac-e135-4dc0-9138-4b01224461d5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a6b854cc417898c5576c60ca129c597eae280df4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62633133"
---
# <a name="update-statement-limitations"></a>Limitazioni dell'istruzione UPDATE
Per il driver Paradox aggiornare una tabella, la tabella deve avere un indice univoco (chiave primaria Paradox). Quando si usa il driver Paradox senza implementare il motore di Database Borland, non è possibile aggiornare una tabella Paradox.  
  
 Non è supportato dal driver del testo.  
  
 Quando viene usato il driver di Microsoft Excel, è possibile aggiornare i valori, ma non può essere eliminata una riga da una tabella basata su un foglio di calcolo di Microsoft Excel. Di conseguenza, l'istruzione UPDATE non è considerata supportati ufficialmente dal driver per Microsoft Excel. Solo l'istruzione INSERT è considerato supportato.
