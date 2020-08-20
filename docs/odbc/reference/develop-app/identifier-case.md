---
description: Maiuscole/minuscole per gli identificatori
title: Caso identificatore | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- identifiers [ODBC], case
- interoperability of SQL statements [ODBC], identifier case
ms.assetid: ee8a31aa-389d-4dd1-bfa9-547f6b50bc70
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ccac9b10e6a32c7265cd5f591944735454b85f80
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461443"
---
# <a name="identifier-case"></a>Maiuscole/minuscole per gli identificatori
Nelle istruzioni SQL e negli argomenti della funzione Catalog, gli identificatori e gli identificatori delimitati possono essere o meno con distinzione tra maiuscole e minuscole, che un'applicazione può determinare chiamando **SQLGetInfo** con le opzioni SQL_IDENTIFIER_CASE e SQL_QUOTED_IDENTIFIER_CASE.  
  
 Ognuna di queste opzioni ha quattro possibili valori restituiti: uno indica che l'identificatore o il case identificatore tra virgolette è sensibile e tre indica che non è sensibile. I tre valori che non fanno distinzione tra maiuscole e minuscole descrivono ulteriormente il caso in cui gli identificatori vengono archiviati nel catalogo di sistema. Il modo in cui gli identificatori vengono archiviati nel catalogo di sistema è pertinente solo a scopo di visualizzazione, ad esempio quando un'applicazione Visualizza i risultati di una funzione di catalogo. non modifica la distinzione tra maiuscole e minuscole degli identificatori.
