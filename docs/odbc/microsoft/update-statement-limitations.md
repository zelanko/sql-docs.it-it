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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8ddf19c0b672901b2e778833f8bf624996d4ced3
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307622"
---
# <a name="update-statement-limitations"></a>Limitazioni dell'istruzione UPDATE
Affinché il driver Paradox aggiorni una tabella, è necessario che la tabella disponga di un indice univoco (chiave primaria Paradox). Quando si usa il driver Paradox senza implementare il motore di database Borland, non è possibile aggiornare una tabella Paradox.  
  
 Non supportato dal driver di testo.  
  
 Quando si utilizza il driver Microsoft Excel, è possibile aggiornare i valori, ma non è possibile eliminare una riga da una tabella basata su un foglio di calcolo di Microsoft Excel. Di conseguenza, l'istruzione UPDATE non viene considerata ufficialmente supportata dal driver Microsoft Excel. Solo l'istruzione INSERT è considerata supportata.
