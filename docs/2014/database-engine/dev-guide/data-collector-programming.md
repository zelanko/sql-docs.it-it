---
title: Programmazione dell'agente di raccolta dati | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: reference
helpviewer_keywords:
- data collector [SQL Server], programming
ms.assetid: 53b4752b-055d-4716-b2bc-75b4cce84101
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 9f4da839f25da8f8aab3e21fa98547eff72d2140
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84933642"
---
# <a name="data-collector-programming"></a>Programmazione dell'agente di raccolta dati
  L'API dell'agente di raccolta dati, nello spazio dei nomi <xref:Microsoft.SqlServer.Management.Collector>, consente il controllo a livello di codice di tutte le operazioni di configurazione tramite il modello a oggetti. Molte delle operazioni di raccolta dati in cui viene utilizzata l'API vengono inoltre implementate come stored procedure installate nel server.

 Nell'illustrazione seguente sono riportati gli elementi principali del modello a oggetti dell'agente di raccolta dati.

 ![Modello a oggetti dell'agente di raccolta dati](../../../2014/database-engine/dev-guide/media/dc-objectmodel.gif "Modello a oggetti dell'agente di raccolta dati")


