---
description: Metodo GetDataProviderDSO
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 1a45d78960b8b6b1ba2534e39f080a6c94fc0655
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88443573"
---
# <a name="getdataproviderdso-method"></a>Metodo GetDataProviderDSO
Recupera l'oggetto origine dati OLE DB sottostante dal provider di forme.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
HRESULT GetDataProviderDSO(  
      IUnknown **ppDataProviderDSOIUnknown  
);  
```  
  
#### <a name="parameters"></a>Parametri  
 *ppDataProviderDSOIUnknown*  
 out  Puntatore a un puntatore che restituisce l'IUnknown dell'oggetto origine dati OLE DB sottostante.  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo non AddRef il puntatore di interfaccia. Se il chiamante prevede di mantenere il puntatore, il chiamante deve eseguire il AddRef e il rilascio richiesti.  
  
## <a name="applies-to"></a>Si applica a  
 [Interfaccia IDSOShapeExtensions](../../../ado/reference/ado-api/idsoshapeextensions-interface.md)
