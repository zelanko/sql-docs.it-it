---
title: Interfaccia IDSOShapeExtensions | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- IDSOShapeExtensions interface [ADO]
ms.assetid: ad4ba313-1161-4bc7-b8f6-4083305bc81e
author: rothja
ms.author: jroth
ms.openlocfilehash: 02eedbeaf8c9d85f3a896b8991661461825b2b19
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/28/2020
ms.locfileid: "87242671"
---
# <a name="idsoshapeextensions-interface"></a>Interfaccia IDSOShapeExtensions
Ottiene l'oggetto origine dati OLE DB sottostante per il provider di forme.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
interface IDSOShapeExtensions: public IUnknown {  
public:  
      HRESULT  GetDataProviderDSO(  
            IUnknown **ppDataProviderDSOIUnknown  
      );  
};  
```  
  
## <a name="methods"></a>Metodi  
  
|Metodo|Descrizione|  
|-|-|  
|[Metodo GetDataProviderDSO](../../../ado/reference/ado-api/getdataproviderdso-method.md)|Recupera l'oggetto origine dati OLE DB sottostante dal provider di forme.|  
  
## <a name="requirements"></a>Requisiti  
 **Versione:** ADO 2,0 e versioni successive  
  
 **Libreria:** msado15.dll  
  
 **UUID:** 00000283-0000-0010-8000-00AA006D2EA4
