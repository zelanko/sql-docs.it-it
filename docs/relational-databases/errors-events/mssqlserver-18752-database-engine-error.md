---
title: MSSQLSERVER_18752 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 18752 (Database Engine error)
ms.assetid: 234c58d8-7a1e-4b07-a64b-32a311527980
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 8aa5f3a75c4d21e148d50fe71b75a21a287a2a2b
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "68137043"
---
# <a name="mssqlserver_18752"></a>MSSQLSERVER_18752
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|18752|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|REPL_INUSE|  
|Testo del messaggio|A un database può connettersi un solo agente di lettura log o una sola procedura correlata ai log (sp_repldone, sp_replcmds e sp_replshowcmds) alla volta. Se è stata eseguita una procedura correlata ai log, eliminare la connessione utilizzata per eseguire la procedura oppure eseguire sp_replflush tramite tale connessione prima di avviare l'agente di lettura log o di eseguire un'altra procedura relativa ai log.|  
  
## <a name="explanation"></a>Spiegazione  
A un database può connettersi solo un agente di lettura log o una sola procedura correlata ai log alla volta.  
  
## <a name="user-action"></a>Azione dell'utente  
Verificare che non sia in esecuzione alcun altro agente di lettura log per lo stesso database di pubblicazione e che in nessuna connessione attiva sia stata eseguita in precedenza sp_replcmds, sp_repltrans o sp_repldone senza la successiva esecuzione di sp_replflush o senza disconnessione.  
  
