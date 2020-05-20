---
title: Proprietà del nome di modifica della forma-dinamica (ADO) | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 490a69a022c2098de1dc4ade67af484b6e50131a
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/04/2020
ms.locfileid: "82756503"
---
# <a name="reshape-name-property-dynamic-ado"></a>Proprietà dinamica Reshape Name (ADO)
Specifica un nome per l'oggetto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) .  
  
## <a name="return-values"></a>Valori restituiti  
 Restituisce un valore **stringa** che rappresenta il nome del **Recordset**.  
  
## <a name="remarks"></a>Osservazioni  
 I nomi vengono mantenuti per la durata della connessione o fino alla chiusura del **Recordset** .  
  
 La proprietà **nome nuova forma** è destinata principalmente all'uso con la funzionalità di rimodellazione del [servizio data shaping Microsoft per OLE DB](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) provider di servizi. I nomi devono essere univoci per partecipare alla ridefinizione.  
  
 Questa proprietà è di sola lettura, ma può essere impostata indirettamente quando viene creato un **Recordset** . Se, ad esempio, una clausola di un comando Shape crea un **Recordset** e lo assegna un nome di alias tramite la parola chiave **As** , l'alias viene assegnato alla proprietà **Reformate Name** . Se non viene dichiarato alcun alias, alla proprietà **nome riforma** viene assegnato un nome univoco generato dal servizio Data Shaping. Se il nome dell'alias corrisponde al nome di un **Recordset**esistente, non è possibile modificare la forma del **Recordset** fino a quando non viene rilasciato uno di essi. Il comportamento predefinito può essere modificato impostando un nome univoco nella proprietà modifica [nome](../../../ado/reference/ado-api/reshape-name-property-dynamic-ado.md) della connessione ADO su **true**. L'impostazione di questa proprietà consente all'autorizzazione del servizio Data Shaping di modificare il nome assegnato dall'utente, se necessario, per garantire l'univocità. Per ulteriori informazioni sul ridimensionamento, vedere [Microsoft Data Shaping Service per OLE DB (provider di servizi ADO)](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md).  
  
 Utilizzare la proprietà **riforma nome** quando si desidera fare riferimento a un **Recordset** in un comando Shape o quando non si conosce il nome perché è stato generato dal servizio Data Shaping. In tal caso, è possibile generare un comando SHAPE concatenando il comando intorno alla stringa restituita dalla proprietà **Reformate Name** .  
  
 Il **nome della riforma** è una proprietà dinamica aggiunta alla raccolta [Properties](../../../ado/reference/ado-api/properties-collection-ado.md) dell'oggetto **Recordset** quando la proprietà [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) è impostata su **adUseClient**.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Servizio Data Shaping Microsoft per OLE DB (provider di servizi ADO)](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)   
 [Comandi per la forma in generale](../../../ado/guide/data/shape-commands-in-general.md)   
 [Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
