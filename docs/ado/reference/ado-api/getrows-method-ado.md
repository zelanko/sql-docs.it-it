---
title: Esempio di metodo GetRows (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::GetRows
- Recordset15::raw_GetRows
helpviewer_keywords:
- Getrows method [ADO]
ms.assetid: 14b92860-4171-47d9-a413-dd60dd6a8880
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d96b7968c7aba8d1249db2f43b53fc8a22596419
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67918457"
---
# <a name="getrows-method-ado"></a>Metodo GetRows (ADO)
Recupera i record più di una [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) oggetto in una matrice.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
array = recordset.GetRows(Rows, Start, Fields )  
```  
  
## <a name="return-value"></a>Valore restituito  
 Restituisce un **Variant** il cui valore è una matrice bidimensionale.  
  
#### <a name="parameters"></a>Parametri  
 *Righe*  
 facoltativo. Oggetto [GetRowsOptionEnum](../../../ado/reference/ado-api/getrowsoptionenum.md) valore che indica il numero di record da recuperare. Il valore predefinito è **adGetRowsRest**.  
  
 *Start*  
 facoltativo. Oggetto **stringa** valore oppure **Variant** che restituisca il segnalibro per il record da cui il **GetRows** deve iniziare l'operazione. È anche possibile usare una [BookmarkEnum](../../../ado/reference/ado-api/bookmarkenum.md) valore.  
  
 *Fields*  
 facoltativo. Oggetto **Variant** che rappresenta un nome di campo singolo o posizione ordinale o una matrice di nomi di campo o i numeri di posizione ordinale. ADO restituisce solo i dati in questi campi.  
  
## <a name="remarks"></a>Note  
 Usare la **GetRows** metodo per copiare i record da un **Recordset** in una matrice bidimensionale. Il primo indice identifica il campo e il secondo il numero di record. Il *matrice* variabile automaticamente viene dimensionata correttamente le dimensioni quando il **GetRows** metodo restituisce i dati.  
  
 Se non si specifica un valore per il *righe* argomento, il **GetRows** metodo recupera automaticamente tutti i record il **Recordset** oggetto. Se si richiedono più record rispetto a quelle disponibili, **GetRows** restituisce solo il numero di record disponibili.  
  
 Se il **Recordset** oggetto supporta i segnalibri, è possibile specificare al record che le **GetRows** metodo deve iniziare il recupero di dati passando il valore di tale record [segnalibro](../../../ado/reference/ado-api/bookmark-property-ado.md)proprietà di *avviare* argomento.  
  
 Se si desidera limitare i campi che la **GetRows** chiamata viene restituito, è possibile passare un singolo campo nome/numero o una matrice di nomi o numeri nel *campi* argomento.  
  
 Dopo aver chiamato **GetRows**, il record successivo da leggere diventa il record corrente, o il [EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) viene impostata su **True** se sono presenti più record.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di metodo GetRows (VB)](../../../ado/reference/ado-api/getrows-method-example-vb.md)   
 [Esempio di metodo GetRows (VC++)](../../../ado/reference/ado-api/getrows-method-example-vc.md)   
