---
description: Metodo GetDataProviderDSO
title: Metodo GetDataProviderDSO | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- GetDataProviderDSO Method [ADO]
ms.assetid: 5a4c6bd5-0c79-4f81-a977-0561392d8d50
author: rothja
ms.author: jroth
ms.openlocfilehash: 85e701cb7ce725aa9afa9d682467c1a97f5dd378
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2020
ms.locfileid: "88972902"
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
 [Interfaccia IDSOShapeExtensions](./idsoshapeextensions-interface.md)