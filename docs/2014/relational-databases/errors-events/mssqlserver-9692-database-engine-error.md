---
title: MSSQLSERVER_9692 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 9692 (Database Engine error)
ms.assetid: 02399d6e-ab5e-4f30-8a3e-2bb1e8c135b5
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: b740f7be7512f73bfe5c6d570ce3a97464a163fe
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/21/2020
ms.locfileid: "86553016"
---
# <a name="mssqlserver_9692"></a>MSSQLSERVER_9692
    
## <a name="details"></a>Dettagli  
  
|Attributo|valore|  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|9692|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|SB2_CANT_LISTEN_PORT_IN_USE|  
|Testo del messaggio|Il trasporto di protocollo %S_MSG non può restare in attesa sulla porta %d perché è in uso da un altro processo.|  
  
## <a name="explanation"></a>Spiegazione  
 Un altro programma in esecuzione nel computer sta utilizzando la porta TCP indicata.  
  
## <a name="user-action"></a>Azione dell'utente  
 Eseguire `netstat -aon` per determinare quale programma sta utilizzando la porta. Disabilitare l'applicazione oppure specificare una porta diversa per Service Broker.  
  
  
