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
ms.openlocfilehash: 29598ed97cba8be04a0c08727cffc40e663becba
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68063609"
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
