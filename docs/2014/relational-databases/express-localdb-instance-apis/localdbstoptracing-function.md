---
title: Funzione LocalDBStopTracing | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
api_name:
- LocalDBStopTracing
api_location:
- sqluserinstance.dll
topic_type:
- apiref
ms.assetid: 1d50e040-8602-4ffa-be8f-b8633fdfa7ff
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 023700b1922946cc1234468aeb0551785067666c
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "63128700"
---
# <a name="localdbstoptracing-function"></a>Funzione LocalDBStopTracing
  Viene disabilitata la traccia delle chiamate API per tutte le istanze del database locale SQL Server Express di proprietà dell'utente di Windows corrente.  
  
 **File di intestazione:** sqlncli. h  
  
## <a name="syntax"></a>Sintassi  
  
```  
HRESULT LocalDBStopTracing();  
```  
  
## <a name="returns"></a>Valori di codice restituiti  
 S_OK  
 Funzione completata.  
  
 [LOCALDB_ERROR_INTERNAL_ERROR](../express-localdb-error-messages/localdb-error-internal-error.md)  
 Si è verificato un errore imprevisto. Per informazioni, vedere il registro eventi.  
  
## <a name="remarks"></a>Osservazioni  
 Per un esempio di codice in cui viene utilizzata l'API del database locale, vedere [SQL Server Express riferimento al database locale](../sql-server-express-localdb-reference.md).  
  
## <a name="see-also"></a>Vedi anche  
 [Informazioni sulla versione e intestazione di SQL Server Express LocalDB](sql-server-express-localdb-header-and-version-information.md)  
  
  
