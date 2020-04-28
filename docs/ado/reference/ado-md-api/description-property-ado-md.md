---
title: Proprietà Description (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Member::Description
- Level::Description
- CubeDef::Description
- Hierarchy::Description
- Description
- Dimension::Description
helpviewer_keywords:
- Description property [ADO MD]
ms.assetid: 6d626d35-0bf3-4f24-9934-ad9c9c91273a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5636b5f4e49ff9a5bbe46937a8d7b972e61b4502
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "67938570"
---
# <a name="description-property-ado-md"></a>Proprietà Description (ADO MD)
Restituisce una spiegazione del testo dell'oggetto corrente.  
  
## <a name="return-values"></a>Valori restituiti  
 Restituisce una **stringa** ed è di sola lettura.  
  
## <a name="remarks"></a>Osservazioni  
 Per gli oggetti [membro](../../../ado/reference/ado-md-api/member-object-ado-md.md) , la **Descrizione** si applica solo ai membri delle formule e delle misure. **Description** restituisce una stringa vuota ("") per tutti gli altri tipi di membri. Per ulteriori informazioni sui vari tipi di membri, vedere la proprietà [Type](../../../ado/reference/ado-md-api/type-property-ado-md.md) .  
  
 Questa proprietà è supportata solo su oggetti **membro** che appartengono a un oggetto [Level](../../../ado/reference/ado-md-api/level-object-ado-md.md) . Si verifica un errore quando si fa riferimento a questa proprietà dagli oggetti **membro** che appartengono a un oggetto [position](../../../ado/reference/ado-md-api/position-object-ado-md.md) .  
  
## <a name="applies-to"></a>Si applica a  
  
||||  
|-|-|-|  
|[Oggetto CubeDef (ADO MD)](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)|[Oggetto Dimension (ADO MD)](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)|[Oggetto Hierarchy (ADO MD)](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md)|  
|[Oggetto Level (ADO MD)](../../../ado/reference/ado-md-api/level-object-ado-md.md)|[Oggetto Member (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)||
