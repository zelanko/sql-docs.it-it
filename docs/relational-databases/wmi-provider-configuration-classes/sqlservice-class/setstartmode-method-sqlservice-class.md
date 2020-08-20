---
description: Metodo SetStartMode (classe SqlService)
title: Metodo SetStartMode (SqlService)
ms.custom: seo-lt-2019
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- SetStartMode Method (SqlService Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SetStartMode method
ms.assetid: f6f198b4-f9a4-468c-8977-76462ef06e61
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: b60886ac53fc31a2c0a0da469ace5adfdb1b1d74
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88488346"
---
# <a name="setstartmode-method-sqlservice-class"></a>Metodo SetStartMode (classe SqlService)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  Modifica la modalità di avvio dell'istanza del servizio.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
object.SetStartMode(StartMode)  
```  
  
## <a name="parts"></a>Parti  
 *object*  
 Oggetto della [classe SqlService](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/sqlservice-class.md) che rappresenta il servizio.  
  
#### <a name="parameters"></a>Parametri  
 *Modalità avvio*  
 Valore **uint32** che specifica la modalità di avvio dell'istanza del servizio.  
  
 I valori validi sono i seguenti:  
  
 Valore = 0. Boot: driver di dispositivo avviato dal caricatore del sistema operativo. Questo valore è valido solo per i servizi del driver.  
  
 Valore = 1. System: driver di dispositivo avviato dal metodo **IoInitSystem** . Questo valore è valido solo per i servizi del driver.  
  
 Valore = 2. Automatic: servizio da avviare automaticamente da Gestione controllo servizi durante l'avvio del sistema.  
  
 Valore = 3. Manual: servizio da avviare da Gestione computer quando un processo chiama il metodo **StartService** .  
  
 Valore = 4. Disabled: impossibile avviare il servizio.  
  
## <a name="property-valuereturn-value"></a>Valore proprietà/Valore restituito  
 Valore **uint32** che è 0 se il servizio è stato modificato correttamente 0 1 se la richiesta non è supportata. Qualsiasi altro numero indica un errore.  
  
## <a name="remarks"></a>Osservazioni  
  
## <a name="see-also"></a>Vedere anche  
 [Avvio e arresto di servizi](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
