---
title: MSSQLSERVER_9001 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 9001 (Database Engine error)
ms.assetid: a54de936-90c6-4845-aa96-29d32f154601
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: cfc717c63cb85207315d00ae8dc06fdd881a503c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62912440"
---
# <a name="mssqlserver_9001"></a>MSSQLSERVER_9001
    
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
  
  
