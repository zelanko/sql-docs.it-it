---
title: Specificare un filtro per un punto di interruzione | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.technology: scripting
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Transact-SQL debugger, breakpoint filter
ms.assetid: 7bf1dddd-7b0b-4c47-8a7b-28a5569b4fa5
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 23cead258b38f8b580d1331f69b7aa70483f41ce
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/16/2019
ms.locfileid: "68267704"
---
# <a name="specify-a-breakpoint-filter"></a>Impostazione di un filtro per un punto di interruzione
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  Un filtro per un punto di interruzione limita il punto di interruzione in modo che agisca solo su computer o processi e thread del sistema operativo specificati. I filtri per i punti di interruzione vengono in genere utilizzati per il debug di applicazioni parallele.  
  
##  <a name="BKMK_ActionConsiderations"></a> Considerazioni sui filtri  
 I filtri per i punti di interruzione non vengono in genere utilizzati con il debugger [!INCLUDE[tsql](../../includes/tsql-md.md)] perché gli script e le stored procedure [!INCLUDE[tsql](../../includes/tsql-md.md)] non sono applicazioni parallele.  
  
#### <a name="to-specify-a-breakpoint-filter"></a>Per specificare un filtro per un punto di interruzione  
  
1.  Nella finestra dell'editor fare clic con il pulsante destro del mouse sul glifo del punto di interruzione, quindi scegliere **Filtro** dal menu di scelta rapida.  
  
     oppure  
  
     Nella finestra **Punti di interruzione** fare clic con il pulsante destro del mouse sul glifo del punto di interruzione, quindi scegliere **Filtro** dal menu di scelta rapida.  
  
2.  Nella finestra di dialogo **Filtri punti di interruzione** usare la casella **Filtro** per specificare i computer per nome o i processi e i thread del sistema operativo per nome o numero ID:  
  
    -   **MachineName** è il computer che esegue l'istanza del motore di database.  
  
    -   **ProcessID**e **ProcessName** sono relativi al processo del sistema operativo che esegue l'istanza del motore di database.  
  
    -   **ThreadID** e **ThreadName** sono relativi al thread del sistema operativo che esegue il batch, la procedura o la funzione [!INCLUDE[tsql](../../includes/tsql-md.md)] nell'istanza del motore di database.  
  
3.  Fare clic su **OK** per implementare le modifiche o su **Annulla** per uscire senza applicare le modifiche.  
  
## <a name="see-also"></a>Vedere anche  
 [Impostare una condizione del punto di interruzione](../../relational-databases/scripting/specify-a-breakpoint-condition.md)   
 [Specifica di un numero di passaggi](../../relational-databases/scripting/specify-a-hit-count.md)   
 [Impostazione di un'azione del punto di interruzione](../../relational-databases/scripting/specify-a-breakpoint-action.md)  
