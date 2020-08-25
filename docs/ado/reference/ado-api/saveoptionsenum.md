---
description: SaveOptionsEnum
title: SaveOptionsEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- SaveOptionsEnum
helpviewer_keywords:
- SaveOptionsEnum enumeration [ADO]
ms.assetid: 59339100-6e29-48d1-aea3-6873796d186b
author: rothja
ms.author: jroth
ms.openlocfilehash: edac11f61b003307703ec13daed8022b8af31bae
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/24/2020
ms.locfileid: "88777560"
---
# <a name="saveoptionsenum"></a>SaveOptionsEnum
Specifica se un file deve essere creato o sovrascritto durante il salvataggio da un oggetto [flusso](./stream-object-ado.md) . I valori possono essere **adSaveCreateNotExist** o **adSaveCreateOverwrite**.  
  
|Costante|valore|Descrizione|  
|--------------|-----------|-----------------|  
|**adSaveCreateNotExist**|1|Valore predefinito. Crea un nuovo file se il file specificato dal parametro *filename* non esiste già.|  
|**adSaveCreateOverWrite**|2|Sovrascrive il file con i dati dell'oggetto **flusso** attualmente aperto, se il file specificato dal parametro *filename* esiste già. Se il file specificato dal parametro *filename* non esiste, viene creato un nuovo file.|  
  
## <a name="adowfc-equivalent"></a>Equivalente ADO/WFC  
 Queste costanti non dispongono di equivalenti ADO/WFC.  
  
## <a name="applies-to"></a>Si applica a  
 [Metodo SaveToFile](./savetofile-method.md)