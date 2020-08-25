---
description: Acquisisci codici di errore ADO
title: Codici di errore ADO | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 02/15/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- errors [ADO], error codes
ms.assetid: 3aee61c7-a9b7-4596-b78e-5828a00d0281
author: rothja
ms.author: jroth
ms.openlocfilehash: b5c3f5f00355bb2c9f9762db1d317a592b4df7dc
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/25/2020
ms.locfileid: "88805335"
---
# <a name="capture-ado-error-codes"></a>Acquisisci codici di errore ADO
Oltre agli errori del provider restituiti negli oggetti [Error](../../reference/ado-api/error-object.md) della raccolta [Errors](../../reference/ado-api/errors-collection-ado.md) , ADO può restituire errori al meccanismo di gestione delle eccezioni dell'ambiente di Runtime. Usare il meccanismo di intercettazione degli errori del linguaggio di programmazione, ad esempio l'istruzione **On Error** in Microsoft® Visual Basic o il blocco **try-catch** in Microsoft Visual C++®, per acquisire gli errori ADO.

 Per l'elenco dei codici di errore ADO, vedere [ErrorValueEnum](../../reference/ado-api/errorvalueenum.md).

## <a name="see-also"></a>Vedere anche
 Raccolta errori [oggetto errore](../../reference/ado-api/error-object.md) [(ADO)](../../reference/ado-api/errors-collection-ado.md)