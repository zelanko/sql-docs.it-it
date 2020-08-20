---
description: Sottochiave Default del driver
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d78cc54253d002c54510fdc47f46f10de9281b65
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494554"
---
# <a name="default-driver-subkey"></a>Sottochiave Default del driver
La sottochiave predefinita contiene un solo valore che descrive il driver utilizzato dall'origine dati predefinita. Il formato di questo valore è illustrato nella tabella seguente.  
  
|Nome|Tipo di dati|Data|  
|----------|---------------|----------|  
|**Driver**|REG_SZ|*default-driver-Description*|  
  
 Il nome *default-driver-Description* corrisponde al nome del valore nella sottochiave ODBC drivers che descrive il driver.  
  
 Se, ad esempio, l'origine dati predefinita usa il driver SQL Server, il valore nella sottochiave predefinita potrebbe essere:  
  
```  
Driver : REG_SZ : SQL Server  
```  
  
> [!NOTE]  
>  Il driver predefinito contenuto nella sottochiave predefinita può fare riferimento a un DSN utente predefinito o a un DSN di sistema predefinito. Se sono stati creati sia un DSN utente predefinito che un DSN di sistema predefinito, il driver predefinito è determinato dal DSN creato per ultimo, quindi potrebbe non essere una voce valida per il DSN creato per primo.
