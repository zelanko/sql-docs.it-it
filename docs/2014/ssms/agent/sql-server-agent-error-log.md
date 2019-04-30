---
title: Log degli errori di SQL Server Agent | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- logs [SQL Server], SQL Server Agent
- messages [SQL Server], SQL Server Agent
- errors [SQL Server], logs
- SQL Server Agent, errors
ms.assetid: 0b2d6e6e-cd2d-4b8b-9fa2-2bbd2fc0da41
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1dfa6926d86fce5006e458b3738a28a8b5f467d0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63267387"
---
# <a name="sql-server-agent-error-log"></a>Log degli errori di SQL Server Agent
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent crea un log degli errori nel quale vengono registrati avvisi ed errori per impostazione predefinita. Nel log vengono visualizzati gli avvisi e gli errori seguenti:  
  
-   Messaggi di avviso che segnalano potenziali problemi, ad esempio "Il processo \<*nome_processo*> è stato eliminato mentre era in esecuzione".  
  
-   Messaggi di errore che richiedono in genere l'intervento dell'amministratore di sistema, quali "Impossibile avviare la sessione di posta elettronica". I messaggi di errore possono essere trasmessi a un utente o un computer specifico con **net send**.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gestisce fino a nove registri errori di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. A ogni log degli errori archiviato viene assegnata un'estensione che indica la posizione cronologica del log stesso. Ad esempio l'estensione 1 indica il log degli errori più recente e l'estensione 9 indica il log degli errori meno recente.  
  
 Per impostazione predefinita, i messaggi di traccia dell'esecuzione non vengono scritti nel log degli errori di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent in quanto potrebbero occuparlo interamente, rendendo complicata la selezione e la consultazione di messaggi di errore più gravi. Poiché il log incrementa il carico di elaborazione del server, è importante valutare attentamente la rilevanza dell'acquisizione di messaggi di traccia dell'esecuzione nel log degli errori. In genere l'acquisizione di tutti i messaggi è opportuna soltanto durante il debug di un problema specifico.  
  
 Quando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent non è in esecuzione, è possibile modificare la posizione del log degli errori di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Quando il log degli errori è vuoto, non sarà possibile aprirlo. È possibile scorrere il log di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent in qualunque momento, senza arrestare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
 **Per visualizzare il log degli errori di SQL Server Agent**  
  
-   [Visualizzare il log degli errori di SQL Server Agent &#40;SQL Server Management Studio&#41;](view-sql-server-agent-error-log-sql-server-management-studio.md) 
  
 **Per rinominare un log degli errori di SQL Server Agent**  
  
-   [Rinominare un log degli errori di SQL Server Agent &#40;SQL Server Management Studio&#41;](rename-a-sql-server-agent-error-log-sql-server-management-studio.md)  
  
 **Per inviare messaggi di errore di SQL Server Agent**  
  
-   [Send SQL Server Agent Error Messages](send-sql-server-agent-error-messages.md)  
  
 **Per scrivere messaggi di traccia esecuzione nel log degli errori di SQL Server Agent**  
  
-   [Scrivere messaggi di traccia esecuzione nel log degli errori di SQL Server Agent &#40;SQL Server Management Studio&#41;](write-execution-trace-messages-to-sql-server-agent-log-ssms.md)  
  
  
