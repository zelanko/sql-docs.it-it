---
title: MSSQLSERVER_9790 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 9790 (Database Engine error)
ms.assetid: 83fd379f-5deb-4f97-8cb4-282e3d3fed94
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5747a13e60182596610f25dd4ed1243670ff5018
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62912175"
---
# <a name="mssqlserver_9790"></a>MSSQLSERVER_9790
    
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
  
  
