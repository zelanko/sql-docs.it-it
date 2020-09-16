---
description: Gestione delle dimensioni delle transazioni
title: Gestione delle dimensioni delle transazioni | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 82900342-bc80-445f-98a4-468a303aae1e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1ba88edf4c4c8f1dfb4e8b7cd27db3102be448c4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88438373"
---
# <a name="managing-transaction-size"></a>Gestione delle dimensioni delle transazioni
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Quando si utilizzano le transazioni, è importante garantire che siano il più brevi possibile. La modalità di commit automatico predefinita, che è possibile abilitare o disabilitare usando il metodo [setAutoCommit](../../connect/jdbc/reference/setautocommit-method-sqlserverconnection.md), esegue automaticamente il commit di ogni azione. e costituisce il metodo di lavoro più semplice per la maggior parte degli sviluppatori.  
  
 Quando si utilizzano transazioni manuali, assicurarsi che il codice esegua il commit della transazione il più rapidamente possibile. Se una transazione viene tenuta aperta, gli altri utenti non possono accedere ai dati. Durante la programmazione è ad esempio consigliabile inserire una chiamata di rollback nel blocco catch e una chiamata di commit nel blocco finally. Questo dipende tuttavia dalla progettazione dell'applicazione.  
  
 Contenendo la dimensione delle transazioni, è possibile creare una concorrenza migliore. Se ad esempio si avvia una transazione manuale e si modificano 10.000 righe in una tabella costituita da 20.000 righe, metà tabella sarà completamente bloccata per tutti gli altri utenti, anche se stanno solo leggendo i dati. Riducendo le modifiche a 2.000 righe, si lascia disponibile il 90% della tabella.  
  
 Assicurarsi inoltre di utilizzare l'impostazione di timeout del blocco se per l'applicazione si prevedono situazioni di blocco ed è necessario impostare un timeout per tali situazioni. A tale scopo, usare il metodo [setLockTimeout](../../connect/jdbc/reference/setlocktimeout-method-sqlserverdatasource.md). L'impostazione predefinita per il timeout del blocco è -1, che significa che il blocco ha un tempo indefinito. È possibile impostare il timeout del blocco su 30 secondi, che significa che se una connessione bloccata viene bloccata da un'altra connessione, si verifica il timeout entro 30 secondi.  
  
## <a name="see-also"></a>Vedere anche  
 [Uso del driver JDBC per il miglioramento di prestazioni e affidabilità](../../connect/jdbc/improving-performance-and-reliability-with-the-jdbc-driver.md)  
  
  
