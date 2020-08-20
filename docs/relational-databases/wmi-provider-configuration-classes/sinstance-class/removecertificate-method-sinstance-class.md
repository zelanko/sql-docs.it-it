---
description: Metodo RemoveCertificate (classe SInstance)
title: Metodo RemoveCertificate (SInstance)
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- RemoveCertificate Method (SInstance Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- RemoveCertificate method
ms.assetid: 7e5dbafa-a634-4617-9622-510514fce0ce
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: c222a9a11e19aad744dd34570e1b20f3e61cfffd
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88472741"
---
# <a name="removecertificate-method-sinstance-class"></a>Metodo RemoveCertificate (classe SInstance)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  Rimuove il certificato di sicurezza corrente dall'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
object.RemoveCertificate()  
```  
  
## <a name="parts"></a>Parti  
 *object*  
 Oggetto della [classe SInstance](../../../relational-databases/wmi-provider-configuration-classes/sinstance-class/sinstance-class.md) che rappresenta le impostazioni del server in un'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="property-valuereturn-value"></a>Valore proprietà/Valore restituito  
 Valore uint32 che è 0 se il servizio è stato modificato correttamente, 1 se la richiesta non è supportata e qualsiasi altro numero per indicare un errore.  
  
## <a name="remarks"></a>Osservazioni  
  
## <a name="see-also"></a>Vedere anche  
 [Configurazione di protocolli di rete server e di librerie di rete](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
