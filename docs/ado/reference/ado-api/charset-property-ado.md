---
title: Proprietà Charset (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::Charset
helpviewer_keywords:
- Charset property [ADO]
ms.assetid: e42507cb-9b46-4ce4-8191-2948eaf14ca2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 20fff124f33bfeccaec665c74687753e2c0af20b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63239747"
---
# <a name="charset-property-ado"></a>Proprietà Charset (ADO)
Indica il set di caratteri in cui il contenuto del testo di una [Stream](../../../ado/reference/ado-api/stream-object-ado.md) deve essere tradotto per la memorizzazione nel buffer interno delle **Stream** oggetto.  
  
## <a name="settings-and-return-values"></a>Le impostazioni e valori restituiti  
 Imposta o restituisce un **stringa** valore che specifica il carattere è impostato in cui il contenuto delle **Stream** verrà convertito. Il valore predefinito è **Unicode**. I valori consentiti sono tipici stringhe passate attraverso l'interfaccia come nomi di set di caratteri di Internet (ad esempio, "iso-8859-1", "Windows-1252" e così via). Per un elenco di set di nomi di caratteri che notoriamente da un sistema, vedere le sottochiavi HKEY_CLASSES_ROOT\MIME\Database\Charset nel Registro di sistema Windows.  
  
## <a name="remarks"></a>Note  
 In un testo **Stream** dell'oggetto, dati di testo viene archiviati nel set di caratteri specificato per il **Charset** proprietà. Il valore predefinito è Unicode. Il **Charset** proprietà viene utilizzata per la conversione di dati verso il **Stream** o prossimi fuori il **Stream**. Ad esempio, se il **Stream** contiene i dati di ISO-8859-1 e che i dati vengono copiati in un BSTR, il **Stream** oggetto convertirà i dati in formato Unicode. È anche vero il contrario.  
  
 Per un oggetto aperto **Stream**, corrente [posizione](../../../ado/reference/ado-api/position-property-ado.md) deve essere all'inizio del **Stream** (0) per poter impostare **Charset**.  
  
 **Set di caratteri** viene usato solo con il testo **Stream** oggetti ([tipo](../../../ado/reference/ado-api/type-property-ado-stream.md) viene **adTypeText**). Questa proprietà viene ignorata se **tipo** viene **adTypeBinary**.  
  
 Per un esempio di codice, vedere [passaggio 4: Popolare la casella di testo dettagli](../../../ado/guide/data/step-4-populate-the-details-text-box.md).  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
