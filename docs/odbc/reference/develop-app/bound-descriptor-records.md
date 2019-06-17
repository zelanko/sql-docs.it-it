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
manager: craigg
ms.openlocfilehash: 6f7d21a1166868603f9389ab4ef5c5b3448b0312
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63199525"
---
# <a name="bound-descriptor-records"></a>Record del descrittore associato
Quando l'applicazione imposta il campo SQL_DESC_DATA_PTR di un record del descrittore in modo che non contiene un valore null, il record viene detto *associato*.  
  
 Se il descrittore è un APD, ogni record associato costituiscono un parametro associato. Per i parametri di input, l'applicazione deve associare un parametro per ogni marcatore di parametro dinamico nell'istruzione SQL prima di eseguire l'istruzione. Per i parametri di output, l'applicazione non necessario associare il parametro.  
  
 Se il descrittore è un ARD, che descrive una riga di dati del database, ogni record associato si intende una colonna associata.
