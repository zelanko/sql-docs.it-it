---
title: ObjectProxy (sintassi ADO-WFC) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- ObjectProxy collection [ADO]
ms.assetid: f68f58bc-ad28-46cc-9fb3-099e1a678397
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 485d011fa6762acd04cad54ff7fffc8d8136e063
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67917950"
---
# <a name="objectproxy-ado---wfc-syntax"></a>ObjectProxy (sintassi ADO/WFC)
Un oggetto **ObjectProxy** rappresenta un server e viene restituito dal metodo **CreateObject** dell'oggetto [DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md) . La classe ObjectProxy dispone di un metodo, **Call**, che può richiamare un metodo sul server e restituire un oggetto risultante da tale chiamata.  
  
 **pacchetto com. ms. wfc. Data**  
  
## <a name="methods"></a>Metodi  
  
### <a name="call-method-adowfc-syntax"></a>Metodo Call (sintassi ADO/WFC)  
 Richiama un metodo sul server rappresentato da ObjectProxy. Facoltativamente, gli argomenti del metodo possono essere passati come una matrice di oggetti.  
  
#### <a name="syntax"></a>Sintassi  
  
```  
public Object ObjectProxy.( String method )  
public Object ObjectProxy.( String method, Object[] args)  
```  
  
#### <a name="returns"></a>Valori di codice restituiti  
 Oggetto  
 Oggetto risultante dalla chiamata al metodo.  
  
#### <a name="parameters"></a>Parametri  
 *ObjectProxy*  
 Oggetto **ObjectProxy** che rappresenta il server.  
  
 *Metodo*  
 Stringa contenente il nome del metodo da richiamare sul server.  
  
 *args*  
 Facoltativa. Matrice di oggetti che sono argomenti del metodo nel server. I tipi di dati Java vengono automaticamente convertiti in tipi di dati appropriati per l'utilizzo nel server.
