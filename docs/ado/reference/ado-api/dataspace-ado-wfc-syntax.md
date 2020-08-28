---
description: DataSpace (sintassi ADO/WFC)
title: DataSpace (sintassi ADO-WFC) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- DataSpace collection [ADO], ADO/WFC syntax
ms.assetid: 950d45d8-07de-467b-b255-f9a7b997204c
author: rothja
ms.author: jroth
ms.openlocfilehash: 6fdc89f6fb9c1c32236d7e4da02ad2afb118ba08
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2020
ms.locfileid: "88974252"
---
# <a name="dataspace-ado---wfc-syntax"></a>DataSpace (sintassi ADO/WFC)
Il metodo **CreateObject** della classe **DataSpace** specifica un oggetto business per elaborare le richieste dell'applicazione client (*ProgID*) e il protocollo di comunicazione e il server (*connessione*). **CreateObject** restituisce un oggetto [ObjectProxy](../../../ado/reference/ado-api/objectproxy-ado-wfc-syntax.md) che rappresenta il server.  
  
## <a name="package-commswfcdata"></a>pacchetto com. ms. wfc. Data  
  
### <a name="constructor"></a>Costruttore  
  
```  
public DataSpace()  
```  
  
### <a name="methods"></a>Metodi  
  
```  
public static ObjectProxy DataSpace.createObject(String  
    progid, String connection)  
```  
  
### <a name="properties"></a>Proprietà  
  
```  
public static int getInternetTimeout()  
public static void setInternetTimeout(int plInetTimeout)  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Oggetto DataSpace (Servizi Desktop remoto)](../../../ado/reference/rds-api/dataspace-object-rds.md)
