---
title: Categoria di eventi Transazioni | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- SQL Server event classes, Transactions event category
- event classes [SQL Server], Transactions event category
- Transactions event category [SQL Server]
ms.assetid: bfc75c5b-7115-49d8-9148-a0c84ee66a9a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 076e68de4dc5d4e25f6cabe6b39ac4a61a05033a
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52801103"
---
# <a name="transactions-event-category"></a>Categoria di eventi Transactions
  Le classi di eventi della categoria **Transactions** consentono di monitorare lo stato delle transazioni. I nomi delle classi di eventi con prefisso **TM:** sono utilizzati per tracciare le operazioni correlate alle transazioni che vengano inviate tramite l'interfaccia di gestione delle transazioni.  
  
## <a name="in-this-section"></a>In questa sezione  
  
|Argomento|Descrizione|  
|-----------|-----------------|  
|[Classe di evento DTCTransaction](dtctransaction-event-class.md)|Tiene traccia delle transazioni coordinate da [!INCLUDE[msCoName](../../includes/msconame-md.md)] Distributed Transaction Coordinator (MS DTC). Si tratta delle transazioni distribuite tra due o più database o istanze di [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].|  
|[Classe di evento SQLTransaction](sqltransaction-event-class.md)|Tiene traccia delle istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] BEGIN TRAN, COMMIT TRAN, SAVE TRAN e ROLLBACK TRAN.|  
|[TM: Begin Tran Completed-classe di evento](tm-begin-tran-completed-event-class.md)|Indica il completamento di una richiesta BEGIN TRANSACTION.|  
|[TM: Begin Tran Starting-classe di evento](tm-begin-tran-starting-event-class.md)|Indica l'avvio di una richiesta BEGIN TRANSACTION.|  
|[TM: Eseguire il commit Tran Completed-classe di evento](tm-commit-tran-completed-event-class.md)|Indica il completamento di una richiesta COMMIT TRANSACTION.|  
|[TM: Eseguire il commit Tran Starting-classe di evento](tm-commit-tran-starting-event-class.md)|Indica l'avvio di una richiesta COMMIT TRANSACTION.|  
|[TM: Promote Tran Completed-classe di evento](tm-promote-tran-completed-event-class.md)|Indica il completamento di una richiesta PROMOTE TRANSACTION.|  
|[TM: Promote Tran Starting-classe di evento](tm-promote-tran-starting-event-class.md)|Indica l'avvio di una richiesta PROMOTE TRANSACTION.|  
|[TM: Rollback Tran Completed-classe di evento](tm-rollback-tran-completed-event-class.md)|Indica il completamento di una richiesta ROLLBACK TRANSACTION.|  
|[TM: Eseguire il rollback Tran Starting-evento classe](tm-rollback-tran-starting-event-class.md)|Indica l'avvio di una richiesta ROLLBACK TRANSACTION.|  
|[TM: Salvataggio Tran Completed-classe di evento](tm-save-tran-completed-event-class.md)|Indica il completamento di una richiesta SAVE TRANSACTION.|  
|[TM: Save Tran Starting-classe di evento](tm-save-tran-starting-event-class.md)|Indica l'avvio di una richiesta SAVE TRANSACTION.|  
|[Classe di evento TransactionLog](transactionlog-event-class.md)|Traccia l'inserimento delle transazioni in un log delle transazioni di database.|  
  
  
