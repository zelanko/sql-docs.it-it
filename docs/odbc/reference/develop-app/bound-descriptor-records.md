---
title: Record del descrittore associato | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- bound descriptor records [ODBC]
- descriptors [ODBC], bound descriptor records
ms.assetid: 55d09344-6682-40f6-b634-036b134ff650
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4d0016a2849feb5656cb3cd6dd46eff444f37058
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68118756"
---
# <a name="bound-descriptor-records"></a>Record del descrittore associato
Quando l'applicazione imposta il campo SQL_DESC_DATA_PTR di un record del descrittore in modo che non contenga più un valore null, il record viene definito *associato*.  
  
 Se il descrittore è un APD, ogni record associato costituisce un parametro associato. Per i parametri di input, l'applicazione deve associare un parametro per ogni marcatore di parametro dinamico nell'istruzione SQL prima dell'esecuzione dell'istruzione. Per i parametri di output, l'applicazione non deve associare il parametro.  
  
 Se il descrittore è un ARD, che descrive una riga di dati del database, ogni record associato costituisce una colonna associata.
