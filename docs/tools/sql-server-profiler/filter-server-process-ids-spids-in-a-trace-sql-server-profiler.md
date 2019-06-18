---
title: Filtrare gli ID del processo server (SPID) in una traccia (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- filters [SQL Server], traces
- filters [SQL Server], SPIDs
- traces [SQL Server], filters
ms.assetid: f5945c39-be6b-4632-91cb-92066c80e188
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5262d9a261e1fa9cb6cb0950f8509253d7eaced5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62712514"
---
# <a name="filter-server-process-ids-spids-in-a-trace-sql-server-profiler"></a>Filtrare gli ID del processo server (SPID) in una traccia (SQL Server Profiler)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  In questo argomento viene descritta la procedura per il filtraggio degli identificatori del processo server (SPID) in una traccia mediante [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].  
  
### <a name="to-filter-system-ids-in-a-trace"></a>Per filtrare gli ID di sistema in una traccia  
  
1.  Scegliere **Nuova traccia** dal menu **File**e quindi connettersi a un'istanza di SQL Server.  
  
     Verrà visualizzata la finestra di dialogo **Proprietà traccia** .  
  
    > [!NOTE]  
    >  Se l'opzione **Avvia traccia non appena viene stabilita una connessione** è selezionata, la finestra di dialogo **Proprietà traccia** non viene visualizzata e viene invece avviata la traccia. Per disattivare questa impostazione, scegliere **Opzioni** dal menu **Strumenti** e deselezionare la casella di controllo **Avvia traccia non appena viene stabilita una connessione**.  
  
2.  Nella casella **Nome traccia** digitare un nome per la traccia.  
  
3.  Nell'elenco di nomi **Modello** selezionare un modello di traccia.  
  
4.  Facoltativamente, è possibile specificare un file o una tabella di destinazione in cui salvare i risultati della traccia.  
  
5.  Nella scheda **Selezione eventi** fare clic sull'intestazione di colonna **SPID** per visualizzare la finestra di dialogo **Modifica filtro**. È anche possibile fare clic con il pulsante destro del mouse sull'intestazione di colonna e scegliere **Modifica filtro colonne**. Se non viene visualizzata la colonna **SPID** , selezionare la casella **Mostra tutte le colonne** .  
  
6.  Nella finestra di dialogo **Modifica filtro** espandere l'operatore di confronto appropriato e immettere uno SPID come valore di confronto.  
  
## <a name="see-also"></a>Vedere anche  
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
