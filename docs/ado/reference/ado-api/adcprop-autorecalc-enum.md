---
description: ADCPROP_AUTORECALC_ENUM
title: ADCPROP_AUTORECALC_ENUM | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADCPROP_AUTORECALC_ENUM
helpviewer_keywords:
- ADCPROP_AUTORECALC_ENUM [ADO]
ms.assetid: ded4f087-87b9-4efa-8026-bde53d3e9e8a
author: rothja
ms.author: jroth
ms.openlocfilehash: 7500fd42ef02b974989488b70e668933aaa00cab
ms.sourcegitcommit: c4d564435c008e2c92035efd2658172f20f07b2b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/24/2020
ms.locfileid: "88760266"
---
# <a name="adcprop_autorecalc_enum"></a>ADCPROP_AUTORECALC_ENUM
Specifica quando il provider [MSDataShape](../../guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) ricalcola le colonne aggregate e calcolate in un recordset gerarchico.  
  
 Queste costanti vengono utilizzate solo con il provider **MSDataShape** e la proprietà dinamica "**ricalcolo automatico**" del **Recordset** , a cui viene fatto riferimento nell' [indice della proprietà dinamica ADO](./ado-dynamic-property-index.md) e documentati nel servizio [Microsoft Cursor per OLE DB](../../guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md) o [Microsoft Data Shaping Service per OLE DB](../../guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) documentazione.  
  
|Costante|Valore|Descrizione|  
|--------------|-----------|-----------------|  
|**adRecalcAlways**|1|Valore predefinito. Ricalcola ogni volta che il provider **MSDataShape** determina che i valori da cui dipendono le colonne calcolate sono stati modificati.|  
|**adRecalcUpFront**|0|Calcola solo quando si compila inizialmente il **Recordset**gerarchico.|  
  
## <a name="adowfc-equivalent"></a>Equivalente ADO/WFC  
 Queste costanti non dispongono di equivalenti ADO/WFC.