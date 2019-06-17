---
title: Rimuovere le chiamate al comando DBCC CONCURRENCYVIOLATION deprecato | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 2cc9f6ff-de36-4e94-bd04-59f5c45c4911
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0110d4bc138ad0da953eb83d3c81ec265d2fd3ba
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66093211"
---
# <a name="remove-calls-to-the-deprecated-dbcc-concurrencyviolation-command"></a>Rimuovere le chiamate al comando DBCC CONCURRENCYVIOLATION deprecato
  È stato rilevato il comando DBCC CONCURRENCYVIOLATION. Questo comando non è più disponibile. L'esecuzione di questo comando restituisce l'errore 2526.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Descrizione  
 Nessuna versione recente dell'edizione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] include un'utilità di Governor del carico di lavoro; pertanto il comando è stato rimosso.  
  
## <a name="corrective-action"></a>Azione correttiva  
 Aggiornare le applicazioni e gli script per rimuovere i riferimenti a questo comando deprecato.  
  
## <a name="external-resources"></a>Risorse esterne  
  
