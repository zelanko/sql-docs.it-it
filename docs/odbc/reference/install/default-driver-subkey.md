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
manager: craigg
ms.openlocfilehash: d78101fd564e18467e6833f480cec2409dc2c44b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63198312"
---
# <a name="default-driver-subkey"></a>Sottochiave Default del driver
La sottochiave predefinito contiene un singolo valore che descrive il driver utilizzato dall'origine dati predefinito. Nella tabella seguente viene illustrato il formato di questo valore.  
  
|nome|Tipo di dati|Dati|  
|----------|---------------|----------|  
|**Driver**|REG_SZ|*default-driver-description*|  
  
 Il *predefinito-driver-description* nome è identico al nome del valore della sottochiave ODBC driver che descrive il driver.  
  
 Ad esempio, se l'origine dati predefinita Usa il driver SQL Server, il valore della sottochiave predefinito potrebbe essere:  
  
```  
Driver : REG_SZ : SQL Server  
```  
  
> [!NOTE]  
>  Il driver predefinita contenuto nella sottochiave predefinito può fare riferimento a un DSN dell'utente predefinito o un DSN di sistema predefinito. Se un DSN dell'utente predefinito sia il sistema DSN creato, il driver predefinito dipende dal DSN creato per ultimo, in modo che non sia una voce valida per il DSN creato prima.
