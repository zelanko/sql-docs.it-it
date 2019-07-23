---
title: Utilità di avvio del daemon filtri full-text di SQL (Gestione configurazione SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: d0dc03db-5f76-4558-b041-1ac7b9b5bb16
author: markingmyname
ms.author: maghan
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: dbc9921dc09f8e55be0bdb4d38953422dc5e7125
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68058306"
---
# <a name="sql-full-text-filter-daemon-launcher-sql-server-configuration-manager"></a>Utilità di avvio del daemon filtri full-text di SQL (Gestione configurazione SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
  A partire da [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], il servizio Utilità di avvio del daemon filtri full-text di SQL (FDHOST Launcher) viene utilizzato dalla ricerca full-text in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per avviare il processo host del daemon di filtri che gestisce il word breaking e l'applicazione di filtri per la ricerca full-text. Per utilizzare la ricerca full-text, questo servizio deve essere in esecuzione. Il servizio utilità di avvio di FDHOST è un servizio specifico dell'istanza associato a una determinata istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Tale servizio propaga le informazioni sull'account del servizio a ogni processo host del daemon di filtri avviato. Per informazioni sui processi host del daemon di filtri, vedere "Architettura della ricerca full-text" nella documentazione online di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
  
