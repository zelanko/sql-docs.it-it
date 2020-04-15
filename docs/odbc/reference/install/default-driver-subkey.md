---
title: Sottochiave del driver predefinito Documenti Microsoft
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
ms.openlocfilehash: bb134d670964e352d94c13474d8a72fa4bd494ba
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301054"
---
# <a name="default-driver-subkey"></a>Sottochiave Default del driver
La sottochiave Default contiene un singolo valore che descrive il driver utilizzato dall'origine dati predefinita. Il formato di questo valore è illustrato nella tabella seguente.  
  
|Nome|Tipo di dati|Data|  
|----------|---------------|----------|  
|**autista**|REG_SZ|*default-driver-description*|  
  
 Il nome *predefinito-driver-descrizione* è lo stesso nome del valore nella sottochiave Drivers ODBC che descrive il driver.  
  
 Ad esempio, se l'origine dati predefinita utilizza il driver di SQL Server, il valore nella sottochiave Default potrebbe essere:  
  
```  
Driver : REG_SZ : SQL Server  
```  
  
> [!NOTE]  
>  Il driver predefinito contenuto nella sottochiave Default può fare riferimento a un DSN utente predefinito o a un DSN di sistema predefinito. Se sono stati creati sia un DSN utente predefinito che un DSN di sistema predefinito, il driver predefinito è determinato dal DSN creato per ultimo, pertanto potrebbe non essere una voce valida per il DSN creato per primo.
