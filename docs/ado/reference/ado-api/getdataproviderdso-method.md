---
title: Metodo GetDataProviderDSO | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- GetDataProviderDSO Method [ADO]
ms.assetid: 5a4c6bd5-0c79-4f81-a977-0561392d8d50
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 5187e8f9fdce65b8e746a4a18a353462bb353d4f
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66698033"
---
# <a name="getdataproviderdso-method"></a>Metodo GetDataProviderDSO
Recupera l'oggetto origine dati OLE DB sottostante dal provider di forma.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
HRESULT GetDataProviderDSO(  
      IUnknown **ppDataProviderDSOIUnknown  
);  
```  
  
#### <a name="parameters"></a>Parametri  
 *ppDataProviderDSOIUnknown*  
 [out]  Un puntatore a un puntatore che restituisce l'IUnknown dell'oggetto origine dati OLE DB sottostante.  
  
## <a name="remarks"></a>Note  
 Questo metodo non non addref il puntatore di interfaccia. Se il chiamante prevede di spostare il puntatore, il chiamante deve effettuare la necessaria addref e release.  
  
## <a name="applies-to"></a>Si applica a  
 [Interfaccia IDSOShapeExtensions](../../../ado/reference/ado-api/idsoshapeextensions-interface.md)
