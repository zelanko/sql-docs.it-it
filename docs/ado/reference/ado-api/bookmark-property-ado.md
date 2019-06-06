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
manager: jroth
ms.openlocfilehash: bb835a84d83730e291afcfdf83910f9b520daea6
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66696297"
---
# <a name="bookmark-property-ado"></a>Proprietà Bookmark (ADO)
Indica un segnalibro che identifica in modo univoco il record corrente in un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) dell'oggetto o imposta il record corrente in un **Recordset** oggetto nel record identificato da un segnalibro valido.  
  
## <a name="settings-and-return-values"></a>Le impostazioni e valori restituiti  
 Imposta o restituisce un **Variant** espressione che restituisca un segnalibro valido.  
  
## <a name="remarks"></a>Note  
 Usare la **segnalibro** proprietà utilizzata per salvare la posizione del record corrente e tornare al record specifico in qualsiasi momento. I segnalibri sono disponibili solo negli **Recordset** gli oggetti che supportano la funzionalità corrispondente.  
  
 Quando si apre un **Recordset** dell'oggetto, ognuno dei relativi record contiene un segnalibro univoco. Per salvare il segnalibro per il record corrente, assegnare il valore dei **segnalibro** proprietà a una variabile. Per tornare rapidamente al record specifico in qualsiasi momento dopo il passaggio a un altro record, impostare il **Recordset** dell'oggetto **segnalibro** proprietà sul valore della variabile.  
  
 L'utente potrebbe non essere in grado di visualizzare il valore del segnalibro. Inoltre, gli utenti non possono prevedere segnalibri sia direttamente confrontabili, perché due segnalibri che fanno riferimento allo stesso record possono avere valori diversi.  
  
 Se si usa la [Clone](../../../ado/reference/ado-api/clone-method-ado.md) metodo per creare una copia di un **Recordset** oggetto, il **segnalibro** impostazioni delle proprietà per l'originale e il duplicato **Recordset**  oggetti sono identici e usarle in modo intercambiabile. Tuttavia, è possibile usare i segnalibri da diversi **Recordset** oggetti in modo intercambiabile, anche se sono stati creati dalla stessa origine o comando.  
  
> [!NOTE]
>  **Utilizzo del servizio dati remoto** quando viene usato in un client-side **Recordset** oggetto, il **segnalibro** proprietà è sempre disponibile.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Proprietà BOF, EOF e segnalibro (esempio di proprietà (VB)](../../../ado/reference/ado-api/bof-eof-and-bookmark-properties-example-vb.md)   
 [Proprietà BOF, EOF e segnalibro esempio di proprietà (VC + +)](../../../ado/reference/ado-api/bof-eof-and-bookmark-properties-example-vc.md)   
 [Metodo Supports](../../../ado/reference/ado-api/supports-method.md)
