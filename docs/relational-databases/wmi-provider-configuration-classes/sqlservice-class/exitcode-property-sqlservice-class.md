---
description: Proprietà ExitCode (classe SqlService)
title: Proprietà ExitCode (SqlService)
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- ExitCode Property (SqlService Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- ExitCode property
ms.assetid: e6b8bff2-946f-4abe-bd50-1f7bb11fdddf
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: ab792d72f904511bb17dda140132e86350255fa2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88446123"
---
# <a name="exitcode-property-sqlservice-class"></a>Proprietà ExitCode (classe SqlService)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  Ottiene o imposta il codice di errore [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Win 32 che definisce i problemi verificatisi durante l'avvio e l'arresto del servizio.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
object.ExitCode [= value]  
```  
  
## <a name="parts"></a>Parti  
 *object*  
 Oggetto della [classe SqlService](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/sqlservice-class.md) che rappresenta il servizio.  
  
## <a name="property-valuereturn-value"></a>Valore proprietà/Valore restituito  
 Valore **uint32** che specifica il codice di uscita.  
  
## <a name="remarks"></a>Osservazioni  
 Questa proprietà è impostata su ERROR_SERVICE_SPECIFIC_ERROR (1066) quando l'errore è univoco al servizio rappresentato da questa classe. Tramite il servizio questo valore viene impostato su NO_ERROR in fase di esecuzione e di nuovo al termine.  
  
## <a name="see-also"></a>Vedere anche  
 [Avvio e arresto di servizi](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
