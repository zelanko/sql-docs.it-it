---
description: Stato di sola lettura (driver Excel)
title: Stato di sola lettura (driver Excel) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- read-only status for Excel driver [ODBC]
- Excel driver [ODBC], read-only status
ms.assetid: ef5d773b-4f8f-4005-b985-84b53d8e9f9b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 04a0c5d0cb2c9932d30c0edb900169d8c5e5f82b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88340387"
---
# <a name="read-only-status-excel-driver"></a>Stato di sola lettura (driver Excel)
Quando si utilizza il driver Microsoft Excel, le tabelle di origine dati vengono aperte come di sola lettura per impostazione predefinita e possono essere aperte da un solo utente alla volta. Sebbene le tabelle abbiano stato di sola lettura, tuttavia, le applicazioni possono eseguire inserimenti e aggiornamenti per le tabelle di Microsoft Excel.  
  
 Quando un'applicazione esegue un comando Salva con nome sui dati di Microsoft Excel tramite il driver Microsoft Excel, l'applicazione deve creare una nuova tabella e inserire i dati da salvare nella nuova tabella. Inserisce il risultato in un accodamento alla tabella. Non è possibile eseguire altre operazioni sulla tabella fino a quando non viene chiusa e riaperta. Una volta chiusa la tabella, non è possibile eseguire operazioni INSERT successive perché la tabella è quindi una tabella di sola lettura.  
  
 È possibile aggiornare i valori quando si utilizza il driver Microsoft Excel, ma non è possibile eliminare una riga da una tabella basata su un foglio di calcolo di Microsoft Excel, quindi gli aggiornamenti non vengono considerati ufficialmente supportati dal driver Microsoft Excel.
