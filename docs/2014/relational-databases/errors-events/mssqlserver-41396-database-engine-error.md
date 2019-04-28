---
title: MSSQLSERVER_41396 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 41396 (Database Engine error)
ms.assetid: 4ff04042-8367-46f3-8a16-c94682d6eedb
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f66a0ce65a0d16099d7371c003a813b129b3859f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62867875"
---
# <a name="mssqlserver41396"></a>MSSQLSERVER_41396
    
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|ID evento|41396|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|MAX_SORT_ROWS_EXCEEDED|  
|Testo del messaggio|L'operazione di ordinamento ha superato il limite del buffer. L'esecuzione della stored procedure è stata interrotta. Per ulteriori informazioni, vedere la documentazione online di SQL Server.|  
  
## <a name="explanation"></a>Spiegazione  
 Le stored procedure compilate in modo nativo eseguono le operazioni di ordinamento in memoria. Esiste un limite di dimensioni nel buffer di ordinamento. Questo errore indica che la dimensione del buffer di ordinamento supera questo limite. L'esecuzione della stored procedure e dell'operazione di ordinamento è stata interrotta.  
  
 Le dimensioni di ciascuna riga o voce nel buffer di ordinamento sono determinate dal numero di righe ordinate nonché dal numero di join e dal numero di funzioni di aggregazioni nella query. Attraverso la semplificazione della query è possibile ridurre le dimensioni di ciascuna riga permettendo così di adattare un numero maggiore di righe nel buffer di ordinamento. Le dimensioni delle righe nelle tabelle di base non influiscono sulle dimensioni di ciascuna riga o voce nel buffer di ordinamento.  
  
## <a name="user-action"></a>Azione dell'utente  
 Selezionare alcune righe o ridurre la complessità della query rimuovendo i join o le funzioni di aggregazione.  
  
## <a name="see-also"></a>Vedere anche  
 [OLTP in memoria &#40;ottimizzazione per la memoria&#41;](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
