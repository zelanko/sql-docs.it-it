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
manager: craigg
ms.openlocfilehash: b095e034df987fd580b5f5855993c9cf070a1236
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63278604"
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
