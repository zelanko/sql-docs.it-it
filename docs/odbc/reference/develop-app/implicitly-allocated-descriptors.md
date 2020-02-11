---
title: Descrittori allocati in modo implicito | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], allocating and freeing
- implicitly allocated descriptors [ODBC]
- allocating and freeing descriptors [ODBC]
ms.assetid: 9f88c863-affc-4ab4-a558-63a3ef766f37
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c0eb34866b75802a32c63e62b41d384e5a1dea73
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68138950"
---
# <a name="implicitly-allocated-descriptors"></a>Descrittori allocati in modo implicito
Quando viene allocato un handle di istruzione, l'applicazione alloca in modo implicito un set di quattro descrittori. L'applicazione può ottenere gli handle di questi descrittori allocati in modo implicito come attributi dell'handle di istruzione. Quando l'applicazione libera l'handle di istruzione, il driver libera tutti i descrittori allocati in modo implicito su tale handle.
