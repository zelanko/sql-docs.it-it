---
title: Metodo AppendChunk (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Parameter::AppendChunk
- Field20::AppendChunk
helpviewer_keywords:
- AppendChunk method [ADO]
ms.assetid: c648b5a8-d4f1-4d16-836e-3957feb03617
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4ac0174a223571e29973ad854f9350a6e60f1de9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63248299"
---
# <a name="appendchunk-method-ado"></a>Metodo AppendChunk (ADO)
Accoda i dati a un testo di grandi dimensioni o dati binari [campo](../../../ado/reference/ado-api/field-object.md), o a un [parametro](../../../ado/reference/ado-api/parameter-object.md) oggetto.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
object.AppendChunk Data  
```  
  
#### <a name="parameters"></a>Parametri  
 *object*  
 Oggetto **campo** oppure **parametro** oggetto.  
  
 *Dati*  
 Oggetto **Variant** che contiene i dati da aggiungere all'oggetto.  
  
## <a name="remarks"></a>Note  
 Usare la **AppendChunk** metodo su un **campo** o **parametro** oggetto per inserirvi i dati caratteri o binari long. In situazioni in cui la memoria di sistema è limitata, è possibile usare la **AppendChunk** metodo per modificare i valori long in parti invece che nel loro complesso.  
  
## <a name="field"></a>Campo  
 Se il **adFldLong** bit nel [attributi](../../../ado/reference/ado-api/attributes-property-ado.md) proprietà di un **campo** è impostata su **true**, è possibile usare il  **Metodo AppendChunk** metodo per il campo.  
  
 Il primo **AppendChunk** chiamare su un **campo** oggetto scrive i dati e il campo, sovrascrivendo eventuali dati esistenti. Le successive **AppendChunk** chiamate aggiungono ai dati esistenti. Se si Accoda dati a un singolo campo e quindi impostare o leggere il valore di un altro campo nel record corrente, si presume che l'utente abbia terminato di accodamento dei dati nel primo campo. Se si chiama il **AppendChunk** metodo nel primo campo anche in questo caso, ADO interpreta la chiamata come nuovo **AppendChunk** operazione e sovrascrive i dati esistenti. L'accesso ai campi in altre [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) oggetti che non sono i cloni dei primi **Recordset** oggetto non interromperà **AppendChunk** operazioni.  
  
 Se è presente nessun record corrente quando si chiama **AppendChunk** in un **campo** dell'oggetto, si verifica un errore.  
  
> [!NOTE]
>  Il **AppendChunk** metodo non opera sui **campo** gli oggetti di un [oggetto Record (ADO)](../../../ado/reference/ado-api/record-object-ado.md) oggetto. Esegue alcuna operazione e produrrà un errore di run-time.  
  
## <a name="parameter"></a>Parametro  
 Se il **adParamLong** bit nel **attributi** proprietà di un **parametro** è impostata su **true**, è possibile usare il  **Metodo AppendChunk** metodo per il parametro.  
  
 Il primo **AppendChunk** chiamare su un **parametro** oggetto scrive i dati per il parametro, sovrascrivendo eventuali dati esistenti. Le successive **AppendChunk** chiama su una **parametro** oggetto aggiungere ai dati di parametro esistente. Un' **AppendChunk** chiamata che passa un valore null Elimina tutti i dati di parametro.  
  
## <a name="applies-to"></a>Si applica a  
  
|||  
|-|-|  
|[Oggetto Field](../../../ado/reference/ado-api/field-object.md)|[Oggetto Parameter](../../../ado/reference/ado-api/parameter-object.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di AppendChunk e GetChunk (esempio di metodi (VB)](../../../ado/reference/ado-api/appendchunk-and-getchunk-methods-example-vb.md)   
 [Esempio di AppendChunk e GetChunk esempio di metodi (VC + +)](../../../ado/reference/ado-api/appendchunk-and-getchunk-methods-example-vc.md)   
 [Proprietà di attributi (ADO)](../../../ado/reference/ado-api/attributes-property-ado.md)   
 [Metodo GetChunk (ADO)](../../../ado/reference/ado-api/getchunk-method-ado.md)
