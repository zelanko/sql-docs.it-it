---
description: Metodo SetDefaults (classe SInstance)
title: Metodo sedefaults (SInstance)
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- SetDefaults Method (SInstance Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SetDefaults method
ms.assetid: dc3c6a85-0711-4688-bf4f-91168c57af28
author: markingmyname
ms.author: maghan
ms.openlocfilehash: cd00c04c726885966014cb40d0174e2226a4feb2
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/08/2020
ms.locfileid: "89537609"
---
# <a name="setdefaults-method-sinstance-class"></a>Metodo SetDefaults (classe SInstance)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  Imposta tutti i valori predefiniti per l'istanza di [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] con l'opzione per sovrascrivere i dati esistenti.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
object.SetDefaults(OverwriteAll)  
```  
  
## <a name="parts"></a>Parti  
 *object*  
 Oggetto della [classe SInstance](../../../relational-databases/wmi-provider-configuration-classes/sinstance-class/sinstance-class.md) che rappresenta un'istanza del server.  
  
#### <a name="parameters"></a>Parametri  
  
|Parametro|Descrizione|  
|---------------|-----------------|  
|*OverwriteAll*|Valore booleano che specifica se sovrascrivere il valore esistente nell'istanza del [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] client: **true** se i dati esistenti vengono sovrascritti oppure **false** se i dati esistenti non vengono sovrascritti.|  
  
## <a name="property-valuereturn-value"></a>Valore proprietà/Valore restituito  
 Valore **uint32** che è 0 se il servizio è stato modificato correttamente, 1 se la richiesta non è supportata e qualsiasi altro numero per indicare un errore.  
  
## <a name="remarks"></a>Osservazioni  
  
## <a name="see-also"></a>Vedere anche  
 [Configurazione di protocolli di rete server e di librerie di rete](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
