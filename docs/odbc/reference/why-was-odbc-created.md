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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 22173b0ad3dd8abf2d168b41a16a03bc414022ce
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302782"
---
# <a name="why-was-odbc-created"></a>Motivi per la creazione di ODBC
Storicamente, le aziende utilizzavano un singolo DBMS. Tutto l'accesso al database è stato fatto attraverso il front-end di tale sistema o attraverso applicazioni scritte per funzionare esclusivamente con quel sistema. Tuttavia, man mano che l'uso dei computer cresceva e diventava disponibile un maggior numero di hardware e software per computer, le aziende iniziarono ad acquisire diversi DBS. Le ragioni erano molte: le persone hanno comprato ciò che era più economico, ciò che era più veloce, quello che già sapevano, ciò che era più recente sul mercato, ciò che funzionava meglio per una singola applicazione. Altri motivi erano le riorganizzazioni e le fusioni, in cui i dipartimenti che in precedenza avevano un solo DBMS ne avevano ora diversi.  
  
 Il problema è diventato ancora più complesso con l'avvento dei personal computer. Questi computer hanno portato in una serie di strumenti per l'esecuzione di query, l'analisi e la visualizzazione dei dati, insieme a una serie di database poco costosi e facili da usare. Da allora in poi, una singola azienda aveva spesso dati sparsi in una miriade di desktop, server e minicomputer, memorizzati in una varietà di database incompatibili e a cui si accede da un vasto numero di strumenti diversi, pochi dei quali potrebbero ottenere tutti i dati.  
  
 La sfida finale è arrivata con l'avvento del client/server computing, che cerca di sfruttare al meglio le risorse del computer. I personal computer economici (i client) si esibiscono sul desktop e forniscono sia un front-end grafico ai dati che una serie di strumenti economici, come fogli di calcolo, programmi di creazione di grafici e generatore di report. I minicomputer e i computer mainframe (i server) ospitano i DBS, dove possono utilizzare la loro potenza di calcolo e la loro posizione centrale per fornire un accesso rapido e coordinato ai dati. In che modo il software front-end doveva quindi essere connesso ai database back-end?  
  
 Un problema simile riguardava fornitori di software indipendenti (ISV). I fornitori che scrivono software di database per minicomputer e mainframe sono stati in genere costretti a scrivere una versione di un'applicazione per ogni DBMS o scrivere codice specifico DBMS per ogni DBMS a cui volevano accedere. I fornitori che scrivevano software per personal computer dovevano scrivere routine di accesso ai dati per ogni DBMS diverso con cui volevano lavorare. Questo spesso significava una grande quantità di risorse sono state spese per la scrittura e la manutenzione delle routine di accesso ai dati piuttosto che le applicazioni, e le applicazioni sono state spesso vendute non sulla loro qualità, ma per quanto riguarda se potevano accedere ai dati in un determinato DBMS.  
  
 Ciò di cui entrambe le serie di sviluppatori avevano bisogno era un modo per accedere ai dati in DBS diversi. Il gruppo mainframe e minicomputer aveva bisogno di un modo per unire i dati provenienti da diversi DBMS in un'unica applicazione, mentre il gruppo di personal computer aveva bisogno di questa capacità e di un modo per scrivere una singola applicazione indipendente da qualsiasi DBMS. In breve, entrambi i gruppi avevano bisogno di un modo interoperabile per accedere ai dati; avevano bisogno di connettività di database aperta.
