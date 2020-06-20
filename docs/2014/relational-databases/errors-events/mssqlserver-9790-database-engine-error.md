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
ms.openlocfilehash: 6d6d065d4a0e841da3b5ecb84f902df17dcfd60c
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85031262"
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
  
  
