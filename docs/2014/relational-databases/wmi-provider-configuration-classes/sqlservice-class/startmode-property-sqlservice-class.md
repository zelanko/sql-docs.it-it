---
title: Proprietà StartMode (classe SqlService) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
api_name:
- StartMode Property (SqlService Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- StartMode property
ms.assetid: c0c2c7f8-d4ae-44f2-ad8e-aecfcb7c2878
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: bf77e36824c05a0f07bc789c380cffbc1518669d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63187830"
---
# <a name="startmode-property-sqlservice-class"></a>Proprietà StartMode (classe SqlService)
  Ottiene la modalità di avvio del servizio.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
object  
.StartMode [= value]  
```  
  
## <a name="parts"></a>Parti  
 *object*  
 Oggetto della [classe SqlService](sqlservice-class.md) che rappresenta il servizio.  
  
## <a name="property-valuereturn-value"></a>Valore proprietà/Valore restituito  
 Valore uint32 che specifica la modalità del servizio.  
  
 I valori possibili sono i seguenti:  
  
 Avvio  
 Valore = 0. Servizio avviato dal caricatore del sistema operativo. Questa opzione è valida solo per i servizi del driver.  
  
 Sistema  
 Valore = 1. Servizio avviato dal metodo `IoInitSystem`. Questa opzione è valida solo per i servizi del driver.  
  
 Automatico  
 Valore = 2. Servizio da avviare automaticamente da Gestione controllo servizi durante l'avvio del sistema.  
  
 Manual  
 Valore = 3. Servizio da avviare da Gestione computer quando un processo chiama il metodo `StartService`.  
  
 Disabilitata  
 Valore = 4. Impossibile avviare il servizio.  
  
## <a name="remarks"></a>Note  
  
## <a name="see-also"></a>Vedere anche  
 [Avvio e arresto di servizi](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
