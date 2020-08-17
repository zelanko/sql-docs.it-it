---
description: Origini dati
title: Origini dati | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC]
- data sources [ODBC], about data sources
ms.assetid: 4ae44fa2-0b9b-4e19-ab45-c1dc93b68406
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3b9f980ad9ccd1fa38b6fce863703ec706e21a76
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88386057"
---
# <a name="data-sources"></a>Origini dati
Un' *origine dati* è semplicemente l'origine dei dati. Può trattarsi di un file, di un database specifico in un DBMS o anche di un feed di dati attivo. I dati potrebbero trovarsi nello stesso computer del programma o in un altro computer in una rete. Ad esempio, un'origine dati potrebbe essere un sistema DBMS Oracle in esecuzione su un sistema operativo/2®, a cui si accede da Novell® NetWare; un DBMS IBM DB2 a cui si accede tramite un gateway; raccolta di file Xbase in una directory del server. o un file di database locale di Microsoft® Access.  
  
 Lo scopo di un'origine dati consiste nel raccogliere tutte le informazioni tecniche necessarie per accedere ai dati, ovvero il nome del driver, l'indirizzo di rete, il software di rete e così via, in un'unica posizione e di nasconderlo dall'utente. L'utente deve essere in grado di esaminare un elenco che includa retribuzioni, inventario e personale, scegliere Payroll dall'elenco e fare in modo che l'applicazione si connetta ai dati relativi alle retribuzioni, senza sapere dove risiedono i dati delle retribuzioni o il modo in cui l'applicazione è stata trovata.  
  
 Il termine *origine dati* non deve essere confuso con termini simili. In questo manuale, *DBMS* o *database* si riferisce a un programma o a un motore di database. Viene fatta un'ulteriore distinzione tra i *database desktop,* progettati per l'esecuzione su personal computer e spesso privi di supporto completo per SQL e transazioni e per i *database server,* progettati per l'esecuzione in una situazione client/server e caratterizzati da un motore di database autonomo e dal supporto avanzato per SQL e transazioni. Il *database* fa riferimento anche a una raccolta specifica di dati, ad esempio una raccolta di file Xbase in una directory o un Database in SQL Server. È in genere equivalente al termine *Catalog,* usato in altre parti del manuale, o al termine *qualificatore* nelle versioni precedenti di ODBC.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Tipi di origini dati](../../odbc/reference/types-of-data-sources.md)  
  
-   [Uso delle origini dati](../../odbc/reference/using-data-sources.md)  
  
-   [Esempio di origine dati](../../odbc/reference/data-source-example.md)
