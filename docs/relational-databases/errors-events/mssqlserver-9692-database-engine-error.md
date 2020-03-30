---
title: MSSQLSERVER_9692 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 9692 (Database Engine error)
ms.assetid: 02399d6e-ab5e-4f30-8a3e-2bb1e8c135b5
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 7041aa3e2262932541c4d81fe93dd1d9a740c97a
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "67903809"
---
# <a name="mssqlserver_9692"></a>MSSQLSERVER_9692
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Dettagli  
  
|||  
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
Eseguire **netstat -aon** per determinare quale programma sta usando la porta. Disabilitare l'applicazione oppure specificare una porta diversa per Service Broker.  
  
