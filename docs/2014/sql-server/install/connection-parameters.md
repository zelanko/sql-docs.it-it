---
title: I parametri di connessione | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Upgrade Advisor [SQL Server], connections
- authentication [Upgrade Advisor]
- SQL Server Upgrade Advisor, connections
- connections [Upgrade Advisor]
- server instances [Upgrade Advisor]
- default server instances
- analyzing system [Upgrade Advisor], connections
ms.assetid: f754d038-637a-4d8e-85b0-b242e6499d26
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ca5d6ed8f1e8a92d22bd32e39c8afe946a0fcfee
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66095982"
---
# <a name="connection-parameters"></a>Parametri di connessione
  Per analizzare determinati tipi di server, ad esempio il [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], è necessario selezionare un'istanza specifica di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Viene automaticamente selezionata l'istanza predefinita di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. È possibile modificare questa selezione, selezionando però solo un'istanza alla volta per l'analisi da Preparazione aggiornamento. Se è stato incluso un tipo di server che richiede l'autenticazione, è necessario immettere la modalità di autenticazione e le credenziali.  
  
## <a name="options"></a>Opzioni  
 **Nome server**  
 Questo campo viene prepopolato con il nome del computer immesso nel riquadro Componenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **Nome dell'istanza**  
 Selezionare una delle istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] disponibili nel computer. Se l'elenco di istanze non viene visualizzato, utilizzare MSSQLSERVER per analizzare l'istanza predefinita. Ciò riguarda soprattutto i computer remoti. È anche possibile utilizzare l'espressione "valore predefinito" per analizzare l'istanza predefinita.  
  
 **Autenticazione**  
 Selezionare una delle modalità di autenticazione disponibili nel computer. Per impostazione predefinita, la modalità di autenticazione è l'autenticazione di Windows.  
  
 **Nome utente**  
 Se si utilizza l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], immettere un nome utente nella casella. È consigliabile che il nome utente disponga delle credenziali amministrative nel computer.  
  
> [!NOTE]  
>  Se si seleziona l'autenticazione di Windows, il nome utente dell'utente attualmente connesso viene popolato nel **nome utente** casella di testo.  
  
 **Password**  
 Immettere la password per l'utente specificato.  
  
## <a name="see-also"></a>Vedere anche  
 [Utilizzo di preparazione aggiornamento](../../../2014/sql-server/install/working-with-upgrade-advisor.md)   
 [Riferimento all'interfaccia utente di preparazione aggiornamento](../../../2014/sql-server/install/upgrade-advisor-user-interface-reference.md)  
  
  
