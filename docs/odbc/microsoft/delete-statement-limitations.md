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
ms.openlocfilehash: eb2587f733f5042436144f7865627fee576e3d9c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68096315"
---
# <a name="delete-statement-limitations"></a>Limitazioni dell'istruzione DELETE
L'istruzione DELETE non è supportata per Microsoft Excel o driver di testo. Si noti che l'istruzione INSERT è supportata per il driver di testo.  
  
 Il driver dBASE non supporta la compressione di una tabella per rimuovere i valori "eliminati".  
  
 Affinché il driver Paradox elimini una riga da una tabella, è necessario che la tabella disponga di un indice univoco (chiave primaria Paradox).
