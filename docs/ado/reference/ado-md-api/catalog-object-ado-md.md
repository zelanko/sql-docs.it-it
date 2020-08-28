---
description: Oggetto Catalog (ADO MD)
title: Oggetto Catalog (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Catalog
helpviewer_keywords:
- Catalog object [ADO MD]
ms.assetid: 11f6f896-d69c-44a4-94cd-d54c93140e4a
author: rothja
ms.author: jroth
ms.openlocfilehash: 0e62b4eedd835cff2d5bd99e054648339ffd9bc0
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2020
ms.locfileid: "88987302"
---
# <a name="catalog-object-ado-md"></a>Oggetto Catalog (ADO MD)
Contiene informazioni di schema multidimensionali, ovvero cubi e dimensioni sottostanti, gerarchie, livelli e membri, specifiche di un provider di dati multidimensionali (MDP).  
  
## <a name="remarks"></a>Osservazioni  
 Con le raccolte e le proprietà di un oggetto **Catalogo** , è possibile eseguire le operazioni seguenti:  
  
-   Aprire il catalogo impostando la proprietà [ActiveConnection](./activeconnection-property-ado-md.md) su un oggetto [connessione](../ado-api/connection-object-ado.md) ADO standard o su una stringa di connessione valida.  
  
-   Identificare il **Catalogo** con la proprietà [Name](./name-property-ado-md.md) .  
  
-   Scorrere i cubi in un catalogo usando la raccolta [CubeDefs](./cubedefs-collection-ado-md.md) .  
  
 Questa sezione contiene l'argomento seguente.  
  
-   [Proprietà, metodi ed eventi](./catalog-object-properties-methods-and-events-ado-md.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di catalogo (VB)](./catalog-example-vb.md)   
 [Oggetto Connection (ADO)](../ado-api/connection-object-ado.md)   
 [Raccolta CubeDefs (ADO MD)](./cubedefs-collection-ado-md.md)