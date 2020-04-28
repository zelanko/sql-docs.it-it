---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 738f4cece8cf2355c12c0de4ac42314152c6370a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "67921447"
---
# <a name="adcprop_autorecalc_enum"></a>ADCPROP_AUTORECALC_ENUM
Specifica quando il provider [MSDataShape](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) ricalcola le colonne aggregate e calcolate in un recordset gerarchico.  
  
 Queste costanti vengono utilizzate solo con il provider **MSDataShape** e la proprietà dinamica "**ricalcolo automatico**" del **Recordset** , a cui viene fatto riferimento nell' [indice della proprietà dinamica ADO](../../../ado/reference/ado-api/ado-dynamic-property-index.md) e documentati nel servizio [Microsoft Cursor per OLE DB](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md) o [Microsoft Data Shaping Service per OLE DB](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) documentazione.  
  
|Costante|valore|Descrizione|  
|--------------|-----------|-----------------|  
|**adRecalcAlways**|1|Valore predefinito. Ricalcola ogni volta che il provider **MSDataShape** determina che i valori da cui dipendono le colonne calcolate sono stati modificati.|  
|**adRecalcUpFront**|0|Calcola solo quando si compila inizialmente il **Recordset**gerarchico.|  
  
## <a name="adowfc-equivalent"></a>Equivalente ADO/WFC  
 Queste costanti non dispongono di equivalenti ADO/WFC.
