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
manager: craigg
ms.openlocfilehash: ba39c4bdc2bffc3198d780aa155e9ee60000d88a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63308733"
---
# <a name="cursoroptionenum"></a>CursorOptionEnum
Specifica il tipo di funzionalità di [supporta](../../../ado/reference/ado-api/supports-method.md) metodo deve verificare la presenza.  
  
|Costante|Value|Descrizione|  
|--------------|-----------|-----------------|  
|**adAddNew**|0x1000400|Supporta il [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md) metodo per aggiungere nuovi record.|  
|**adApproxPosition**|0x4000|Supporta il [esempio di AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md) e [AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md) proprietà.|  
|**adBookmark**|0x2000|Supporta il [segnalibro](../../../ado/reference/ado-api/bookmark-property-ado.md) proprietà per accedere a record specifici.|  
|**adDelete**|0x1000800|Supporta il [eliminare](../../../ado/reference/ado-api/delete-method-ado-recordset.md) metodo per eliminare i record.|  
|**adFind**|0x80000|Supporta il [trovare](../../../ado/reference/ado-api/find-method-ado.md) metodo per individuare una riga in un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md).|  
|**adHoldRecords**|0x100|È possibile recuperare più record o modifiche alla posizione successiva senza eseguire il commit di tutte le modifiche in sospeso.|  
|**adIndex**|0x100000|Supporta il [indice](../../../ado/reference/ado-api/index-property.md) proprietà per assegnare un nome di un indice.|  
|**adMovePrevious**|0x200|Supporta il [MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md) e [MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md) metodi, e [spostare](../../../ado/reference/ado-api/move-method-ado.md) oppure [GetRows](../../../ado/reference/ado-api/getrows-method-ado.md) i metodi per spostare il record corrente della posizione all'indietro senza richiedere i segnalibri.|  
|**adNotify**|0x40000|Indica che il provider di dati sottostante supporta le notifiche (che determina se **Recordset** gli eventi sono supportati).|  
|**adResync**|0x20000|Supporta il [Risincronizza](../../../ado/reference/ado-api/resync-method.md) metodo per aggiornare il cursore con i dati che sono visibili nel database sottostante.|  
|**adSeek**|0x200000|Supporta il [Seek](../../../ado/reference/ado-api/seek-method.md) metodo per individuare una riga in un **Recordset**.|  
|**adUpdate**|0x1008000|Supporta il [Update](../../../ado/reference/ado-api/update-method.md) metodo per modificare i dati esistenti.|  
|**adUpdateBatch**|0x10000|Supporta l'aggiornamento batch ([UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) e [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md) metodi) per trasmettere i gruppi delle modifiche apportate al provider.|  
  
## <a name="adowfc-equivalent"></a>Equivalente di ADO o WFC  
 Package: **com.ms.wfc.data**  
  
|Costante|  
|--------------|  
|AdoEnums.CursorOption.ADDNEW|  
|AdoEnums.CursorOption.APPROXPOSITION|  
|AdoEnums.CursorOption.BOOKMARK|  
|AdoEnums.CursorOption.DELETE|  
|AdoEnums.CursorOption.FIND|  
|AdoEnums.CursorOption.HOLDRECORDS|  
|AdoEnums.CursorOption.INDEX|  
|AdoEnums.CursorOption.MOVEPREVIOUS|  
|AdoEnums.CursorOption.NOTIFY|  
|AdoEnums.CursorOption.RESYNC|  
|AdoEnums.CursorOption.SEEK|  
|AdoEnums.CursorOption.UPDATE|  
|AdoEnums.CursorOption.UPDATEBATCH|  
  
## <a name="applies-to"></a>Si applica a  
 [Metodo Supports](../../../ado/reference/ado-api/supports-method.md)
