---
title: Proprietà CursorLocation (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::CursorLocation
- Recordset15::CursorLocation
helpviewer_keywords:
- CursorLocation property [ADO]
ms.assetid: 39c8d86e-7ee9-4182-be5e-aad5ce952f84
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3860434236f5a0751ddb857c6b8bce1cf54d19ac
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63308686"
---
# <a name="cursorlocation-property-ado"></a>Proprietà CursorLocation (ADO)
Indica la posizione del servizio di cursore.  
  
## <a name="settings-and-return-values"></a>Le impostazioni e valori restituiti  
 Imposta o restituisce un **lungo** valore che può essere impostato su uno delle [CursorLocationEnum](../../../ado/reference/ado-api/cursorlocationenum.md) valori.  
  
## <a name="remarks"></a>Note  
 Questa proprietà consente di scegliere tra diverse librerie di cursore accessibile al provider. In genere, è possibile scegliere tra l'uso di una libreria di cursori sul lato client o uno che si trova nel server.  
  
 Impostazione di questa proprietà influisce sulle connessioni stabilite solo dopo aver impostata la proprietà. Modifica il **CursorLocation** proprietà non ha alcun effetto sulle connessioni esistenti.  
  
 Cursori restituiti per il [Execute](../../../ado/reference/ado-api/execute-method-ado-connection.md) metodo erediteranno questa impostazione. **Recordset** oggetti erediterà automaticamente questa impostazione dalle connessioni associate.  
  
 Questa proprietà è di lettura/scrittura in un [Connection](../../../ado/reference/ado-api/connection-object-ado.md) o un chiuso [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)e sola lettura su un elemento aperto **Recordset**.  
  
> [!NOTE]
>  **Utilizzo del servizio dati remoto** quando viene usato in un client-side **Recordset** oppure **connessione** oggetto, il **CursorLocation** proprietà può essere impostata solo su **adUseClient**.  
  
## <a name="applies-to"></a>Si applica a  
  
|||  
|-|-|  
|[Oggetto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)|[Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Appendice a: Providers](../../../ado/guide/appendixes/appendix-a-providers.md)
