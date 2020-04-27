---
title: Opzioni della riga di comando dello strumento di amministrazione (utilità Riesecuzione distribuita) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
ms.assetid: c01b0ed3-67e4-4561-92d2-a8fbb086aca8
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f53c456832e89aa96c0f7c9a1decd9fabbe96360
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "63151586"
---
# <a name="administration-tool-command-line-options-distributed-replay-utility"></a>Opzioni della riga di comando dello strumento di amministrazione (Distributed Replay Utility)
  Lo [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] strumento di amministrazione riesecuzione distribuita `DReplay.exe`,, è uno strumento da riga di comando che è possibile utilizzare per comunicare con il controller di riesecuzione distribuita. Usare lo strumento di amministrazione per avviare, monitorare e annullare operazioni nel controller.  
  
 ![Icona di collegamento all'argomento](../../database-engine/media/topic-link.gif "Icona di collegamento a un argomento") Per altre informazioni sulle convenzioni relative alla sintassi dello strumento di amministrazione, vedere [Convenzioni della sintassi Transact-SQL &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/transact-sql-syntax-conventions-transact-sql).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
      dreplay {preprocess|replay|status|cancel} [options] [-?]}  
  
Usage:  
  
  dreplay preprocess [-mcontroller] -iinput_trace_file  
    -dcontroller_working_dir [-cconfig_file] [-fstatus_interval]  
  
  dreplay replay [-mcontroller] -dcontroller_working_dir [-o]  
    [-starget_server] -wclients [-cconfig_file]  
    [-fstatus_interval]  
  
  dreplay status [-mcontroller] [-fstatus_interval]  
  
  dreplay cancel [-mcontroller] [-q]   
```  
  
## <a name="remarks"></a>Osservazioni  
 È possibile eseguire le seguenti opzioni della riga di comando con `DReplay.exe`:  
  
 **preprocess**  
 Avvia la fase di pre-elaborazione. Il controller prepara i dati di traccia di input, acquisiti dall'ambiente di produzione, per la riproduzione sul server di destinazione.  
  
 **replay**  
 Avvia la fase di riproduzione dell'evento. Il controller recapita i dati di riproduzione ai client specificati, avvia la riproduzione distribuita e sincronizza i client. Ogni client selezionato può eventualmente registrare l'attività di riproduzione e salvare in locale i file di traccia dei risultati.  
  
 **Stato**  
 Viene eseguita una query sul controller e viene visualizzato lo stato corrente.  
  
 **cancel**  
 Viene annullata l'operazione corrente eseguita nel controller.  
  
 Per informazioni dettagliate sulla sintassi, inclusi gli argomenti dei comandi e gli esempi, vedere gli argomenti seguenti:  
  
-   [Opzione preprocess &#40;strumento di amministrazione Distributed Replay&#41;](preprocess-option-distributed-replay-administration-tool.md)  
  
-   [Opzione replay &#40;strumento di amministrazione Distributed Replay&#41;](replay-option-distributed-replay-administration-tool.md)  
  
-   [Opzione status &#40;strumento di amministrazione Distributed Replay&#41;](status-option-distributed-replay-administration-tool.md)  
  
-   [Opzione cancel &#40;strumento di amministrazione Distributed Replay&#41;](cancel-option-distributed-replay-administration-tool.md)  
  
 Le chiamate RPC vengono riprodotte come RPC e non come eventi di linguaggio.  
  
## <a name="permissions"></a>Autorizzazioni  
 È necessario eseguire lo strumento di amministrazione come utente interattivo, scegliendo tra utente locale e account utente di dominio. Per utilizzare un account utente locale, lo strumento di amministrazione e il controller devono essere eseguiti nello stesso computer.  
  
 Per altre informazioni, vedere [Sicurezza di Distributed Replay](distributed-replay-security.md).  
  
## <a name="see-also"></a>Vedi anche  
 [SQL Server Distributed Replay](sql-server-distributed-replay.md)  
  
  
