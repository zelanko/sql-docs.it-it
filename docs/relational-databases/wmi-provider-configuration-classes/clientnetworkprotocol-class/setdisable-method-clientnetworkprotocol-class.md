---
description: Metodo SetDisable (classe ClientNetworkProtocol)
title: Metodo sedisable (ClientNetworkProtocol)
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- SetDisable Method (ClientNetworkProtocol Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SetDisable method
ms.assetid: bce69ab9-ea5b-43fd-8114-08b1b5890755
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 73430317142354c33b973ee5dca6f0748ba1d6cb
ms.sourcegitcommit: 783b35f6478006d654491cb52f6edf108acf2482
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/09/2020
ms.locfileid: "91889210"
---
# <a name="setdisable-method-clientnetworkprotocol-class"></a>Metodo SetDisable (classe ClientNetworkProtocol)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  Disabilita il protocollo di rete client specificato dalla [configurazione dei protocolli client](../../../database-engine/configure-windows/configure-client-protocols.md).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
object.SetDisable()  
```  
  
## <a name="parts"></a>Parti  
 *object*  
 Oggetto della [classe ClientNetworkProtocol](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocol-class/clientnetworkprotocol-class.md) che rappresenta il protocollo di rete utilizzato dal [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] client.  
  
## <a name="property-valuereturn-value"></a>Valore proprietà/Valore restituito  
 Valore **uint32** che è 0 se il servizio è stato modificato correttamente, 1 se la richiesta non è supportata e qualsiasi altro numero per indicare un errore.  
  
## <a name="remarks"></a>Commenti  
  
## <a name="see-also"></a>Vedere anche  
 [Configurazione di protocolli di rete client e di librerie di rete](../../../database-engine/configure-windows/configure-client-protocols.md)  
  
