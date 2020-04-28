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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: deca1648d6ef4f9ba3a1dfd020dc5193c8cc0d25
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "67932428"
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
  
|||  
|-|-|  
|[Metodo GetDataProviderDSO](../../../ado/reference/ado-api/getdataproviderdso-method.md)|Recupera l'oggetto origine dati OLE DB sottostante dal provider di forme.|  
  
## <a name="requirements"></a>Requisiti  
 **Versione:** ADO 2,0 e versioni successive  
  
 **Libreria:** msado15. dll  
  
 **UUID:** 00000283-0000-0010-8000-00AA006D2EA4
