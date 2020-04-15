---
title: Operazioni della libreria di cursori Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC cursor library [ODBC], backward compatibility
- compatibility [ODBC], cursor library
- upgrading applications [ODBC], cursor library
- application upgrades [ODBC], cursor library
- backward compatibility [ODBC], cursor library
- cursor library [ODBC], backward compatibility
ms.assetid: 04d514b1-dc4d-4b84-bf35-60f4657ef1f6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a2297e72aacad7ea91b7af934a47bebbc61f0686
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301618"
---
# <a name="cursor-library-operations"></a>Operazioni della libreria di cursori
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di utilizzare questa funzionalità nelle nuove attività di sviluppo e pianificare la modifica delle applicazioni che attualmente utilizzano questa funzionalità. Microsoft consiglia di utilizzare la funzionalità del cursore del driver.  
  
 Se un'applicazione che utilizza un driver ODBC *2.x* effettua chiamate alla libreria di cursori ODBC *3.x,* l'applicazione potrebbe essere in grado di utilizzare le funzionalità di ODBC *3.x* che non sono supportate dal driver ODBC *2.x.* Un writer di applicazioni deve prestare attenzione a come vengono utilizzate queste funzionalità, tuttavia. L'utilizzo della libreria di cursori ODBC *3.x* non trasforma un driver ODBC *2.x* in un driver ODBC *3.x.*
