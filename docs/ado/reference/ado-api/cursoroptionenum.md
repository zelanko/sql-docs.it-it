---
title: CursorOptionEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- CursorOptionEnum
helpviewer_keywords:
- CursorOptionEnum enumeration [ADO]
ms.assetid: 4e10cda7-ce81-4466-94c2-844d38191cf1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1d5cc44950754c4b63e644d2d9210edcc94bd9ff
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67933269"
---
# <a name="cursoroptionenum"></a>CursorOptionEnum
Specifica la funzionalità che il metodo [supporta](../../../ado/reference/ado-api/supports-method.md) deve testare.  
  
|Costante|valore|Descrizione|  
|--------------|-----------|-----------------|  
|**adAddNew**|0x1000400|Supporta il metodo [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md) per aggiungere nuovi record.|  
|**adApproxPosition**|0x4000|Supporta le proprietà [AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md) e [AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md) .|  
|**adBookmark**|0x2000|Supporta la proprietà [Bookmark](../../../ado/reference/ado-api/bookmark-property-ado.md) per accedere a record specifici.|  
|**adDelete**|0x1000800|Supporta il metodo [Delete](../../../ado/reference/ado-api/delete-method-ado-recordset.md) per eliminare i record.|  
|**adFind**|0x80000|Supporta il metodo [Find](../../../ado/reference/ado-api/find-method-ado.md) per individuare una riga in un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md).|  
|**adHoldRecords**|0x100|Recupera più record o modifica la posizione successiva senza eseguire il commit di tutte le modifiche in sospeso.|  
|**adIndex**|0x100000|Supporta la proprietà [index](../../../ado/reference/ado-api/index-property.md) per assegnare un nome a un indice.|  
|**adMovePrevious**|0x200|Supporta i metodi [MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md) e [MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md) e i metodi [Move](../../../ado/reference/ado-api/move-method-ado.md) o [GetRows](../../../ado/reference/ado-api/getrows-method-ado.md) per spostare la posizione del record corrente indietro senza richiedere segnalibri.|  
|**adNotify**|0x40000|Indica che il provider di dati sottostante supporta le notifiche, che determinano se gli eventi del **Recordset** sono supportati.|  
|**adResync**|0x20000|Supporta il metodo di [Risincronizzazione](../../../ado/reference/ado-api/resync-method.md) per aggiornare il cursore con i dati visibili nel database sottostante.|  
|**adSeek**|0x200000|Supporta il metodo [Seek](../../../ado/reference/ado-api/seek-method.md) per individuare una riga in un **Recordset**.|  
|**adUpdate**|0x1008000|Supporta il metodo [Update](../../../ado/reference/ado-api/update-method.md) per modificare i dati esistenti.|  
|**adUpdateBatch**|0x10000|Supporta l'aggiornamento in batch (metodi[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) e [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md) ) per trasmettere i gruppi di modifiche al provider.|  
  
## <a name="adowfc-equivalent"></a>Equivalente ADO/WFC  
 Pacchetto: **com. ms. wfc. Data**  
  
|Costante|  
|--------------|  
|AdoEnums. CursorOption. ADDNEW|  
|AdoEnums. CursorOption. APPROXPOSITION|  
|AdoEnums. CursorOption. BOOKMARK|  
|AdoEnums. CursorOption. DELETE|  
|AdoEnums. CursorOption. FIND|  
|AdoEnums. CursorOption. HOLDRECORDS|  
|AdoEnums. CursorOption. INDEX|  
|AdoEnums. CursorOption. MOVEPREVIOUS|  
|AdoEnums. CursorOption. NOTIFY|  
|AdoEnums. CursorOption. Resync|  
|AdoEnums. CursorOption. SEEK|  
|AdoEnums. CursorOption. UPDATE|  
|AdoEnums. CursorOption. UPDATEBATCH|  
  
## <a name="applies-to"></a>Si applica a  
 [Metodo Supports](../../../ado/reference/ado-api/supports-method.md)
