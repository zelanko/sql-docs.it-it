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
ms.openlocfilehash: 819fb89d7f8c43e76ba9260a72fafa68084bf880
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67933440"
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
