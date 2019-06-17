---
title: ConnectOptionEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ConnectOptionEnum
helpviewer_keywords:
- ConnectOptionEnum enumeration [ADO]
ms.assetid: bff07eeb-dee3-4e4e-9b2d-d56061ea744d
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 5cecd58998e84b608c5bece462bf58d7f376e237
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66698623"
---
# <a name="connectoptionenum"></a>ConnectOptionEnum
Specifica se il [aperto](../../../ado/reference/ado-api/open-method-ado-connection.md) metodo di un [connessione](../../../ado/reference/ado-api/connection-object-ado.md) oggetto deve restituire una volta stabilita la connessione (in modo sincrono) o è precedente (in modo asincrono).  
  
|Costante|Value|Descrizione|  
|--------------|-----------|-----------------|  
|**adAsyncConnect**|16|Apre la connessione in modo asincrono. Il [ConnectComplete](../../../ado/reference/ado-api/connectcomplete-and-disconnect-events-ado.md) evento può essere utilizzato per determinare quando è disponibile la connessione.|  
|**adConnectUnspecified**|-1|Valore predefinito. Apre la connessione in modo sincrono.|  
  
## <a name="adowfc-equivalent"></a>Equivalente di ADO o WFC  
 Package: **com.ms.wfc.data**  
  
|Costante|  
|--------------|  
|AdoEnums.ConnectOption.ASYNCCONNECT|  
|AdoEnums.ConnectOption.CONNECTUNSPECIFIED|  
  
## <a name="applies-to"></a>Si applica a  
 [Metodo Open (connessione ADO)](../../../ado/reference/ado-api/open-method-ado-connection.md)
