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
manager: craigg
ms.openlocfilehash: 643bcfef67b1f3c5434d7beaac46da2d46bbdd14
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63225797"
---
# <a name="description-property-ado-md"></a>Proprietà Description (ADO MD)
Restituisce una spiegazione del testo dell'oggetto corrente.  
  
## <a name="return-values"></a>Valori restituiti  
 Restituisce un **stringa** ed è di sola lettura.  
  
## <a name="remarks"></a>Note  
 Per la [membro](../../../ado/reference/ado-md-api/member-object-ado-md.md) oggetti **descrizione** si applica solo ai membri di misure e formule. **Descrizione** restituisce una stringa vuota ("") per tutti gli altri tipi di membri. Per altre informazioni sui vari tipi di membri, vedere la [tipo](../../../ado/reference/ado-md-api/type-property-ado-md.md) proprietà.  
  
 Questa proprietà è supportata solo nei **membro** oggetti appartenenti a un [livello](../../../ado/reference/ado-md-api/level-object-ado-md.md) oggetto. Si verifica un errore quando questa proprietà viene fatto riferimento dal **membro** oggetti appartenenti a un [posizione](../../../ado/reference/ado-md-api/position-object-ado-md.md) oggetto.  
  
## <a name="applies-to"></a>Si applica a  
  
||||  
|-|-|-|  
|[Oggetto CubeDef (ADO MD)](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)|[Oggetto Dimension (ADO MD)](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)|[Oggetto Hierarchy (ADO MD)](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md)|  
|[Oggetto Level (ADO MD)](../../../ado/reference/ado-md-api/level-object-ado-md.md)|[Oggetto Member (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)||
