---
description: Oggetto Group (ADOX)
title: Oggetto Group (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Group
helpviewer_keywords:
- group object [ADOX]
ms.assetid: 55ef0ade-68ea-4da5-8aa5-4cd27d1f6d1e
author: rothja
ms.author: jroth
ms.openlocfilehash: 21514bbcbe91e1320a4a2806e545d5f7b40df8d3
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2020
ms.locfileid: "88984432"
---
# <a name="group-object-adox"></a>Oggetto Group (ADOX)
Rappresenta un account di gruppo che dispone di autorizzazioni di accesso all'interno di un database protetto.  
  
## <a name="remarks"></a>Osservazioni  
 La raccolta di [gruppi](./groups-collection-adox.md) di un [Catalogo](./catalog-object-adox.md) rappresenta tutti gli account di gruppo del catalogo. La raccolta **gruppi** per un [utente](./user-object-adox.md) rappresenta solo il gruppo a cui appartiene l'utente.  
  
 Con le proprietà, le raccolte e i metodi di un oggetto **gruppo** , è possibile:  
  
-   Identificare il gruppo con la proprietà [Name](./name-property-adox.md) .  
  
-   Determinare se un gruppo dispone di autorizzazioni di lettura, scrittura o eliminazione con i metodi [GetPermissions](./getpermissions-method-adox.md) e [sepermissions](./setpermissions-method-adox.md) .  
  
-   Accedere agli account utente che dispongono di appartenenze al gruppo con la raccolta [Users](./users-collection-adox.md) .  
  
-   Accedere alle proprietà specifiche del provider con la raccolta [Properties](../ado-api/properties-collection-ado.md) .  
  
 Questa sezione contiene l'argomento seguente.  
  
-   [Proprietà, metodi ed eventi dell'oggetto Group](./group-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Raccolta Groups (ADOX)](./groups-collection-adox.md)   
 [Raccolta Users (ADOX)](./users-collection-adox.md)