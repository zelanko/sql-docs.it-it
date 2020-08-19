---
description: Metodo Create (ADOX)
title: Metodo Create (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Catalog::raw_Create
- _Catalog::Create
helpviewer_keywords:
- Create method [ADOX]
ms.assetid: 64f5c21c-b581-42d8-bdc7-c4f1bebaf105
author: rothja
ms.author: jroth
ms.openlocfilehash: b291651caa93e93999d87a926c9abe391e71d21e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88440213"
---
# <a name="create-method-adox"></a>Metodo Create (ADOX)
Crea un nuovo catalogo.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Catalog.Create ConnectString  
```  
  
#### <a name="parameters"></a>Parametri  
 *ConnectString*  
 Valore **stringa** utilizzato per la connessione all'origine dati.  
  
## <a name="remarks"></a>Osservazioni  
 Il metodo **create** crea e apre una nuova [connessione](../../../ado/reference/ado-api/connection-object-ado.md) ADO all'origine dati specificata in *ConnectString*. In caso di esito positivo, il nuovo oggetto **Connection** viene assegnato alla proprietà [ActiveConnection](../../../ado/reference/adox-api/activeconnection-property-adox.md) .  
  
 Se il provider non supporta la creazione di nuovi cataloghi, si verificherà un errore.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Catalog (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di metodo Create (VB)](../../../ado/reference/adox-api/create-method-example-vb.md)   
 [Proprietà ActiveConnection (ADOX)](../../../ado/reference/adox-api/activeconnection-property-adox.md)
