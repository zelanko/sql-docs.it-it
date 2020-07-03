---
title: Proprietà StartMode (SqlService)
ms.custom: seo-lt-2019
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- StartMode Property (SqlService Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- StartMode property
ms.assetid: c0c2c7f8-d4ae-44f2-ad8e-aecfcb7c2878
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 6c6aab858d98baa0404e4ef5f33adc16ece687d8
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/02/2020
ms.locfileid: "85888321"
---
# <a name="startmode-property-sqlservice-class"></a>Proprietà StartMode (classe SqlService)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  Ottiene la modalità di avvio del servizio.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
object.StartMode [= value]  
```  
  
## <a name="parts"></a>Parti  
 *object*  
 Oggetto della [classe SqlService](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/sqlservice-class.md) che rappresenta il servizio.  
  
## <a name="property-valuereturn-value"></a>Valore proprietà/Valore restituito  
 Valore uint32 che specifica la modalità del servizio.  
  
 I valori possibili sono i seguenti:  
  
 Avvio  
 Valore = 0. Servizio avviato dal caricatore del sistema operativo. Questa opzione è valida solo per i servizi del driver.  
  
 System  
 Valore = 1. Servizio avviato dal metodo **IoInitSystem** . Questa opzione è valida solo per i servizi del driver.  
  
 Automatico  
 Valore = 2. Servizio da avviare automaticamente da Gestione controllo servizi durante l'avvio del sistema.  
  
 Manuale  
 Valore = 3. Servizio da avviare da Gestione computer quando un processo chiama il metodo **StartService** .  
  
 Disabilitata  
 Valore = 4. Impossibile avviare il servizio.  
  
## <a name="remarks"></a>Osservazioni  
  
## <a name="see-also"></a>Vedere anche  
 [Avvio e arresto di servizi](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
