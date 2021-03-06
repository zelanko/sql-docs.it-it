---
description: Proprietà Provider (ADO)
title: Proprietà provider (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::get_Provider
- Connection15::PutProvider
- Connection15::put_Provider
- Connection15::GetProvider
- Connection15::Provider
helpviewer_keywords:
- Provider property [ADO]
ms.assetid: 0ff70e72-0061-4ffc-90fb-e3ea23129bb2
author: rothja
ms.author: jroth
ms.openlocfilehash: 4c3f45e8652568bd0440121e27ee6ee0c116e676
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2020
ms.locfileid: "88989912"
---
# <a name="provider-property-ado"></a>Proprietà Provider (ADO)
Indica il nome del provider per un oggetto [Connection](./connection-object-ado.md) .  
  
## <a name="settings-and-return-values"></a>Impostazioni e valori restituiti  
 Imposta o restituisce un valore **stringa** che indica il nome del provider.  
  
## <a name="remarks"></a>Osservazioni  
 Utilizzare la proprietà **provider** per impostare o restituire il nome del provider per una connessione. Questa proprietà può essere impostata anche dal contenuto della proprietà [ConnectionString](./connectionstring-property-ado.md) o dell'argomento *ConnectionString* del metodo [Open](./open-method-ado-connection.md) . Tuttavia, la specifica di un provider in più di una posizione durante la chiamata del metodo **Open** può avere risultati imprevedibili. Se non viene specificato alcun provider, per impostazione predefinita la proprietà verrà impostata su MSDASQL ([provider Microsoft OLE DB per ODBC](../../guide/appendixes/microsoft-ole-db-provider-for-odbc.md)).  
  
 La proprietà del **provider** è in lettura/scrittura quando la connessione è chiusa e in sola lettura quando è aperta. L'impostazione non ha effetto fino a quando non si apre l'oggetto **connessione** o si accede alla raccolta [Properties](./properties-collection-ado.md) dell'oggetto **Connection** . Se l'impostazione non è valida, si verifica un errore.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Connection (ADO)](./connection-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di proprietà provider e DefaultDatabase (VB)](./provider-and-defaultdatabase-properties-example-vb.md)   
 [Esempio di proprietà provider e DefaultDatabase (VB)](./provider-and-defaultdatabase-properties-example-vb.md)   
 [Provider OLE DB Microsoft per ODBC](../../guide/appendixes/microsoft-ole-db-provider-for-odbc.md)   
 [Appendice A: Provider](../../guide/appendixes/appendix-a-providers.md)