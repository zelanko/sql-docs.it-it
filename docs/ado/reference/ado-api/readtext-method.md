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
ms.openlocfilehash: d6c174d2e6a659a3b9da8f89816b5bdf90342416
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67917377"
---
# <a name="readtext-method"></a>Metodo ReadText
Legge il numero specificato di caratteri da un oggetto [flusso](../../../ado/reference/ado-api/stream-object-ado.md) di testo.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
String = Stream.ReadText ( NumChars)  
```  
  
#### <a name="parameters"></a>Parametri  
 *NumChars*  
 Facoltativa. Valore **Long** che specifica il numero di caratteri da leggere dal file o un valore [StreamReadEnum](../../../ado/reference/ado-api/streamreadenum.md) . Il valore predefinito è **adReadAll**.  
  
## <a name="return-value"></a>Valore restituito  
 Il metodo **READTEXT** legge un numero specificato di caratteri, un'intera riga o l'intero flusso da un oggetto **flusso** e restituisce la stringa risultante.  
  
## <a name="remarks"></a>Osservazioni  
 Se *NumChar* è maggiore del numero di caratteri rimanenti nel flusso, vengono restituiti solo i caratteri rimanenti. La stringa letta non viene riempita in modo da corrispondere alla lunghezza specificata da *NumChar*. Se non sono presenti caratteri da leggere, viene restituita una variante il cui valore è null. Non è possibile usare **READTEXT** per leggere le versioni precedenti.  
  
> [!NOTE]
>  Il metodo **READTEXT** viene usato con i flussi di testo (il[tipo](../../../ado/reference/ado-api/type-property-ado-stream.md) è **adTypeText**). Per i flussi binari (**tipo** è **adTypeBinary**), usare [Read](../../../ado/reference/ado-api/read-method.md).  
  
 L'esecuzione di query che comportano la restituzione di una grande quantità di dati XML tramite il metodo **READTEXT** dell'oggetto flusso ADO (ActiveX Data Object) può richiedere molto tempo. Se questa operazione viene eseguita in un componente COM+ richiamato da una pagina ASP, è possibile che si verifichi il timeout della sessione dell'utente. ADO converte i dati degli oggetti flusso dalla codifica UTF-8 a Unicode; la riallocazione di memoria frequente per la conversione di una quantità elevata di dati contemporaneamente è molto dispendiosa in termini di tempo. Per risolvere il tentativo, effettuare chiamate ripetute al metodo **READTEXT** dell'oggetto comando ADO e specificare un numero minore di caratteri. I test hanno dimostrato che un valore equivalente a 128 KB (131.072) è ottimale. Il tempo di risposta diminuisce perché questo valore viene ridotto. Per ulteriori informazioni, vedere l'articolo della Knowledge base 280067, "PRB: il recupero di documenti XML di grandi dimensioni da SQL Server 2000 tramite il metodo ReadText dell'oggetto flusso ADO potrebbe essere lento" nella Microsoft Knowledge https://support.microsoft.combase all'indirizzo.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Metodo Read](../../../ado/reference/ado-api/read-method.md)
