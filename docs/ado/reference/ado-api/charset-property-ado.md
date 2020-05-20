---
title: Proprietà CharSet (ADO) | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: a5750364a745cda43459ecba69ba42cbf6f3da40
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/04/2020
ms.locfileid: "82763142"
---
# <a name="charset-property-ado"></a>Proprietà Charset (ADO)
Indica il set di caratteri in cui il contenuto di un [flusso](../../../ado/reference/ado-api/stream-object-ado.md) di testo deve essere convertito per l'archiviazione nel buffer interno dell'oggetto **flusso** .  
  
## <a name="settings-and-return-values"></a>Impostazioni e valori restituiti  
 Imposta o restituisce un valore **stringa** che specifica il set di caratteri in cui verrà convertito il contenuto del **flusso** . Il valore predefinito è **Unicode**. I valori consentiti sono stringhe tipiche passate sull'interfaccia come nomi dei set di caratteri Internet (ad esempio, "ISO-8859-1", "Windows-1252" e così via). Per un elenco dei nomi dei set di caratteri noti da un sistema, vedere le sottochiavi di HKEY_CLASSES_ROOT \MIME\Database\Charset nel registro di sistema di Windows.  
  
## <a name="remarks"></a>Osservazioni  
 In un oggetto **flusso** di testo, i dati di testo vengono archiviati nel set di caratteri specificato dalla proprietà **CharSet** . Il valore predefinito è Unicode. La proprietà **CharSet** viene utilizzata per convertire i dati in ingresso nel **flusso** o in uscita dal **flusso**. Se, ad esempio, il **flusso** contiene dati ISO-8859-1 e i dati vengono copiati in un BSTR, l'oggetto **flusso** convertirà i dati in formato Unicode. È anche vero il contrario.  
  
 Per un **flusso**aperto, la [posizione](../../../ado/reference/ado-api/position-property-ado.md) corrente deve trovarsi all'inizio del **flusso** (0) per poter impostare il set di **caratteri**.  
  
 Il **set di caratteri** viene usato solo con gli oggetti del **flusso** di testo (il[tipo](../../../ado/reference/ado-api/type-property-ado-stream.md) è **adTypeText**). Questa proprietà viene ignorata se il **tipo** è **adTypeBinary**.  
  
 Per un esempio di codice, vedere [passaggio 4: popolare la casella di testo Dettagli](../../../ado/guide/data/step-4-populate-the-details-text-box.md).  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
