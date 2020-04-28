---
title: Proprietà Bookmark (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 03/20/2018
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::Bookmark
helpviewer_keywords:
- Bookmark property [ADO]
ms.assetid: 481dcc93-487b-490e-ac58-a1e9b2ebfd43
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 48b1c90b59b220841aa45f618fdfda5ff2db82da
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "67920344"
---
# <a name="bookmark-property-ado"></a>Proprietà Bookmark (ADO)
Indica un segnalibro che identifica in modo univoco il record corrente in un oggetto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) o imposta il record corrente in un oggetto **Recordset** sul record identificato da un segnalibro valido.  
  
## <a name="settings-and-return-values"></a>Impostazioni e valori restituiti  
 Imposta o restituisce un'espressione **Variant** che restituisce un segnalibro valido.  
  
## <a name="remarks"></a>Osservazioni  
 Usare la proprietà **Bookmark** per salvare la posizione del record corrente e tornare a tale record in qualsiasi momento. I segnalibri sono disponibili solo negli oggetti **Recordset** che supportano la funzionalità di segnalibro.  
  
 Quando si apre un oggetto **Recordset** , ognuno dei relativi record dispone di un segnalibro univoco. Per salvare il segnalibro per il record corrente, assegnare il valore della proprietà **Bookmark** a una variabile. Per tornare rapidamente a tale record in qualsiasi momento dopo il passaggio a un record diverso, impostare la proprietà **Bookmark** dell'oggetto **Recordset** sul valore di tale variabile.  
  
 L'utente potrebbe non essere in grado di visualizzare il valore del segnalibro. Inoltre, gli utenti non devono prevedere che i segnalibri siano direttamente confrontabili, perché due segnalibri che fanno riferimento allo stesso record possono avere valori diversi.  
  
 Se si usa il metodo [Clone](../../../ado/reference/ado-api/clone-method-ado.md) per creare una copia di un oggetto **Recordset** , le impostazioni delle proprietà del **segnalibro** per gli oggetti **Recordset** originali e duplicati sono identiche ed è possibile usarle in modo intercambiabile. Tuttavia, non è possibile usare i segnalibri di oggetti **Recordset** diversi in modo interscambiabile, anche se sono stati creati con lo stesso codice sorgente o lo stesso comando.  
  
> [!NOTE]
>  **Utilizzo servizio dati remoto** Se utilizzata su un oggetto **Recordset** sul lato client, la proprietà **Bookmark** è sempre disponibile.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di proprietà BOF, EOF e Bookmark (VB)](../../../ado/reference/ado-api/bof-eof-and-bookmark-properties-example-vb.md)   
 [Esempio di proprietà BOF, EOF e segnalibro (VC + +)](../../../ado/reference/ado-api/bof-eof-and-bookmark-properties-example-vc.md)   
 [Metodo Supports](../../../ado/reference/ado-api/supports-method.md)
