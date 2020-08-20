---
description: Descrittori allocati in modo implicito
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5daa7f622798e1394c186b333069933b48e367af
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461423"
---
# <a name="implicitly-allocated-descriptors"></a>Descrittori allocati in modo implicito
Quando viene allocato un handle di istruzione, l'applicazione alloca in modo implicito un set di quattro descrittori. L'applicazione può ottenere gli handle di questi descrittori allocati in modo implicito come attributi dell'handle di istruzione. Quando l'applicazione libera l'handle di istruzione, il driver libera tutti i descrittori allocati in modo implicito su tale handle.
