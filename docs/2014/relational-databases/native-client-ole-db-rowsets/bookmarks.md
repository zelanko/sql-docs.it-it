---
title: Segnalibri | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- bookmarks [OLE DB]
- SQL Server Native Client OLE DB provider, bookmarks
- rowsets [OLE DB], bookmarks
- OLE DB rowsets, bookmarks
ms.assetid: 7d9076f2-bf9c-452e-b816-70371a0c1644
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 436cbd68ae60446df94b63283cd3291c9fc63fee
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/01/2020
ms.locfileid: "82704688"
---
# <a name="bookmarks"></a>Segnalibri
  I segnalibri consentono ai consumer di tornare rapidamente su una riga. Grazie ai segnalibri, essi possono accedere in modo casuale alle righe in base al valore del segnalibro. La colonna del segnalibro è la colonna 0 nel set di righe. Il consumer imposta il valore del campo dwFlag della struttura di associazione su DBCOLUMNSINFO_ISBOOKMARK per indicare che la colonna viene utilizzata come segnalibro. Imposta inoltre la proprietà del set di righe DBPROP_BOOKMARKS su VARIANT_TRUE, consentendo alla colonna 0 di essere presente nel set di righe. Viene quindi usato il metodo **IRowsetLocate::GetRowsAt** per recuperare le righe, a partire da quella specificata in corrispondenza di un offset da un segnalibro.  
  
## <a name="see-also"></a>Vedere anche  
 [Set di righe](rowsets.md)  
  
  
