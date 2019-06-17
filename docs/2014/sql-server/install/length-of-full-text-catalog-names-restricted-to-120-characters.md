---
title: Lunghezza dei nomi di catalogo full-text è limitata a 120 caratteri | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- full-text catalogs names
ms.assetid: 50633373-83f6-4ed9-99b9-71f92479a14f
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5cce05426fdff2aacf40612738ad80b07d9ec0e2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66094055"
---
# <a name="length-of-full-text-catalog-names-restricted-to-120-characters"></a>La lunghezza dei nomi di catalogo full-text è limitata a 120 caratteri
  La lunghezza dei nomi di catalogo full-text è limitata a 120 caratteri, rispetto a 128 caratteri nelle versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="description"></a>Descrizione  
 Questa modifica non influisce sui nomi di catalogo esistenti. Tuttavia, gli script che creano cataloghi full-text con nomi più lunghi di 120 caratteri generano un errore. I nomi del catalogo vengono utilizzati per generare nomi di file logici che corrispondono a cataloghi.  
  
## <a name="corrective-action"></a>Azione correttiva  
 Modificare tutti gli script che creano cataloghi full-text per assicurarsi che la lunghezza dei nomi di catalogo sia limitata a 120 caratteri.  
  
## <a name="see-also"></a>Vedere anche  
 [Uso di Preparazione aggiornamento](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
