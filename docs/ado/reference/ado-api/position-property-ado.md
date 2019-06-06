---
title: Posiziona proprietà (ADO) | Microsoft Docs
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
manager: jroth
ms.openlocfilehash: 7b777179ad83250d9707f7717b5833bbbff4fec7
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66703408"
---
# <a name="position-property-ado"></a>Proprietà Position (ADO)
Indica la posizione corrente all'interno di un [Stream](../../../ado/reference/ado-api/stream-object-ado.md) oggetto.  
  
## <a name="settings-and-return-values"></a>Le impostazioni e valori restituiti  
 Imposta o restituisce un **lungo** valore che specifica l'offset, in numero di byte, della posizione corrente dall'inizio del flusso. Il valore predefinito è 0, che rappresenta il primo byte nel flusso.  
  
## <a name="remarks"></a>Note  
 La posizione corrente può essere spostata in un punto dopo la fine del flusso. Se si specifica la posizione corrente oltre la fine del flusso, il [dimensioni](../../../ado/reference/ado-api/size-property-ado-stream.md) delle **Stream** oggetto verrà aumentato di conseguenza. I byte di nuovo aggiunti in questo modo sarà null.  
  
> [!NOTE]
>  **Posizione** misura sempre i byte. Per i flussi di testo con set di caratteri multibyte, moltiplicare la posizione per la dimensione dei caratteri per determinare il numero di caratteri. Ad esempio, per un set di caratteri a due byte, il primo carattere è nella posizione 0, il secondo carattere nella posizione 2, il terzo carattere nella posizione 4 e così via.  
  
> [!NOTE]
>  Impossibile utilizzare valori negativi per modificare la posizione corrente in un **Stream**. Sono utilizzabile solo numeri positivi per **posizione**.  
  
> [!NOTE]
>  Per sola lettura **Stream** oggetti, ADO non restituirà un errore se **posizione** è impostato su un valore maggiore di **dimensioni** del **Stream**. Ciò non modifica le dimensioni dei **Stream**, o si modifica il **Stream** contenuto in alcun modo. Tuttavia, in questo modo deve essere evitato perché comporta un significativo **posizione**valore.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Proprietà Charset (ADO)](../../../ado/reference/ado-api/charset-property-ado.md)
