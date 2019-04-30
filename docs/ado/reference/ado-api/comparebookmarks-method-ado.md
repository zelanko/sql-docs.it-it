---
title: Esempio di metodo CompareBookmarks (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- CompareBookmarks
- Recordset20::CompareBookmarks
- Recordset20::raw_CompareBookmarks
helpviewer_keywords:
- CompareBookmarks method [ADO]
ms.assetid: d0b64286-2cc4-4a22-8f1d-9aefeebbcbc6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 85ca76678c0d3e75a106164626c4e3c3a81bd7e9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63315983"
---
# <a name="comparebookmarks-method-ado"></a>Metodo CompareBookmarks (ADO)
Confronta due segnalibri e restituisce un'indicazione dei relativi valori.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
result = recordset.CompareBookmarks(Bookmark1, Bookmark2)  
```  
  
## <a name="return-value"></a>Valore restituito  
 Restituisce un [CompareEnum](../../../ado/reference/ado-api/compareenum.md) valore che indica la posizione della riga relativo di due record rappresentati dai relativi segnalibri.  
  
#### <a name="parameters"></a>Parametri  
 *Bookmark1*  
 Il segnalibro della prima riga.  
  
 *Bookmark2*  
 Il segnalibro della seconda riga.  
  
## <a name="remarks"></a>Note  
 I segnalibri è necessario applicare allo stesso [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) oggetto, o una **Recordset** oggetto e il relativo [clone](../../../ado/reference/ado-api/clone-method-ado.md). Non è possibile confrontare in modo affidabile i segnalibri da diversi **Recordset** oggetti, anche se sono stati creati dalla stessa origine o comando. Né è possibile confrontare i segnalibri per una **Recordset** oggetto a cui provider sottostante non supporta i confronti.  
  
 Segnalibro che identifica in modo univoco una riga in una **Recordset** oggetto. Usare la [segnalibro](../../../ado/reference/ado-api/bookmark-property-ado.md) proprietà della riga corrente per ottenere il segnalibro.  
  
 Poiché il tipo di dati di un segnalibro è specifico per ogni provider, ADO lo espone come un **Variant**. Ad esempio, i segnalibri di SQL Server sono di tipo DBTYPE_R8 (**doppie**). ADO esporrà questo tipo come un **Variant** con un sottotipo **doppie**.  
  
 Quando si confrontano i segnalibri, ADO non tenta di coercizione qualsiasi tipo. I valori vengono semplicemente passati al provider in cui si verifica il confronto. Se i segnalibri passato per il **CompareBookmarks** metodo vengono archiviati in variabili di tipi diversi, può generare l'errore di mancata corrispondenza di tipo seguente: "Gli argomenti sono di tipo errato, sono compreso nell'intervallo accettabile o sono in conflitto".  
  
 Segnalibro che non è valida o formato non corretto verrà generato un errore.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di metodo CompareBookmarks (VB)](../../../ado/reference/ado-api/comparebookmarks-method-example-vb.md)   
 [Esempio di metodo CompareBookmarks (VC + +)](../../../ado/reference/ado-api/comparebookmarks-method-example-vc.md)   
 [Proprietà Bookmark (ADO)](../../../ado/reference/ado-api/bookmark-property-ado.md)
