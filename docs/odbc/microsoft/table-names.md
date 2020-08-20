---
description: Nomi di tabella
title: Nomi di tabella | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL grammar [ODBC], table names
- table names [ODBC]
ms.assetid: f7a5cb0a-3be7-4f46-82f9-64ffdbceaa9b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5b264999f800e4387099240526f558110c39e27a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471459"
---
# <a name="table-names"></a>Nomi di tabella
Quando si usa il driver dBASE, Microsoft Excel, Paradox o text, i nomi di tabella che si verificano nella clausola FROM di SELECT o DELETE, dopo la clausola INTO in INSERT e After UPDATE, CREATE TABLE e DROP TABLE possono contenere un percorso valido, un nome primario e un'estensione di file.  
  
 L'uso di un nome di tabella in un'altra posizione in un'istruzione SQL non supporta l'uso di percorsi o estensioni, ma accetta solo il nome primario (ad esempio, EMP da C:\ABC\EMP).  
  
 È possibile utilizzare i nomi di correlazione (alias). Ad esempio:  
  
```  
SELECT *    
FROM C:\ABC\EMP T1    
WHERE T1.COL1 = 'aaa'  
```
