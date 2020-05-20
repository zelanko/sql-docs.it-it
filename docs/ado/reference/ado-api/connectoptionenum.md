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
author: rothja
ms.author: jroth
ms.openlocfilehash: fa372f05a80290e907298a0969d9eb9f14355f90
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/04/2020
ms.locfileid: "82762602"
---
# <a name="connectoptionenum"></a>ConnectOptionEnum
Specifica se il metodo [Open](../../../ado/reference/ado-api/open-method-ado-connection.md) di un oggetto [Connection](../../../ado/reference/ado-api/connection-object-ado.md) deve essere restituito dopo che la connessione è stata stabilita (in modalità sincrona) o prima (in modo asincrono).  
  
|Costante|Valore|Descrizione|  
|--------------|-----------|-----------------|  
|**adAsyncConnect**|16|Apre la connessione in modo asincrono. L'evento [ConnectComplete](../../../ado/reference/ado-api/connectcomplete-and-disconnect-events-ado.md) può essere utilizzato per determinare quando la connessione è disponibile.|  
|**adConnectUnspecified**|-1|Valore predefinito. Apre la connessione in modo sincrono.|  
  
## <a name="adowfc-equivalent"></a>Equivalente ADO/WFC  
 Pacchetto: **com. ms. wfc. Data**  
  
|Costante|  
|--------------|  
|AdoEnums. ConnectOption. ASYNCCONNECT|  
|AdoEnums. ConnectOption. CONNECTUNSPECIFIED|  
  
## <a name="applies-to"></a>Si applica a  
 [Metodo Open (Connection - ADO)](../../../ado/reference/ado-api/open-method-ado-connection.md)
