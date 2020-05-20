---
title: Metodo get_OLEDBCommand | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- get_OLEDBCommand method [ADO]
ms.assetid: 23d551f5-3d5b-434b-ade6-fef15f1710e7
author: rothja
ms.author: jroth
ms.openlocfilehash: 043e432bfef39f90fbeb5b147487272c4d284bdb
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/04/2020
ms.locfileid: "82760077"
---
# <a name="get_oledbcommand-method"></a>Metodo get_OLEDBCommand
Restituisce il comando OLE DB sottostante, propagando prima di tutto le informazioni sui parametri impostate nel comando ADO al comando OLE DB.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
HRESULT get_OLEDBCommand(  
      IUnknown **ppOLEDBCommand  
);  
```  
  
#### <a name="parameters"></a>Parametri  
 *ppOLEDBCommand*  
 out Puntatore a una posizione del puntatore in cui verrà scritto il puntatore IUnknown per il OLE DB comando sottostante.  
  
## <a name="applies-to"></a>Si applica a  
 [IADOCommandConstruction](https://msdn.microsoft.com/d8e54333-00eb-4b72-bf4a-ca92c7ca5f86)
