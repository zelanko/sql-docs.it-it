---
title: Componenti SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Upgrade Advisor, components
- listing components to analyze
- Upgrade Advisor [SQL Server], components
- component analysis [Upgrade Advisor]
- finding components to analyze
- locating components to analyze
- detecting components to analyze
- server names [Upgrade Advisor]
- analyzing system [Upgrade Advisor], component list
- identifying components to analyze
ms.assetid: 539b9525-ce3f-4950-9146-5527a5a297ee
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 809705e50e9337a63bf33c2883a1e5d43197be09
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85036276"
---
# <a name="sql-server-components"></a>Componenti di SQL Server
  È possibile eseguire l'analisi guidata di preparazione aggiornamento in un computer locale o remoto in cui è [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] installato,, [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] o [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] . Il primo passaggio dell'analisi di pre-aggiornamento consiste nell'identificare il computer e i componenti per l'analisi.  
  
## <a name="options"></a>Opzioni  
 **Nome computer**  
 Specifica il nome del computer da analizzare, Preparazione aggiornamento compila la casella **nome server** con il nome del computer locale. È anche possibile utilizzare "." e "localhost" per connettersi al computer locale.  
  
 Per analizzare un computer diverso, utilizzare le linee guida seguenti:  
  
-   Per analizzare le istanze non cluster, immettere il nome del computer.  
  
-   Per analizzare istanze cluster, immettere il nome dell'istanza del cluster di failover di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Per analizzare i componenti non cluster installati in un nodo di un cluster, immettere il nome del computer del nodo del cluster di failover.  
  
    > [!IMPORTANT]  
    >  Non includere il nome dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Anziché il nome del computer, è possibile specificare l'indirizzo IP.  
  
 Se si analizza [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], è necessario specificare il nome del computer locale. Con Preparazione aggiornamento vengono analizzati solo i server di report locali.  
  
 **Detect**  
 Il pulsante **rileva** accede al computer specificato e rileva i componenti da analizzare:  
  
-   Se si analizza un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in un computer remoto, è necessario abilitare i servizi del Registro di sistema nel computer remoto.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene rilevato se nel Registro di sistema del computer viene individuata un'istanza di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] o [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)].  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] viene rilevato se nel Registro di sistema del computer viene individuata un'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] viene rilevato se nel Registro di sistema del computer viene individuato [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Tuttavia, con Preparazione aggiornamento vengono analizzati solo i server di report locali.  
  
 **Componenti**  
 Selezionare i componenti da analizzare. È possibile fare clic sul pulsante **rileva** per selezionare tutti i componenti installati nel computer. Accanto ai componenti rilevati come installati nel computer verrà visualizzato un segno di spunta. È anche possibile selezionare manualmente i componenti da analizzare selezionando o deselezionando la casella di controllo corrispondente.  
  
## <a name="see-also"></a>Vedere anche  
 [Utilizzo di preparazione aggiornamento](../../../2014/sql-server/install/working-with-upgrade-advisor.md)   
 [Guida di riferimento all'interfaccia utente di Preparazione aggiornamento](../../../2014/sql-server/install/upgrade-advisor-user-interface-reference.md)  
  
  
