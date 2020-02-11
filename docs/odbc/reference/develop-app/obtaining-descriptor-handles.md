---
title: Recupero di handle descrittore | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], retrieving or setting field values
ms.assetid: 936f983f-c7e9-43f3-97ea-dd4b1bbf4654
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8bfa0b36ecca3af655efde84c3ce3f22ab0c1f88
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68086313"
---
# <a name="obtaining-descriptor-handles"></a>Recupero di handle descrittore
Un'applicazione ottiene l'handle di qualsiasi descrittore allocato in modo esplicito come argomento di output della chiamata a **SQLAllocHandle**. L'handle di un descrittore allocato in modo implicito viene ottenuto chiamando **SQLGetStmtAttr**.
