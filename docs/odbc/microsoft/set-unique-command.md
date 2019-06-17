---
title: SET UNIQUE (comando) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SET UNIQUE command [ODBC]
ms.assetid: 1f69e31e-4599-47cc-ac89-b86fba8703c5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7f58eb771245b9820e27ca4d14c2f69035effa44
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63159319"
---
# <a name="set-unique-command"></a>SET UNIQUE (comando)
Specifica se i record con valori di chiave di indice duplicati vengono mantenuti in un file di indice.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
SET UNIQUE ON | OFF  
```  
  
## <a name="arguments"></a>Argomenti  
 ON  
 Specifica che tutti i record con un valore di chiave di indice duplicati non verranno incluse nel file di indice. Solo il primo record con il valore della chiave dell'indice originale è incluso nel file di indice.  
  
 OFF  
 (Predefinito). Specifica che i record con valori di chiave di indice duplicati verranno incluse nel file di indice.  
  
## <a name="remarks"></a>Note  
 Un file di indice mantiene il SET univoco impostato quando si emette REINDICIZZAZIONE. Per altre informazioni, vedere [indice](../../odbc/microsoft/index-command.md).
