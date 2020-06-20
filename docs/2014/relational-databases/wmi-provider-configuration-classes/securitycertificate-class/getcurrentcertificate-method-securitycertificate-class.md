---
title: Metodo GetCurrentCertificate (classe SecurityCertificate) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
api_name:
- GetCurrentCertificate Method (SecurityCertificate Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- GetCurrentCertificate method
ms.assetid: 987a2671-1801-45c4-93e6-29f883c58720
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 4b79e57afac4509401acc69892eb1665ec73bf84
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85060040"
---
# <a name="getcurrentcertificate-method-securitycertificate-class"></a>Metodo GetCurrentCertificate (classe SecurityCertificate)
  Ottiene il certificato di sicurezza corrente.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
object  
.GetCurrentCertificate(  
SHA , SQLInstance  
)  
  
```  
  
## <a name="parts"></a>Parti  
 *object*  
 Oggetto della [classe SecurityCertificate](securitycertificate-class.md) che rappresenta un certificato di sicurezza.  
  
#### <a name="parameters"></a>Parametri  
  
|Parametro|Descrizione|  
|---------------|-----------------|  
|*SHA*|Valore string (parametro di output) che specifica l'identificazione digitale SHA del certificato di sicurezza corrente dopo il completamento del metodo.|  
|*SQLInstance*|Valore string che specifica l'istanza per la quale viene richiesto il certificato.|  
  
## <a name="property-valuereturn-value"></a>Valore proprietà/Valore restituito  
 Valore `uint32` che è 0 se il servizio è stato modificato correttamente, 1 se la richiesta non è supportata e qualsiasi altro numero per indicare un errore.  
  
## <a name="remarks"></a>Osservazioni  
  
## <a name="see-also"></a>Vedere anche  
 [Configurazione di protocolli di rete server e di librerie di rete](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
