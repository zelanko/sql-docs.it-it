---
description: SET UNIQUE (comando)
title: IMPOSTA comando univoco | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b8fa4ca11ed5beae08bfcbeb8b5a55d6c2969785
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88412457"
---
# <a name="set-unique-command"></a>SET UNIQUE (comando)
Specifica se i record con valori di chiave di indice duplicati vengono mantenuti in un file di indice.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
SET UNIQUE ON | OFF  
```  
  
## <a name="arguments"></a>Argomenti  
 ON  
 Specifica che i record con un valore di chiave di indice duplicato non verranno inclusi nel file di indice. Nel file di indice è incluso solo il primo record con il valore di chiave di indice originale.  
  
 OFF  
 (Impostazione predefinita). Specifica che i record con valori di chiave di indice duplicati siano inclusi nel file di indice.  
  
## <a name="remarks"></a>Osservazioni  
 Un file di indice mantiene l'impostazione UNIVOCa impostata quando si rilascia REINDEX. Per ulteriori informazioni, vedere [index](../../odbc/microsoft/index-command.md).
