---
title: MSSQLSERVER_9001 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 9001 (Database Engine error)
ms.assetid: a54de936-90c6-4845-aa96-29d32f154601
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 22767609a0281cc21a38d51716661ac98a8ffc24
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "68118371"
---
# <a name="mssqlserver_9001"></a>MSSQLSERVER_9001
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|9001|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|LOG_NOT_AVAIL|  
|Testo del messaggio|Il log per il database '%.*ls' non è disponibile. Controllare il registro eventi per i messaggi di errore correlati. Risolvere eventuali errori e riavviare il database.|  
  
## <a name="explanation"></a>Spiegazione  
Il log del database è stato messo offline. In genere questa situazione implica un errore irreversibile per cui è necessario riavviare il database.  
  
## <a name="user-action"></a>Azione dell'utente  
Diagnosticare altri errori e riavviare l'istanza di SQL Server qualora il riavvio non sia già stato eseguito automaticamente.  
  
