---
title: Driver sottochiave default | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- default subkey [ODBC]
- registry entries for components [ODBC], default subkey
- subkeys [ODBC], default subkey
- drivers subkey [ODBC]
ms.assetid: 9e58b24f-ebfc-4286-a272-0843b4d6f2d5
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e82644d3bddab5d4f6fde6f7103bd9731872bab9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68094192"
---
# <a name="default-driver-subkey"></a>Sottochiave Default del driver
La sottochiave predefinito contiene un singolo valore che descrive il driver utilizzato dall'origine dati predefinito. Nella tabella seguente viene illustrato il formato di questo valore.  
  
|Nome|Tipo di dati|Data|  
|----------|---------------|----------|  
|**Driver**|REG_SZ|*default-driver-description*|  
  
 Il *predefinito-driver-description* nome è identico al nome del valore della sottochiave ODBC driver che descrive il driver.  
  
 Ad esempio, se l'origine dati predefinita Usa il driver SQL Server, il valore della sottochiave predefinito potrebbe essere:  
  
```  
Driver : REG_SZ : SQL Server  
```  
  
> [!NOTE]  
>  Il driver predefinita contenuto nella sottochiave predefinito può fare riferimento a un DSN dell'utente predefinito o un DSN di sistema predefinito. Se un DSN dell'utente predefinito sia il sistema DSN creato, il driver predefinito dipende dal DSN creato per ultimo, in modo che non sia una voce valida per il DSN creato prima.
