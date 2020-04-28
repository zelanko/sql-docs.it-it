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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 886825b4d32354572a5162487add419b00ec35d6
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "67931060"
---
# <a name="seekenum"></a>SeekEnum
Specifica il tipo di [ricerca](../../../ado/reference/ado-api/seek-method.md) da eseguire.  
  
|Costante|valore|Descrizione|  
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
