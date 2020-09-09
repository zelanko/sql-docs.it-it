---
description: Proprietà ErrorControl (classe SqlService)
title: Proprietà ErrorControl (SqlService)
ms.custom: seo-lt-2019
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- ErrorControl Property (SqlService Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- ErrorControl property
ms.assetid: cbb1e0fa-5bfc-4b1b-a6ed-f7d5cfad4d73
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 6c0c802c236495a5de48c2617a76f4422e608fca
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/08/2020
ms.locfileid: "89545239"
---
# <a name="errorcontrol-property-sqlservice-class"></a>Proprietà ErrorControl (classe SqlService)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  Ottiene o imposta la gravità dell'errore se il servizio non viene avviato durante l'avvio del computer.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
object.ErrorControl [= value]  
```  
  
## <a name="parts"></a>Parti  
 *object*  
 Oggetto della [classe SqlService](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/sqlservice-class.md) che rappresenta il servizio.  
  
## <a name="property-valuereturn-value"></a>Valore proprietà/Valore restituito  
 Valore string che specifica la gravità dell'errore riportato se il servizio non viene avviato durante l'avvio del computer. Nella tabella seguente sono illustrati i possibili valori.  
  
 Ignora  
 L'utente non viene notificato.  
  
 Normale  
 L'utente viene notificato.  
  
 Severe  
 Il sistema viene riavviato con l'ultima configurazione valida nota.  
  
 Critico  
 Il sistema tenta un riavvio con una configurazione valida.  
  
 Sconosciuto  
 La gravità è sconosciuta.  
  
## <a name="remarks"></a>Osservazioni  
 Il valore indica l'azione intrapresa dal programma di avvio in caso di errore. Tutti gli errori vengono registrati dal computer.  
  
## <a name="see-also"></a>Vedere anche  
 [Avvio e arresto di servizi](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
