---
description: Proprietà MarshalOptions (ADO)
title: Proprietà MarshalOptions (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::MarshalOptions
helpviewer_keywords:
- MarshalOptions property [ADO]
ms.assetid: 390c8abf-133e-40da-8b99-8f748a983e4f
author: rothja
ms.author: jroth
ms.openlocfilehash: 2e7e574836f09df6f3bb8fdb078661c85cbf6355
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2020
ms.locfileid: "88990672"
---
# <a name="marshaloptions-property-ado"></a>Proprietà MarshalOptions (ADO)
Indica i record del [Recordset](./recordset-object-ado.md) di cui eseguire il marshalling nel server.  
  
## <a name="settings-and-return-values"></a>Impostazioni e valori restituiti  
 Imposta o restituisce un valore [MarshalOptionsEnum](./marshaloptionsenum.md) . Il valore predefinito è **adMarshalAll**.  
  
## <a name="remarks"></a>Osservazioni  
 Quando si usa un [Recordset](./recordset-object-ado.md)lato client, i record modificati sul client vengono riscritti al livello intermedio o al server Web tramite una tecnica chiamata marshalling, il processo di creazione di pacchetti e invio di parametri del metodo di interfaccia tra i limiti del thread o del processo. L'impostazione della proprietà **MarshalOptions** può migliorare le prestazioni quando viene effettuato il marshalling dei dati remoti modificati per eseguire l'aggiornamento al livello intermedio o al server Web.  
  
> [!NOTE]
>  **Utilizzo servizio dati remoto** Questa proprietà viene utilizzata solo in un **Recordset**lato client.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Recordset (ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di proprietà MarshalOptions (VB)](./marshaloptions-property-example-vb.md)   
 [Esempio della proprietà MarshalOptions (VC++)](./marshaloptions-property-example-vc.md)