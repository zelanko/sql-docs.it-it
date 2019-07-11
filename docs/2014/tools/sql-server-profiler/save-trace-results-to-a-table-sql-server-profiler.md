---
title: Salvare i risultati della traccia in una tabella (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- saving traces
- traces [SQL Server], saving
ms.assetid: edbecf74-683b-4e43-a1ef-7a3d5f5e27f6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8571f7273cc2667040ffffc8ffbfb0df4e2a6ef6
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2019
ms.locfileid: "67792692"
---
# <a name="save-trace-results-to-a-table-sql-server-profiler"></a>Salvare i risultati della traccia in una tabella (SQL Server Profiler)
  In questo argomento viene descritta la procedura per salvare i risultati della traccia in una tabella di database mediante [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].  
  
### <a name="to-save-trace-results-to-a-table"></a>Per salvare i risultati della traccia in una tabella  
  
1.  Scegliere **Nuova traccia** dal menu **File**e quindi connettersi a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
     Verrà visualizzata la finestra di dialogo **Proprietà traccia**.  
  
    > [!NOTE]  
    >  Se l'opzione **Avvia traccia non appena viene stabilita una connessione**è selezionata, la finestra di dialogo **Proprietà traccia**non viene visualizzata e viene invece avviata la traccia. Per disabilitare questa impostazione, scegliere **Opzioni**dal menu **Strumenti**e deselezionare la casella di controllo **Avvia traccia non appena viene stabilita una connessione** .  
  
2.  Nella casella **Nome traccia** digitare il nome della traccia e quindi fare clic su **Salva nella tabella**.  
  
3.  Nella finestra di dialogo **Connetti al server** connettersi al database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che conterrà la tabella di traccia.  
  
4.  Nella finestra di dialogo **Tabella di destinazione** selezionare un database dall'elenco **Database**.  
  
5.  Nell'elenco **Proprietario** selezionare il proprietario della traccia.  
  
6.  Nell'elenco **Tabella** digitare o selezionare il nome della tabella per i risultati della traccia. Fare clic su **OK**.  
  
7.  Nel **proprietà traccia** finestra di dialogo, seleziona la **numero massimo di righe (in migliaia)** casella di controllo per specificare il numero massimo di righe da salvare.  
  
## <a name="see-also"></a>Vedere anche  
 [SQL Server Profiler](sql-server-profiler.md)  
  
  
