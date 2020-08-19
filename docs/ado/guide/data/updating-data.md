---
description: Aggiornamento dei dati
title: Aggiornamento dei dati | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data updates [ADO], about data updates
- updating data [ADO], about updating data
ms.assetid: 6508e4e9-e33a-4dad-b340-5d632fd78a91
author: rothja
ms.author: jroth
ms.openlocfilehash: 5ea884479e7353b822e8b679a0fff34d70c3fd93
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88452643"
---
# <a name="updating-data"></a>Aggiornamento dei dati
Il comportamento e le funzionalità degli aggiornamenti dipendono in gran parte dalla modalità di aggiornamento (tipo di blocco), dal tipo di cursore e dalla posizione del cursore.  
  
 Utilizzare il metodo **Update** per salvare le modifiche apportate al record corrente di un oggetto **Recordset** , a partire dalla chiamata al metodo **AddNew** o dalla modifica dei valori di campo in un record esistente. L'oggetto **Recordset** deve supportare gli aggiornamenti.  
  
 Se l'oggetto **Recordset** supporta l'aggiornamento in batch, è possibile memorizzare nella cache più modifiche a uno o più record localmente fino a quando non si chiama il metodo **UpdateBatch** . Se si modifica il record corrente o si aggiunge un nuovo record quando si chiama il metodo **UpdateBatch** , ADO chiamerà automaticamente il metodo **Update** per salvare le modifiche in sospeso apportate al record corrente prima di trasmettere le modifiche in batch al provider.  
  
 Il record corrente rimane aggiornato dopo la chiamata dei metodi **Update** o **UpdateBatch** .  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Modalità immediata](../../../ado/guide/data/immediate-mode.md)  
  
-   [Modalità batch](../../../ado/guide/data/batch-mode.md)  
  
-   [Elaborazione delle transazioni](../../../ado/guide/data/transaction-processing.md)
