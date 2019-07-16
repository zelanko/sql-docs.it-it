---
title: I nomi di correlazione | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- correlation names [ODBC]
- SQL grammar [ODBC], correlation names
ms.assetid: 76c36c6f-f8e1-4ece-a77b-611dde3bdd8a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 535c169123923cdb36c355e098f6e0c55ebb9d56
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68127312"
---
# <a name="correlation-names"></a>Nomi di correlazione
I nomi di correlazione sono completamente supportati, inclusi all'interno dell'elenco di tabelle. Ad esempio, nella stringa seguente, E1 è il nome di correlazione per la tabella Emp denominato:  
  
```  
SELECT * FROM Emp E1   
WHERE E1.LastName = 'Smith'  
```
