---
title: Impostazione del cursore Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- scrollable cursors [ODBC]
- cursors [ODBC], scrollable
- cursors [ODBC], creating
ms.assetid: b80afb0e-ef2f-408f-86f5-a392edd99a56
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 805d8076c853513d86f9a3a92d9342d1224226c9
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299801"
---
# <a name="setting-up-the-cursor"></a>Configurazione del cursore
L'applicazione può specificare il tipo di cursore prima di eseguire un'istruzione che crea un set di risultati. Questa operazione viene eseguito con l'attributo dell'istruzione SQL_ATTR_CURSOR_TYPE. Se l'applicazione non specifica in modo esplicito un tipo, verrà utilizzato un cursore forward-only. Per ottenere un cursore misto, un'applicazione specifica un cursore basato su keyset ma dichiara una dimensione del set di chiavi inferiore alla dimensione del set di risultati.  
  
 Per i cursori con chiaveset e misti, l'applicazione può anche specificare le dimensioni del keyset. Questa operazione viene eseguito con l'attributo di istruzione SQL_ATTR_KEYSET_SIZE. Se la dimensione del keyset è impostata su 0, che è l'impostazione predefinita, la dimensione del set di chiavi viene impostata sulla dimensione del set di risultati e viene utilizzato un cursore basato su keyset. La dimensione del keyset può essere modificata dopo l'apertura del cursore.  
  
 L'applicazione può anche impostare le dimensioni del set di righe; Per ulteriori informazioni, vedere [Utilizzo dei cursori](../../../odbc/reference/develop-app/using-block-cursors.md)a blocchi , più indietro in questa sezione.
