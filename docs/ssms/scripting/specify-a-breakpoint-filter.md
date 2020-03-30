---
title: Impostazione di un filtro per un punto di interruzione
titleSuffix: T-SQL debugger
ms.prod: sql
ms.technology: scripting
ms.topic: conceptual
helpviewer_keywords:
- Transact-SQL debugger, breakpoint filter
ms.assetid: 7bf1dddd-7b0b-4c47-8a7b-28a5569b4fa5
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 12/04/2019
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 070a7ab77a025c2949888582947c805f13710198
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "75253632"
---
# <a name="specify-a-breakpoint-filter"></a>Impostazione di un filtro per un punto di interruzione

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Un filtro per un punto di interruzione limita il punto di interruzione in modo che agisca solo su computer o processi e thread del sistema operativo specificati. I filtri per i punti di interruzione vengono in genere utilizzati per il debug di applicazioni parallele.

[!INCLUDE[ssms-old-versions](../../includes/ssms-old-versions.md)]
  
##  <a name="filter-considerations"></a><a name="BKMK_ActionConsiderations"></a> Considerazioni sui filtri

I filtri per i punti di interruzione non vengono in genere utilizzati con il debugger [!INCLUDE[tsql](../../includes/tsql-md.md)] perché gli script e le stored procedure [!INCLUDE[tsql](../../includes/tsql-md.md)] non sono applicazioni parallele.  
  
#### <a name="to-specify-a-breakpoint-filter"></a>Per specificare un filtro per un punto di interruzione  
  
1.  Nella finestra dell'editor fare clic con il pulsante destro del mouse sul glifo del punto di interruzione, quindi scegliere **Filtro** dal menu di scelta rapida.  
  
     -oppure-  
  
     Nella finestra **Punti di interruzione** fare clic con il pulsante destro del mouse sul glifo del punto di interruzione, quindi scegliere **Filtro** dal menu di scelta rapida.  
  
2.  Nella finestra di dialogo **Filtri punti di interruzione** usare la casella **Filtro** per specificare i computer per nome o i processi e i thread del sistema operativo per nome o numero ID:  
  
    -   **MachineName** è il computer che esegue l'istanza del motore di database.  
  
    -   **ProcessID**e **ProcessName** sono relativi al processo del sistema operativo che esegue l'istanza del motore di database.  
  
    -   **ThreadID** e **ThreadName** sono relativi al thread del sistema operativo che esegue il batch, la procedura o la funzione [!INCLUDE[tsql](../../includes/tsql-md.md)] nell'istanza del motore di database.  
  
3.  Fare clic su **OK** per implementare le modifiche o su **Annulla** per uscire senza applicare le modifiche.  
  
## <a name="see-also"></a>Vedere anche  
 [Impostare una condizione del punto di interruzione](../../relational-databases/scripting/specify-a-breakpoint-condition.md)   
 [Specifica di un numero di passaggi](../../relational-databases/scripting/specify-a-hit-count.md)   
 [Specificare un'azione del punto di interruzione](../../relational-databases/scripting/specify-a-breakpoint-action.md)  
