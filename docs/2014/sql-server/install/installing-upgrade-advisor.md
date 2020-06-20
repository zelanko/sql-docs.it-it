---
title: Installazione di preparazione aggiornamento | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- installing Upgrade Advisor
- Setup [Upgrade Advisor]
- Upgrade Advisor [SQL Server], installing
ms.assetid: 1b7d6eca-1df1-47df-bbba-0fc485706a95
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 40f214b01f3e2066708a060c5f3ad1e8aa4a0a23
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85065338"
---
# <a name="installing-upgrade-advisor"></a>Installazione di Preparazione aggiornamento
  Il computer in cui installare Preparazione aggiornamento a SQL Server 2014 dipende dai componenti che verranno analizzati. Preparazione aggiornamento supporta l'analisi remota di tutti i componenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ad eccezione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Se non si stanno analizzando le istanze di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , è possibile installare Preparazione aggiornamento in qualsiasi computer in grado di connettersi a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e che soddisfi i [prerequisiti di preparazione aggiornamento](../../../2014/sql-server/install/upgrade-advisor-prerequisites.md). Se si prevede di analizzare le istanze di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], è necessario installare Preparazione aggiornamento nel server di report.  
  
 Eseguire il file di **SQLUA.msi** per installare Preparazione aggiornamento. È possibile eseguire l'installazione dal prompt dei comandi per installazioni automatiche e automatizzate. Per la sintassi e gli esempi, vedere [installazione di preparazione aggiornamento dal prompt dei comandi](../../../2014/sql-server/install/installing-upgrade-advisor-from-the-command-prompt.md) .  
  
 Ottenere SQLUA.msi:  
  
-   Nella cartella **Redist** del supporto del [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] prodotto.  
  
-   Come parte del [download del Feature Pack di SQL 2014](https://www.microsoft.com/download/details.aspx?id=42295).  
  
## <a name="uninstalling-upgrade-advisor"></a>Disinstallazione di Preparazione aggiornamento  
 È possibile disinstallare Preparazione aggiornamento utilizzando **Installazione applicazioni**. La sintassi del prompt dei comandi supporta anche la rimozione e/o la disinstallazione.  
  
  
