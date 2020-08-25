---
description: ConnectOptionEnum
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
ms.openlocfilehash: 73fb0218b9a4a9437dbe8c103c8496f0a209e9b1
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/24/2020
ms.locfileid: "88775810"
---
# <a name="connectoptionenum"></a>ConnectOptionEnum
Specifica se il metodo [Open](./open-method-ado-connection.md) di un oggetto [Connection](./connection-object-ado.md) deve essere restituito dopo che la connessione è stata stabilita (in modalità sincrona) o prima (in modo asincrono).  
  
|Costante|valore|Descrizione|  
|--------------|-----------|-----------------|  
|**adAsyncConnect**|16|Apre la connessione in modo asincrono. L'evento [ConnectComplete](./connectcomplete-and-disconnect-events-ado.md) può essere utilizzato per determinare quando la connessione è disponibile.|  
|**adConnectUnspecified**|-1|Valore predefinito. Apre la connessione in modo sincrono.|  
  
## <a name="adowfc-equivalent"></a>Equivalente ADO/WFC  
 Pacchetto: **com. ms. wfc. Data**  
  
|Costante|  
|--------------|  
|AdoEnums. ConnectOption. ASYNCCONNECT|  
|AdoEnums. ConnectOption. CONNECTUNSPECIFIED|  
  
## <a name="applies-to"></a>Si applica a  
 [Metodo Open (Connection - ADO)](./open-method-ado-connection.md)