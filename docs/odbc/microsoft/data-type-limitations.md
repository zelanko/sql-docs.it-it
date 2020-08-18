---
description: Limitazioni dei tipi di dati
title: Limitazioni dei tipi di dati | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC desktop database drivers [ODBC], data types
- data types [ODBC], desktop database drivers
- desktop database drivers [ODBC], data types
ms.assetid: 81c4eab7-1f6b-47a0-b940-89d6c6a14dae
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4853846f21aa0ad763295bbdc4233c472ac53864
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88412787"
---
# <a name="data-type-limitations"></a>Limitazioni dei tipi di dati
I driver di database di Microsoft ODBC Desktop impongono le seguenti limitazioni sui tipi di dati:  
  
|Tipo di dati|Descrizione|  
|---------------|-----------------|  
|Tutti i tipi di dati|Gli errori di conversione dei tipi possono comportare l'impostazione della colonna interessata su NULL.|  
|BINARY|La creazione di una colonna BINARIa di lunghezza zero restituisce effettivamente una colonna BINARIa a 255 byte.|  
|DATE|Il tipo di dati DATE non può essere convertito in un altro tipo di dati (o in se stesso) tramite la funzione CONVERT.|  
|DECIMAL (valore numerico esatto)|Non supportato.|  
|Tipi di dati a virgola mobile|Il numero di posizioni decimali in un numero a virgola mobile può essere limitato dal formato numerico impostato nella sezione internazionale del pannello di controllo di Windows.|  
|NUMERIC|Supporta la precisione massima e una scala di 28.|  
|timestamp|Il tipo di dati TIMESTAMP non può essere convertito in se stesso dalla funzione CONVERT.|  
|TINYINT|I valori TINYINT sono sempre senza segno.|  
|Stringhe di lunghezza zero|Quando si usa dBASE, Microsoft Excel, Paradox o Textdriver, l'inserimento di una stringa di lunghezza zero in una colonna inserisce effettivamente un valore NULL.|
