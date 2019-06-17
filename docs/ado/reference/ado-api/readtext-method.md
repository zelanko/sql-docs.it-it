---
title: Metodo ReadText | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::raw_ReadText
- _Stream::ReadText
helpviewer_keywords:
- ReadText method [ADO]
ms.assetid: be5a409e-cf87-4859-9ea5-713401755a77
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 5e7f9a484ecb873a141f9b91a88c64f65ff25336
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66712211"
---
# <a name="readtext-method"></a>Metodo ReadText
Legge un numero di caratteri da un testo specificato [Stream](../../../ado/reference/ado-api/stream-object-ado.md) oggetto.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
String = Stream.ReadText ( NumChars)  
```  
  
#### <a name="parameters"></a>Parametri  
 *NumChars*  
 Facoltativo. Oggetto **lungo** valore che specifica il numero di caratteri da leggere dal file o una [StreamReadEnum](../../../ado/reference/ado-api/streamreadenum.md) valore. Il valore predefinito è **adReadAll**.  
  
## <a name="return-value"></a>Valore restituito  
 Il **ReadText** metodo legge un numero specificato di caratteri, un'intera riga o dell'intero flusso da un **Stream** specificato e restituisce la stringa risultante.  
  
## <a name="remarks"></a>Note  
 Se *NumChar* è maggiore del numero di caratteri rimanenti nel flusso, vengono restituiti solo i caratteri rimanenti. La stringa letta non possono essere riempita per corrispondere alla lunghezza specificata da *NumChar*. Se sono presenti caratteri rimanenti per la lettura, viene restituito un valore variant il cui valore è null. **ReadText** non può essere usato per leggere le versioni precedenti.  
  
> [!NOTE]
>  Il **ReadText** metodo viene utilizzato con i flussi di testo ([tipo](../../../ado/reference/ado-api/type-property-ado-stream.md) viene **adTypeText**). Per i flussi binari (**tipo** viene **adTypeBinary**), utilizzare [lettura](../../../ado/reference/ado-api/read-method.md).  
  
 Le query che generano una grande quantità di dati XML restituiti tramite il **ReadText** metodo dell'oggetto Stream dei dati oggetto ADO (ActiveX) può richiedere una notevole quantità di tempo da eseguire; se questa operazione viene eseguita in un componente COM+ da cui viene richiamato un Pagina ASP, la sessione dell'utente potrebbe verificarsi un timeout. ADO converte i dati oggetto Stream dalla codifica UTF-8 in Unicode; la riallocazione di memoria frequente coinvolto nella conversione di una grande quantità di dati in una sola volta è piuttosto che richiedono molto tempo. Per risolvere, effettuare chiamate ripetute al **ReadText** metodo ADO oggetto command e specificare un numero inferiore di caratteri. I test hanno dimostrato che un valore equivalente a 128 KB (131.072) è ottimale. Tempo di risposta diminuisce quando questo valore è ridotto. Per altre informazioni, vedere l'articolo della Knowledge Base 280067, "PRB: Recupero di documenti XML molto grandi da SQL Server 2000 tramite il metodo ReadText dell'oggetto ADO flusso potrebbe essere lento", nella Microsoft Knowledge Base al https://support.microsoft.com.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Metodo Read](../../../ado/reference/ado-api/read-method.md)
