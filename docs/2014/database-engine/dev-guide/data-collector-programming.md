---
title: Programmazione dell'agente di raccolta dei dati | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 11da8d77f5ea97dc435b9af23090d1d34da0f05c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62753117"
---
# <a name="data-collector-programming"></a>Programmazione dell'agente di raccolta dati
  L'API dell'agente di raccolta dati, nello spazio dei nomi <xref:Microsoft.SqlServer.Management.Collector>, consente il controllo a livello di codice di tutte le operazioni di configurazione tramite il modello a oggetti. Molte delle operazioni di raccolta dati in cui viene utilizzata l'API vengono inoltre implementate come stored procedure installate nel server.  
  
 Nell'illustrazione seguente sono riportati gli elementi principali del modello a oggetti dell'agente di raccolta dati.  
  
 ![Il modello a oggetti dell'agente di raccolta dati](../../../2014/database-engine/dev-guide/media/dc-objectmodel.gif "il modello a oggetti dell'agente di raccolta dati")  
  
  
