---
description: Limitazioni dell'istruzione DELETE
title: Limitazioni dell'istruzione DELETE | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- DELETE statement limitations [ODBC]
- ODBC SQL grammar, DELETE statement limitations
ms.assetid: 084761fe-e65b-4f38-ba4f-69884b2a7700
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5ffb3a6d0ab28fc2b8bc8785df586ac6bbc86aa0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88340897"
---
# <a name="delete-statement-limitations"></a>Limitazioni dell'istruzione DELETE
L'istruzione DELETE non è supportata per Microsoft Excel o driver di testo. Si noti che l'istruzione INSERT è supportata per il driver di testo.  
  
 Il driver dBASE non supporta la compressione di una tabella per rimuovere i valori "eliminati".  
  
 Affinché il driver Paradox elimini una riga da una tabella, è necessario che la tabella disponga di un indice univoco (chiave primaria Paradox).
