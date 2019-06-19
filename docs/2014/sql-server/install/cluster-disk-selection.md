---
title: Selezione del disco del cluster | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- cluster disk selection
ms.assetid: 0d6b863d-5972-4a20-9990-64ee8016fea6
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 156c17d7dae5c4de07033a96f2e936448d8d02ed
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66096498"
---
# <a name="cluster-disk-selection"></a>Selezione dischi cluster
  Usare la pagina **Selezione dischi cluster** dell'Installazione guidata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per selezionare la risorsa disco del cluster condiviso per il cluster di failover di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Il disco del cluster è l'unità in cui verranno memorizzati i dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Un disco cluster condiviso non è un requisito per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] le installazioni di cluster. Un file server SMB è un archivio supportato per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] failover le installazioni di cluster e può essere specificato usando la **motore di Database - directory dati** pagina prima di completare l'installazione.  
  
> [!WARNING]  
>  Se si è scelto di installare Analysis Services, è necessario specificare un disco del cluster condiviso.  
>   
>  Se si intende abilitare FILESTREAM in questa istanza del cluster di failover di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è necessario specificare un disco del cluster condiviso.  
  
## <a name="options"></a>Opzioni  
 **Dischi condivisi**  
 Selezionare un singolo disco dall'elenco. Il disco del cluster è l'unità in cui verranno memorizzati i dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 È possibile specificare un solo disco. Se si seleziona il gruppo contenente la risorsa quorum del cluster, verrà visualizzato un messaggio di avviso. È consigliabile non installare la risorsa quorum del cluster.  
  
 **Dischi condivisi disponibili**  
 Visualizza un elenco dei dischi disponibili, una descrizione di ogni risorsa disco e l'indicazione se ciascun disco è qualificato come disco fisso.  
  
  
