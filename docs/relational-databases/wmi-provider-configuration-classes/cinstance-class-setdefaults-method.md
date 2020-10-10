---
description: Classe CInstance - Metodo SetDefaults
title: Metodo sedefaults (CInstance)
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- SetDefaults Method (CInstance Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SetDefaults method
ms.assetid: ed9e99c2-3e28-4ee8-bc20-61ca05984973
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 99771d12be4c10d8d4b823ceb788e9722d417fca
ms.sourcegitcommit: 783b35f6478006d654491cb52f6edf108acf2482
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/09/2020
ms.locfileid: "91890981"
---
# <a name="cinstance-class---setdefaults-method"></a>Classe CInstance - Metodo SetDefaults
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Imposta tutti i valori predefiniti per l'istanza del [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] client con l'opzione per sovrascrivere i dati esistenti.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
object.SetDefaults(OverwriteAll)  
```  
  
## <a name="parts"></a>Parti  
 *object*  
 Oggetto della [classe CInstance](../../relational-databases/wmi-provider-configuration-classes/cinstance-class.md) che rappresenta un'istanza del client di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
#### <a name="parameters"></a>Parametri  
  
|Parametro|Descrizione|  
|---------------|-----------------|  
|*OverwriteAll*|Valore booleano che specifica se sovrascrivere i valori esistenti nell'istanza del [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] client: **true** per sovrascrivere i dati esistenti oppure **false** se i dati esistenti non devono essere sovrascritti.|  
  
## <a name="property-valuereturn-value"></a>Valore proprietà/Valore restituito  
 Valore **uint32** che è 0 se il servizio è stato modificato correttamente, 1 se la richiesta non è supportata e qualsiasi altro numero per indicare un errore.  
  
## <a name="remarks"></a>Commenti  
  
## <a name="see-also"></a>Vedere anche  
 [Configurazione di protocolli client](../../database-engine/configure-windows/configure-client-protocols.md)  
  
