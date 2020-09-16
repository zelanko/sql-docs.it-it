---
title: Utilità di avvio del daemon filtri full-text di SQL (Gestione configurazione SQL Server)
description: Informazioni sull'Utilità di avvio del daemon filtri full-text di SQL, un servizio usato da SQL Server per avviare un processo necessario per la ricerca full-text.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
ms.assetid: d0dc03db-5f76-4558-b041-1ac7b9b5bb16
author: markingmyname
ms.author: maghan
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 793c05674f09a5fc7a0b85af314cd119c8896f6b
ms.sourcegitcommit: 6d53ecfdc463914f045c20eda96da39dec22acca
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/26/2020
ms.locfileid: "88900987"
---
# <a name="sql-full-text-filter-daemon-launcher-sql-server-configuration-manager"></a>Utilità di avvio del daemon filtri full-text di SQL (Gestione configurazione SQL Server)
[!INCLUDE [SQL Server Windows Only - ASDBMI ](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]
  A partire da [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], il servizio Utilità di avvio del daemon filtri full-text di SQL (FDHOST Launcher) viene utilizzato dalla ricerca full-text in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per avviare il processo host del daemon di filtri che gestisce il word breaking e l'applicazione di filtri per la ricerca full-text. Per utilizzare la ricerca full-text, questo servizio deve essere in esecuzione. Il servizio utilità di avvio di FDHOST è un servizio specifico dell'istanza associato a una determinata istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Tale servizio propaga le informazioni sull'account del servizio a ogni processo host del daemon di filtri avviato. Per informazioni sui processi host del daemon di filtri, vedere "Architettura della ricerca full-text" nella documentazione online di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
  
