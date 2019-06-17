---
title: L'aggiornamento dei dati | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 8ea95b7d34f1395f6322d9a6ad6a0229bb8c7e45
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66704563"
---
# <a name="updating-data"></a>Aggiornamento di dati
Comportamento di aggiornamento e le funzionalità non dipende in larga misura aggiornamento modalità (tipo di blocco), il tipo di cursore e posizione del cursore.  
  
 Usare la **Update** metodo per salvare le modifiche apportate al record corrente di un **Recordset** oggetto dal momento della chiamata il **AddNew** (metodo) oppure dopo aver modificato i valori di campo in un record esistente. Il **Recordset** oggetto deve supportare gli aggiornamenti.  
  
 Se il **Recordset** oggetto supporta l'aggiornamento in batch, è possibile memorizzare nella cache più modifiche a uno o più record in locale fino a quando non si chiama il **UpdateBatch** (metodo). Se si modifica il record corrente o aggiungere un nuovo record quando si chiama il **UpdateBatch** metodo, ADO chiama automaticamente il **Update** metodo per salvare le modifiche in sospeso per il record corrente prima di trasmettere le modifiche in batch al provider.  
  
 Il record corrente rimane invariato dopo aver chiamato il **Update** oppure **UpdateBatch** metodi.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Modalità immediata](../../../ado/guide/data/immediate-mode.md)  
  
-   [Modalità batch](../../../ado/guide/data/batch-mode.md)  
  
-   [Elaborazione di transazioni](../../../ado/guide/data/transaction-processing.md)
