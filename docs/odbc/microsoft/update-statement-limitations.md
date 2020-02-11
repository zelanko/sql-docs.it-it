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
ms.openlocfilehash: 1cc8cf58d4e4d826dc4b152e395dedbea395a095
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68088197"
---
# <a name="update-statement-limitations"></a>Limitazioni dell'istruzione UPDATE
Affinché il driver Paradox aggiorni una tabella, è necessario che la tabella disponga di un indice univoco (chiave primaria Paradox). Quando si usa il driver Paradox senza implementare il motore di database Borland, non è possibile aggiornare una tabella Paradox.  
  
 Non supportato dal driver di testo.  
  
 Quando si utilizza il driver Microsoft Excel, è possibile aggiornare i valori, ma non è possibile eliminare una riga da una tabella basata su un foglio di calcolo di Microsoft Excel. Di conseguenza, l'istruzione UPDATE non viene considerata ufficialmente supportata dal driver Microsoft Excel. Solo l'istruzione INSERT è considerata supportata.
