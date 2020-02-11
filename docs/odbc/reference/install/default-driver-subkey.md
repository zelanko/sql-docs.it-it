---
title: Sottochiave driver predefinita | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68094192"
---
# <a name="default-driver-subkey"></a>Sottochiave Default del driver
La sottochiave predefinita contiene un solo valore che descrive il driver utilizzato dall'origine dati predefinita. Il formato di questo valore è illustrato nella tabella seguente.  
  
|Nome|Tipo di dati|data|  
|----------|---------------|----------|  
|**Driver**|REG_SZ|*default-driver-Description*|  
  
 Il nome *default-driver-Description* corrisponde al nome del valore nella sottochiave ODBC drivers che descrive il driver.  
  
 Se, ad esempio, l'origine dati predefinita usa il driver SQL Server, il valore nella sottochiave predefinita potrebbe essere:  
  
```  
Driver : REG_SZ : SQL Server  
```  
  
> [!NOTE]  
>  Il driver predefinito contenuto nella sottochiave predefinita può fare riferimento a un DSN utente predefinito o a un DSN di sistema predefinito. Se sono stati creati sia un DSN utente predefinito che un DSN di sistema predefinito, il driver predefinito è determinato dal DSN creato per ultimo, quindi potrebbe non essere una voce valida per il DSN creato per primo.
