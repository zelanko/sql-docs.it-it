---
description: Limitazioni dell'istruzione UPDATE
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
ms.openlocfilehash: b7c1ea2e5e9d887005084cdb5454dcf9b5e8fa24
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471400"
---
# <a name="update-statement-limitations"></a>Limitazioni dell'istruzione UPDATE
Affinché il driver Paradox aggiorni una tabella, è necessario che la tabella disponga di un indice univoco (chiave primaria Paradox). Quando si usa il driver Paradox senza implementare il motore di database Borland, non è possibile aggiornare una tabella Paradox.  
  
 Non supportato dal driver di testo.  
  
 Quando si utilizza il driver Microsoft Excel, è possibile aggiornare i valori, ma non è possibile eliminare una riga da una tabella basata su un foglio di calcolo di Microsoft Excel. Di conseguenza, l'istruzione UPDATE non viene considerata ufficialmente supportata dal driver Microsoft Excel. Solo l'istruzione INSERT è considerata supportata.
