---
title: Caso dell'identificatore Documenti Microsoft
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
ms.openlocfilehash: 940d96ece6b2c344fa02e0daadd6248270f4d19e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300151"
---
# <a name="identifier-case"></a>Maiuscole/minuscole per gli identificatori
Nelle istruzioni SQL e negli argomenti della funzione di catalogo, gli identificatori e gli identificatori tra virgolette possono fare tra maiuscole e minuscole o meno, che un'applicazione può determinare chiamando **SQLGetInfo** con le opzioni SQL_IDENTIFIER_CASE e SQL_QUOTED_IDENTIFIER_CASE.  
  
 Ognuna di queste opzioni dispone di quattro possibili valori restituiti, uno che indica che l'identificatore o l'identificatore tra virgolette è sensibile e tre che indica che non è sensibile. I tre valori che non fanno distinzione tra maiuscole e minuscole descrivono ulteriormente il caso in cui gli identificatori vengono archiviati nel catalogo di sistema. La modalità di archiviazione degli identificatori nel catalogo di sistema è rilevante solo ai fini della visualizzazione, ad esempio quando un'applicazione visualizza i risultati di una funzione di catalogo. non modifica la distinzione tra maiuscole e minuscole degli identificatori.
