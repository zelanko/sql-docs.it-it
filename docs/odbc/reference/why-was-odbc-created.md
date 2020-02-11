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
ms.openlocfilehash: 8cfdd0babe84d309391b3e1ca546c4e05fdf1331
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68049170"
---
# <a name="why-was-odbc-created"></a>Motivi per la creazione di ODBC
In passato le aziende usavano un singolo sistema DBMS. Tutti gli accessi al database sono stati eseguiti attraverso il front-end del sistema o le applicazioni scritte per funzionare esclusivamente con tale sistema. Tuttavia, con l'aumento dell'utilizzo dei computer e la disponibilità di hardware e software per computer, le aziende hanno iniziato ad acquisire diversi DBMS. I motivi sono molti: gli utenti hanno acquistato quello che era più economico, cosa era più veloce, cosa sapevano, cosa era più recente sul mercato, che funzionava meglio per una singola applicazione. Altri motivi sono rappresentati da riorganizzazioni e fusioni, in cui i reparti che in precedenza avevano un singolo DBMS ora erano diversi.  
  
 Il problema è diventato ancora più complesso con l'avvento dei personal computer. Questi computer hanno introdotto una serie di strumenti per l'esecuzione di query, l'analisi e la visualizzazione dei dati, oltre a una serie di database convenienti e di facile utilizzo. Da quel punto in poi, una singola azienda possedeva spesso dati sparsi in una miriade di desktop, server e minicomputer, archiviati in un'ampia gamma di database incompatibili e a cui si accede da un vasto numero di strumenti diversi, alcuni dei quali potrebbero ottenere tutti i dati.  
  
 La sfida finale è stata rappresentata dall'avvento dell'elaborazione client/server, che cerca di sfruttare al meglio le risorse del computer. I computer personali economici (i client) si trovano sul desktop e forniscono un front-end grafico ai dati e una serie di strumenti economici, ad esempio fogli di calcolo, programmi per grafici e generatori di report. I computer minicomputer e mainframe (i server) ospitano i DBMS, dove possono utilizzare la potenza di calcolo e la posizione centrale per offrire un accesso ai dati rapido e coordinato. In che modo è stato possibile connettere il software front-end ai database back-end?  
  
 Un problema analogo affrontato con fornitori di software indipendenti (ISV). I fornitori che scrivono software di database per minicomputer e mainframe venivano in genere costretti a scrivere una versione di un'applicazione per ogni DBMS o scrivere codice specifico del DBMS per ogni DBMS a cui volevano accedere. I fornitori che scrivono software per personal computer hanno dovuto scrivere routine di accesso ai dati per ogni DBMS diverso con cui volevano lavorare. Questa operazione spesso significava una grande quantità di risorse per la scrittura e la gestione delle routine di accesso ai dati piuttosto che delle applicazioni, mentre le applicazioni venivano spesso vendute senza la loro qualità, ma con la possibilità di accedere ai dati in un determinato sistema DBMS.  
  
 Gli insiemi di sviluppatori necessari erano un modo per accedere ai dati in DBMS diversi. Il gruppo mainframe e minicomputer aveva bisogno di un modo per unire i dati da DBMS diversi in una singola applicazione, mentre il gruppo personal computer aveva bisogno di questa capacità e di scrivere una singola applicazione indipendente da un sistema DBMS. In breve, entrambi i gruppi necessitavano di un metodo interoperativo per accedere ai dati; necessari per la connettività open database.
