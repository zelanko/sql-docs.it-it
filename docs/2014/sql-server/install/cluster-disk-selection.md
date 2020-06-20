---
title: Selezione disco cluster | Microsoft Docs
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
ms.openlocfilehash: 0f53d6d3f623254d2b17996be7fd5b8235dca223
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85037122"
---
# <a name="cluster-disk-selection"></a>Selezione dischi cluster
  Usare la pagina **Selezione dischi cluster** dell'Installazione guidata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per selezionare la risorsa disco del cluster condiviso per il cluster di failover di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Il disco del cluster è l'unità in cui verranno memorizzati i dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Un disco del cluster condiviso non è un requisito per le [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] installazioni di cluster. Un file server SMB è una risorsa di archiviazione supportata per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] le installazioni del cluster di failover di e può essere specificato tramite la pagina **motore di database-Directory dati** prima di completare l'installazione.  
  
> [!WARNING]  
>  Se si è scelto di installare Analysis Services, è necessario specificare un disco del cluster condiviso.  
>   
>  Se si intende abilitare FILESTREAM in questa istanza del cluster di failover di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , è necessario specificare un disco del cluster condiviso.  
  
## <a name="options"></a>Opzioni  
 **Dischi condivisi**  
 Selezionare un singolo disco dall'elenco. Il disco del cluster è l'unità in cui verranno memorizzati i dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 È possibile specificare un solo disco. Se si seleziona il gruppo contenente la risorsa quorum del cluster, verrà visualizzato un messaggio di avviso. È consigliabile non installare la risorsa quorum del cluster.  
  
 **Dischi condivisi disponibili**  
 Visualizza un elenco dei dischi disponibili, una descrizione di ogni risorsa disco e l'indicazione se ciascun disco è qualificato come disco fisso.  
  
  
