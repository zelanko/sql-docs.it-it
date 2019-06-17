---
title: 'Case study: Creazione di un ecosistema aziendale con Microsoft Dynamics ERP e di SQL Server 2014 Replication for Scalability and Performance | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 2b0b5ab7-4e08-431a-bd59-360177c4565c
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 64a1423295b8117640de555a7132a44af98b87c0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62470102"
---
# <a name="case-study-building-an-enterprise-ecosystem-with-microsoft-dynamics-erp-and-sql-server-2014-replication-for-scalability-and-performance"></a>Case study: Creazione di un ecosistema aziendale con Microsoft Dynamics ERP e la replica di SQL Server 2014 per ottenere scalabilità e prestazioni

  **Riepilogo:** In questo documento illustra gli scenari seguenti:  
Come usare la replica transazionale in SQL Server 2014 per distribuire le transazioni dai client Dynamics AX in più nodi. Poiché i dati vengono gestiti nei nodi in tempo reale, la replica transazionale fornisce la ridondanza dei dati, che aumenta la disponibilità dei dati, e include i dati disponibili per un'analisi delle prestazioni più efficiente.  
Come comprendere le specifiche coinvolte, sfruttando al contempo la replica transazionale per creare ecosistemi aziendali altamente scalabili in Microsoft Dynamics ERP. Offrire prestazioni e scalabilità elevate senza personalizzare le funzionalità predefinite di AX.  
  
 La replica transazionale viene in genere usata nei flussi di lavoro server-server con esigenze di velocità effettiva elevata, inclusi gli scenari di miglioramento della scalabilità e della disponibilità, di data warehouse e creazione di report, di integrazione di dati da più siti, di integrazione di dati eterogenei e di offload dell'elaborazione batch. Questo white paper descrive uno scenario specifico e i modelli associati in cui viene usata la replica transazionale in Microsoft Dynamics ERP. Illustra anche le problematiche e le procedure consigliate nella valutazione della replica transazionale per creare soluzioni aziendali specifiche per ERP (Enterprise Resource Planning), nonché l'analisi delle prestazioni nelle diverse fasi.  
  
 Questo contenuto è adatto agli sviluppatori, agli architetti e agli amministratori di database. Si presuppone che i lettori di questo white paper abbiano una conoscenza di base di SQL Server 2008, 2012 o 2014, nonché esperienza di amministrazione di SQL Server.  
  
 **Writer:** Prabhakaran Sethuraman (PRAB), Microsoft  
  
 **Revisori tecnici:** Prabhakaran Sethuraman (PRAB), Microsoft; Santosh Padhy, Microsoft; Pavel Majstrov, Microsoft; Karthik Sankaranarayanan, Microsoft; Jon Acone, Microsoft; David Stahlkopf, Microsoft; Kent Oldenburger, Microsoft; Mandi Ohlinger, Microsoft; Jason Roth, Microsoft  
  
 **Data di pubblicazione:** ottobre 2015  
  
 **Si applica a:** SQL Server 2008, SQL Server 2012 e SQL Server 2014  
  
 Per esaminare il documento, scaricare il  
        [Case Study: Creazione di un ecosistema aziendale con Microsoft Dynamics ERP e la replica di SQL Server 2014 per la scalabilità e prestazioni](https://download.microsoft.com/download/D/2/0/D20E1C5F-72EA-4505-9F26-FEF9550EFD44/A%20Case%20Study%20Using%20Replication%20to%20Build%20an%20Enterprise%20Ecosystem%20in%20Microsoft%20Dynamics%20ERP%20for%20Scalability%20and%20Performance.docx) documento di Word.  
  
  
