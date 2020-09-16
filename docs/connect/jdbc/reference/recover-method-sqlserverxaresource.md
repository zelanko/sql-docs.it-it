---
description: Metodo recover (SQLServerXAResource)
title: Metodo recover (SQLServerXAResource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerXAResource.recover
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 840ecfcf-0dd3-4b7b-976f-dc9a96cd1464
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5769fddf9bf39d31f784dd57544fb51769caa754
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88432823"
---
# <a name="recover-method-sqlserverxaresource"></a>Metodo recover (SQLServerXAResource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ottiene un elenco di rami di transazioni preparati da uno strumento di gestione delle risorse.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public javax.transaction.xa.Xid[] recover(int flags)  
```  
  
#### <a name="parameters"></a>Parametri  
 *flags*  
  
 Valore **int** che può accettare uno dei valori seguenti: XAResource.TMSTARTRSCAN o XAResource.TMENDRSCAN o XAResource.TMNOFLAGS o XAResource.TMSTARTTRSCAN | XAResource.TMENDRSCAN.  
  
## <a name="return-value"></a>Valore restituito  
 Oggetto Xid.  
  
## <a name="exceptions"></a>Eccezioni  
 javax.transaction.xa.XAException  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo recover viene specificato dal metodo recover nell'interfaccia javax.transaction.xa.XAResource.  
  
 Se il parametro **flag** non è XAResource.TMSTARTRSCAN o XAResource.TMSTARTRSCAN | XAResource.TMENDRSCAN, deve essere in corso un'analisi di ripristino.  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi di SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-methods.md)   
 [Membri di SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-members.md)   
 [Classe SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md)  
  
  
