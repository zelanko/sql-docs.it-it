---
title: MSSQLSERVER_9790 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 9790 (Database Engine error)
ms.assetid: 83fd379f-5deb-4f97-8cb4-282e3d3fed94
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: dd965940d43fdcc1e2420e8c5a43e512b45298e2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63014969"
---
# <a name="mssqlserver9790"></a>MSSQLSERVER_9790
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|9790|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|SB3_XMIT_ERROR_ENTRANCE_BROKER_SINGLE_USER|  
|Testo del messaggio|Impossibile eseguire il routing del messaggio in arrivo. Il database di sistema MSDB contenente le informazioni di routing è in modalità utente singolo.|  
  
## <a name="explanation"></a>Spiegazione  
Si è verificato un errore durante il tentativo di classificare un messaggio ricevuto fuori collegamento poiché il database MSDB è in modalità utente singolo.  
  
## <a name="user-action"></a>Azione dell'utente  
Impostare MSDB sulla modalità MULTI USER con il comando ALTER DATABASE.  
  
