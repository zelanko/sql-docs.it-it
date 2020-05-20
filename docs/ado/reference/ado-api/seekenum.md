---
title: SeekEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- SeekEnum
helpviewer_keywords:
- SeekEnum enumeration [ADO]
ms.assetid: f0ec0c92-8253-47c6-9a14-e5dbccbad219
author: rothja
ms.author: jroth
ms.openlocfilehash: dca33c975b3d25347b0cb9bb804b852ec5f93d7d
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/04/2020
ms.locfileid: "82765392"
---
# <a name="seekenum"></a>SeekEnum
Specifica il tipo di [ricerca](../../../ado/reference/ado-api/seek-method.md) da eseguire.  
  
|Costante|Valore|Descrizione|  
|--------------|-----------|-----------------|  
|**adSeekFirstEQ**|1|Cerca la prima chiave uguale ai *valori*di chiave.|  
|**adSeekLastEQ**|2|Cerca l'ultima chiave uguale ai *valori*di chiave.|  
|**adSeekAfterEQ**|4|Cerca una chiave uguale a un *valore* di chiave o subito dopo dove si è verificata la corrispondenza.|  
|**adSeekAfter**|8|Cerca una chiave subito dopo dove si è verificata una corrispondenza con i *valori* di chiave.|  
|**adSeekBeforeEQ**|16|Cerca una chiave uguale a un *valore*di chiave o immediatamente prima del punto in cui si è verificata la corrispondenza.|  
|**adSeekBefore**|32|Cerca una chiave immediatamente prima del verificarsi di una corrispondenza con i *valori* di chiave.|  
  
## <a name="adowfc-equivalent"></a>Equivalente ADO/WFC  
 Pacchetto: **com. ms. wfc. Data**  
  
|Costante|  
|--------------|  
|AdoEnums. Seek. FIRSTEQ|  
|AdoEnums. Seek. LASTEQ|  
|AdoEnums. Seek. AFTEREQ|  
|AdoEnums. Seek. AFTER|  
|AdoEnums. Seek. BEFOREEQ|  
|AdoEnums. Seek. BEFORe|  
  
## <a name="applies-to"></a>Si applica a  
 [Seek (metodo)](../../../ado/reference/ado-api/seek-method.md)
