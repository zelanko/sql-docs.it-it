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
manager: craigg
ms.openlocfilehash: 889158e04cbadb63c712ead73a61a7002ea61eae
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "78175370"
---
# <a name="data-collector-programming"></a>Programmazione dell'agente di raccolta dati
  L'API dell'agente di raccolta dati, nello spazio dei nomi <xref:Microsoft.SqlServer.Management.Collector>, consente il controllo a livello di codice di tutte le operazioni di configurazione tramite il modello a oggetti. Molte delle operazioni di raccolta dati in cui viene utilizzata l'API vengono inoltre implementate come stored procedure installate nel server.

 Nell'illustrazione seguente sono riportati gli elementi principali del modello a oggetti dell'agente di raccolta dati.

 ![Modello a oggetti dell'agente di raccolta dati](../../../2014/database-engine/dev-guide/media/dc-objectmodel.gif "Modello a oggetti dell'agente di raccolta dati")


