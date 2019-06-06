---
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: bbdd7f6b663fb1c6c2ee12b7a6e4c843eb16d42d
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66703358"
---
# <a name="create-method-adox"></a>Metodo Create (ADOX)
Crea un nuovo catalogo.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Catalog.Create ConnectString  
```  
  
#### <a name="parameters"></a>Parametri  
 *ConnectString*  
 Oggetto **stringa** valore utilizzato per la connessione all'origine dati.  
  
## <a name="remarks"></a>Note  
 Il **Create** metodo crea e apre un nuovo file ADO [connessione](../../../ado/reference/ado-api/connection-object-ado.md) all'origine dati specificato in *ConnectString*. Se l'operazione riesce, il nuovo **Connection** oggetto viene assegnato alle [ActiveConnection](../../../ado/reference/adox-api/activeconnection-property-adox.md) proprietà.  
  
 Se il provider non supporta la creazione di nuovi cataloghi, si verificherà un errore.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Catalog (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio del metodo Create (VB)](../../../ado/reference/adox-api/create-method-example-vb.md)   
 [Proprietà ActiveConnection (ADOX)](../../../ado/reference/adox-api/activeconnection-property-adox.md)
