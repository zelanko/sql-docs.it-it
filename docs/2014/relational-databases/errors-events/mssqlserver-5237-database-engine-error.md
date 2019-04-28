---
title: MSSQLSERVER_5237 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 5237 (Database Engine error)
ms.assetid: 9ff28935-d1eb-47ee-99b3-1a65cb948ce7
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: eabe36c423b1df3702b594137aca371a6075e327
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62867628"
---
# <a name="mssqlserver5237"></a>MSSQLSERVER_5237
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|5237|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|DBCC4_INDEXED_VIEW_CHECK_QUERY_FAILED_NO_ERRORCODE|  
|Testo del messaggio|Controllo DBCC per il set di righe non riuscito per l'oggetto 'NAME' (ID di oggetto O_ID) a causa di un errore interno della query.|  
  
## <a name="explanation"></a>Spiegazione  
Si è verificato un errore interno poiché DBCC non è in grado di eseguire la query per controllare viste indicizzate.  
  
## <a name="user-action"></a>Azione dell'utente  
Eseguire di nuovo il comando DBCC.  
  
