---
title: Salvare i risultati della traccia in un file (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- saving traces
- traces [SQL Server], saving
ms.assetid: ac528747-0c19-4f3d-96f5-44c762a4abed
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 206ba778a5c131ac4f9260ed37de63b29de86820
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "63025676"
---
# <a name="save-trace-results-to-a-file-sql-server-profiler"></a>Salvare i risultati della traccia in un file (SQL Server Profiler)
  Nel presente argomento viene illustrata la procedura di salvataggio dei risultati della traccia in un file utilizzando [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].  
  
### <a name="to-save-trace-results-to-a-file"></a>Per salvare i risultati della traccia in un file  
  
1.  Scegliere **Nuova traccia** dal menu **File**e quindi connettersi a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
     Verrà visualizzata la finestra di dialogo **Proprietà traccia**.  
  
    > [!NOTE]  
    >  Se l'opzione **Avvia traccia non appena viene stabilita una connessione**è selezionata, la finestra di dialogo **Proprietà traccia**non viene visualizzata e viene invece avviata la traccia. Per disabilitare questa impostazione, scegliere **Opzioni**dal menu **Strumenti**e deselezionare la casella di controllo **Avvia traccia non appena viene stabilita una connessione** .  
  
2.  Nella casella **Nome traccia** digitare un nome per la traccia.  
  
3.  Selezionare la casella di controllo **Salva nel file** .  
  
     Verrà visualizzata la finestra di dialogo **Salva con nome**.  
  
4.  Specificare un percorso e un nome di file nella finestra di dialogo **Salva con nome**. Fare clic su **Salva**.  
  
    > [!NOTE]  
    >  Assicurarsi che il servizio SQL Server disponga delle autorizzazioni necessarie per la scrittura su un file nella directory specificata.  
  
5.  Nella finestra di dialogo **Proprietà traccia** digitare le dimensioni massime del file nella casella di testo **Dimensioni massime del file (MB)** . Il valore predefinito è 5 megabyte (MB).  
  
6.  Facoltativamente, specificare le opzioni seguenti:  
  
    -   Selezionare la casella di controllo **Consenti rollover dei file** per fare in modo che [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] crei nuovi file per i dati di traccia dopo aver raggiunto le dimensioni massime del file. Questa opzione è selezionata per impostazione predefinita.  
  
    -   Selezionare la casella di controllo **Dati di traccia elaborati dal server** per assicurare che il server registri ogni evento di traccia.  
  
        > [!NOTE]  
        >  Quando la casella di controllo **Dati di traccia elaborati dal server**deselezionata, il server non registra gli eventi se tale registrazione determina una significativa riduzione delle prestazioni.  
  
## <a name="see-also"></a>Vedere anche  
 [SQL Server Profiler](sql-server-profiler.md)  
  
  
