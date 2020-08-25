---
description: Proprietà Type (ADO MD)
title: Proprietà Type (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Member::Type
- Type
helpviewer_keywords:
- Type property [ADO MD]
ms.assetid: 34698910-64b9-41d8-8531-9de12f2b1e32
author: rothja
ms.author: jroth
ms.openlocfilehash: 30cf3c161e30884d370aea0fefd81260bafe141e
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/24/2020
ms.locfileid: "88777820"
---
# <a name="type-property-ado-md"></a>Proprietà Type (ADO MD)
Indica il tipo del [membro](./member-object-ado-md.md)corrente.  
  
## <a name="return-values"></a>Valori restituiti  
 Restituisce un valore [MemberTypeEnum](./membertypeenum.md) ed è di sola lettura.  
  
## <a name="remarks"></a>Commenti  
 Questa proprietà è supportata solo per gli oggetti [membro](./member-object-ado-md.md) che appartengono a un oggetto [Level](./level-object-ado-md.md) . Si verifica un errore quando si fa riferimento a questa proprietà dagli oggetti **membro** che appartengono a un oggetto [position](./position-object-ado-md.md) .  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Member (ADO MD)](./member-object-ado-md.md)