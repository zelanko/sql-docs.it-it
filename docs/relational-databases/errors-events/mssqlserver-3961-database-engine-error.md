---
title: MSSQLSERVER_3961 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 3961 (Database Engine error)
ms.assetid: 3bbc6965-6445-400c-940a-2d85b037513f
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 9b89aab7a129aec5fcae840086b140f6975a8c99
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68043513"
---
# <a name="mssqlserver3961"></a>MSSQLSERVER_3961
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|3961|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|XACT_METADATA_INVALID|  
|Testo del messaggio|Transazione di isolamento snapshot non riuscita nel database '%. * ls' perché l'oggetto a cui accede l'istruzione è stato modificato da un'istruzione DDL in un'altra transazione simultanea fin dall'inizio di questa transazione.  Operazione non consentita perché il controllo della versione non viene applicato ai metadati. Un aggiornamento simultaneo nei metadati può provocare un'inconsistenza se si utilizza anche l'isolamento snapshot.|  
  
## <a name="explanation"></a>Spiegazione  
Questo errore può verificarsi se si esegue una query nei metadati sotto isolamento snapshot e c'è un'istruzione DDL simultanea che aggiorna i metadati a cui si accede sotto isolamento dello snapshot. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non supporta il controllo delle versioni dei metadati. Per questo motivo, esistono limitazioni sulle operazioni DDL che è possibile eseguire in una transazione esplicita che viene eseguita con l'isolamento dello snapshot. Per definizione, una transazione implicita è una sola istruzione che rende possibile l'applicazione della semantica dell'isolamento dello snapshot, anche con le istruzioni DDL. Le istruzioni DDL seguenti non sono consentite con l'isolamento snapshot dopo un'istruzione BEGIN TRANSACTION: ALTER TABLE, CREATE INDEX, CREATE XML INDEX, ALTER INDEX, DROP INDEX, DBCC REINDEX, ALTER PARTITION FUNCTION, ALTER PARTITION SCHEME o qualsiasi istruzione DDL di Common Language Runtime (CLR). Queste istruzioni sono permesse quando viene utilizzato l'isolamento dello snapshot all'interno di transazioni implicite. Per definizione, una transazione implicita è una sola istruzione che rende possibile l'applicazione della semantica dell'isolamento dello snapshot, anche con le istruzioni DDL.  
  
## <a name="user-action"></a>Azione dell'utente  
Spostare il livello di isolamento dello snapshot su un livello di isolamento non snapshot ad esempio Read committed prima di eseguire una query sui metadati.  
  
