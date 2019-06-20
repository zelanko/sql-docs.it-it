---
title: Motivi per la creazione di ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC [ODBC], about ODBC
ms.assetid: ba6eb993-316b-4650-bab8-d76583c00e53
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 871919554975f04fae0aeaa1b8e6ec684c6650a4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62714148"
---
# <a name="why-was-odbc-created"></a>Motivi per la creazione di ODBC
In passato, le aziende utilizzato un singolo DBMS. L'accesso al database è stato eseguito il front-end del sistema o mediante le applicazioni scritte per lavorare esclusivamente con tale sistema. Tuttavia, quando le dimensioni sono aumentate dell'utilizzo di computer e ulteriori componenti hardware e software è diventato disponibile, le aziende è stata avviata acquisire diversi DBMS. I motivi sono numerosi: Persone bought Qual era più conveniente, qual è più veloce, le risorse di cui già conosce, ciò che è stato più recente sul mercato, cosa ha funzionato ottimale per una singola applicazione. Per altri motivi erano riorganizzazione e fusioni, in cui i reparti che in precedenza aveva un DBMS singolo ora include diversi.  
  
 Il problema sono aumentate ancora più complesso con l'avvento dei personal computer. Questi computer portati in una serie di strumenti per l'esecuzione di query, analisi e visualizzazione dei dati, insieme a un numero di database convenienti e facile da usare. Da questo momento, una singola azienda è spesso dati sparsi tra una miriade di desktop, server e minicomputer, archiviati in un'ampia gamma di database incompatibili e dell'accesso da una vasta gamma di strumenti diversi, alcuni dei quali è stato possibile ottenere tutti i dati.  
  
 La richiesta di verifica finale fornita con l'avvento del client/server di elaborazione, che tenta di rendere l'uso più efficiente delle risorse del computer. Conveniente personal computer (client) si trovano sul desktop e forniscono entrambi un con interfaccia grafico front-end per i dati e una serie di strumenti poco costosi, ad esempio fogli di calcolo, creazione di grafici di programmi e generatori di report. I computer mainframe (server) e minicomputer ospitano DBMS, in cui è possibile usare la propria potenza di calcolo e di una posizione centrale per fornire l'accesso ai dati rapido e coordinato. Come si era il software front-end a cui connettersi i database back-end?  
  
 Un problema analogo affrontato i fornitori di software indipendenti (ISV). I fornitori di software di database per minicomputer e mainframe in genere erano costretti a scrivere una versione di un'applicazione per ogni sistema DBMS o scrivere codice specifico del sistema DBMS per ogni sistema DBMS è quindi necessario accedere. I fornitori di software per PC di scrittura dovevano scrivere routine di accesso ai dati per ogni diversi sistemi DBMS con il quale si desidera intervenire. Questo comportava una notevole quantità di risorse sono stati usati per la scrittura e la gestione di routine, piuttosto che le applicazioni di accesso ai dati e le applicazioni spesso sono state vendute non la qualità ma se è stato possibile accedere ai dati in un sistema DBMS.  
  
 Cosa necessari entrambi i set di sviluppatori è un modo per accedere ai dati nel DBMS diverso. Il gruppo di computer mainframe e minicomputer serviva un modo per unire dati da diversi DBMS in una singola applicazione, mentre il gruppo di computer di personal necessaria questa possibilità, nonché un modo per scrivere una singola applicazione che era indipendente da qualsiasi un DBMS. In breve, entrambi i gruppi necessitassero una modalità interoperativa per accedere ai dati; aprono necessaria la connettività del database.
