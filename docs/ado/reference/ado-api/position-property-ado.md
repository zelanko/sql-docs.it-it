---
title: Proprietà Position (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::Position
helpviewer_keywords:
- Position property [ADO]
ms.assetid: daa8319a-49aa-4c1c-9af6-0b01e9ab2f9d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: dba8636f07b88f1c05d465b844376c6ef3e61240
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67931650"
---
# <a name="position-property-ado"></a>Proprietà Position (ADO)
Indica la posizione corrente all'interno di un oggetto [flusso](../../../ado/reference/ado-api/stream-object-ado.md) .  
  
## <a name="settings-and-return-values"></a>Impostazioni e valori restituiti  
 Imposta o restituisce un valore **Long** che specifica l'offset, espresso in numero di byte, della posizione corrente a partire dall'inizio del flusso. Il valore predefinito è 0, che rappresenta il primo byte nel flusso.  
  
## <a name="remarks"></a>Osservazioni  
 La posizione corrente può essere spostata in un punto successivo alla fine del flusso. Se si specifica la posizione corrente oltre la fine del flusso, le [dimensioni](../../../ado/reference/ado-api/size-property-ado-stream.md) dell'oggetto **flusso** verranno aumentate di conseguenza. Eventuali nuovi byte aggiunti in questo modo saranno null.  
  
> [!NOTE]
>  **Position** misura sempre i byte. Per i flussi di testo che utilizzano set di caratteri multibyte, moltiplicare la posizione per la dimensione del carattere per determinare il numero di caratteri. Per un set di caratteri a due byte, ad esempio, il primo carattere è nella posizione 0, il secondo carattere nella posizione 2, il terzo carattere nella posizione 4 e così via.  
  
> [!NOTE]
>  Non è possibile usare valori negativi per modificare la posizione corrente in un **flusso**. Per la **posizione**è possibile utilizzare solo numeri positivi.  
  
> [!NOTE]
>  Per gli oggetti di **flusso** di sola lettura, ADO non restituirà un errore se la **posizione** è impostata su un valore maggiore della **dimensione** del **flusso**. Questa operazione non modifica le dimensioni del **flusso**o modifica in alcun modo il contenuto del **flusso** . Questa operazione, tuttavia, deve essere evitata perché comporta un valore di **posizione**non significativo.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Proprietà Charset (ADO)](../../../ado/reference/ado-api/charset-property-ado.md)
