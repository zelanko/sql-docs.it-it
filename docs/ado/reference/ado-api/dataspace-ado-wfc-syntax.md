---
title: Spazio dati (ADO - WFC sintassi) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- DataSpace collection [ADO], ADO/WFC syntax
ms.assetid: 950d45d8-07de-467b-b255-f9a7b997204c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 94a539fb2ba3285bd8bb5c3668879695598725a4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63140101"
---
# <a name="dataspace-ado---wfc-syntax"></a>DataSpace (sintassi ADO/WFC)
Il **createObject** metodo per il **DataSpace** classe specifica sia un oggetto business per elaborare le richieste dell'applicazione client (*progid*) e il protocollo di comunicazione e il server (*connessione*). **createObject** restituisce un [ObjectProxy](../../../ado/reference/ado-api/objectproxy-ado-wfc-syntax.md) oggetto che rappresenta il server.  
  
## <a name="package-commswfcdata"></a>creare un pacchetto com.ms. wfc.  
  
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
