---
title: MSSQLSERVER_9003 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 9003 (Database Engine error)
ms.assetid: 7fdfb391-5c6f-428b-b434-6c3d0b30fd7b
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 33fc97759f43b58fdb7066ce6da957ea9311a491
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/21/2020
ms.locfileid: "86550756"
---
# <a name="mssqlserver_9003"></a>MSSQLSERVER_9003
    
## <a name="details"></a>Dettagli  
  
|Attributo|valore|  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|9003|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|LOG_INVALID_LSN|  
|Testo del messaggio|Il numero di analisi log %S_LSN passato alla funzione di analisi dei log nel database '%.*ls' non è valido. L'errore può indicare la presenza di dati danneggiati o un problema di mancata corrispondenza tra il file di log (con estensione ldf) e il file di dati (con estensione mdf). Se l'errore si è verificato durante la replica, ricreare la pubblicazione. Se invece il problema provoca un errore all'avvio, eseguire il ripristino da un backup.|  
  
## <a name="explanation"></a>Spiegazione  
 Un componente ha passato un numero di sequenza del file di log (LSN) non valido allo strumento di gestione del log per il database. L'errore potrebbe verificarsi durante la replica oppure in presenza di dati danneggiati o di incoerenza tra il file di dati primario e il log.  
  
## <a name="user-action"></a>Azione dell'utente  
 Se l'errore si è verificato durante la replica, ricreare la pubblicazione. In caso contrario, eseguire un ripristino dal backup.  
  
  
