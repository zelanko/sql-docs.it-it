---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 98bd56051c724186d7308eff669263d29b82ecd5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63198165"
---
# <a name="delete-statement-limitations"></a>Limitazioni dell'istruzione DELETE
L'istruzione DELETE non è supportata per il driver di Microsoft Excel o di testo. Si noti che l'istruzione INSERT è supportata per il driver di testo.  
  
 Il driver dBASE non supporta la creazione di una tabella per rimuovere i valori "eliminato".  
  
 Per il driver Paradox eliminare una riga da una tabella, la tabella deve avere un indice univoco (chiave primaria Paradox).
