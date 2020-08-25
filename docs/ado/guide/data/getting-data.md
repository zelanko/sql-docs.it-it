---
description: Recupero di dati
title: Recupero di dati | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO, getting data
ms.assetid: 3931e7ec-f66b-4d5d-aad3-c4bf12e8b154
author: rothja
ms.author: jroth
ms.openlocfilehash: 80f1bcfad7a931898396d2463275a2426fbf0033
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/25/2020
ms.locfileid: "88806810"
---
# <a name="getting-data"></a>Recupero di dati
Le [nozioni di base su ADO](./ado-fundamentals.md)e l'esempio [HelloData](./hellodata-a-simple-ado-application.md) , in particolare, hanno introdotto le quattro operazioni principali necessarie per la creazione di un'applicazione ADO, ovvero il recupero dei dati, l'analisi dei dati, la modifica dei dati e l'aggiornamento dei dati. Questa sezione illustra il recupero dei dati in modo più dettagliato.  
  
 A livello di base, diversi oggetti ADO contribuiscono alle operazioni di recupero dei dati. Per prima cosa è necessario connettersi a un'origine dati utilizzando un oggetto ADO **Connection** . Passare quindi le istruzioni all'origine dati usando un oggetto **comando** ADO. Infine, si ricevono spesso dati in un oggetto **Recordset** ADO.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Connessione a origini dati](./connecting-to-data-sources.md)  
  
-   [Preparazione ed esecuzione di comandi](./preparing-and-executing-commands.md)  
  
-   [Ricezione dei risultati](./receiving-results.md)