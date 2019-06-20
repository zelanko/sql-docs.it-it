---
title: Modificare la forma di nome proprietà dinamica (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Reshape Name property [ADO]
ms.assetid: 690229d1-46cc-42e6-a57d-4438251fe248
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: f9b8898a3cc75cf47ae783a1dd2a120c8954ab8f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66711660"
---
# <a name="reshape-name-property-dynamic-ado"></a>Proprietà dinamica Reshape Name (ADO)
Specifica un nome per il [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) oggetto.  
  
## <a name="return-values"></a>Valori restituiti  
 Restituisce un **stringa** valore che rappresenta il nome del **Recordset**.  
  
## <a name="remarks"></a>Note  
 I nomi di rendere persistente per la durata della connessione o finché il **Recordset** viene chiuso.  
  
 Il **Reshape Name** proprietà è progettata principalmente per l'uso con la funzionalità di data shaping nuovamente le [Microsoft Data shaping per OLE DB](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) provider di servizi. I nomi devono essere univoci per partecipare rivoluzionando.  
  
 Questa proprietà è di sola lettura, ma può essere impostata indirettamente quando un **Recordset** viene creato. Ad esempio, se una clausola di un comando Shape crea un **Recordset** e gli assegna un nome di alias utilizzando il **AS** (parola chiave), l'alias viene assegnato al **Reshape Name** proprietà. Se non viene dichiarato alcun alias, il **Reshape Name** proprietà viene assegnato un nome univoco generato dal servizio di data shaping. Se il nome di alias è identico al nome di un oggetto esistente **Recordset**, né **Recordset** possono essere ridefinite fino a quando non uno di essi viene rilasciato. Il comportamento predefinito può essere modificato impostando un nome univoco [Reshape Name](../../../ado/reference/ado-api/reshape-name-property-dynamic-ado.md) proprietà sulla connessione ADO **True**. Impostazione di questa proprietà fornisce i dati di data shaping di autorizzazione del servizio per modificare il nome utente assegnato, se necessario, per garantire l'univocità. Per altre informazioni sulla modifica della forma, vedere [Microsoft Data shaping per OLE DB (ADO Service Provider)](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md).  
  
 Usare la **Reshape Name** proprietà quando si desidera fare riferimento a un **Recordset** in un comando Shape, o quando non si conosce il nome perché è stato generato dal servizio di Data Shaping. In tal caso, è possibile generare un comando SHAPE concatenando il la stringa restituita dal comando il **Reshape Name** proprietà.  
  
 **Proprietà dinamica Reshape Name** viene aggiunta una proprietà dinamica per il **Recordset** dell'oggetto [delle proprietà](../../../ado/reference/ado-api/properties-collection-ado.md) raccolta quando la [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) è impostata su **adUseClient**.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Microsoft Data Shaping Service per OLE DB (ADO Service Provider)](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)   
 [Comandi Shape in generale](../../../ado/guide/data/shape-commands-in-general.md)   
 [Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
