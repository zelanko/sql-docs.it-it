---
title: Meccanismi interni OLTP in memoria di SQL Server
description: Informazioni sull'implementazione della tecnologia OLTP in memoria di SQL Server che dichiara le tabelle come ottimizzate per la memoria per abilitare le funzionalità di OLTP in memoria.
ms.custom: seo-dt-2019
ms.date: 09/14/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: b14da361-a6b8-4d85-b196-7f2f13650f44
author: jodebrui
ms.author: jodebrui
ms.openlocfilehash: 4f9b1e77d082ad5e42a9818272fc1c4a48b44968
ms.sourcegitcommit: d56a834269132a83e5fe0a05b033936776cda8bb
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/29/2020
ms.locfileid: "91529382"
---
# <a name="sql-server-in-memory-oltp-internals-for-sql-server-2016"></a>Caratteristiche interne di OLTP in memoria di SQL Server per SQL Server 2016
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

**Riepilogo:** OLTP in memoria, a cui si fa spesso riferimento con il nome in codice "Hekaton", è stato introdotto in SQL Server 2014.
Questa efficace tecnologia consente di sfruttare grandi quantità di memoria e decine di core per migliorare da 30 a 40 volte in più le prestazioni delle operazioni di OLTP. SQL Server 2016 sta ampliando l'interazione con OLTP in memoria rimuovendo gran parte delle limitazioni rilevate in SQL Server 2014 e migliorando gli algoritmi di elaborazione interna in modo che OLTP in memoria possa offrire prestazioni ancora più efficienti. Questo articolo illustra l'implementazione della tecnologia di OLTP in memoria di SQL Server 2016 a partire da SQL Server 2016 RTM. Con l'uso di OLTP in memoria, le tabelle possono essere dichiarate come "tabelle ottimizzate per la memoria" per abilitare le funzionalità di OLTP in memoria. Le tabelle con ottimizzazione per la memoria sono completamente transazionali e sono accessibili tramite Transact-SQL. Le stored procedure di Transact-SQL, i trigger e le funzioni definite dall'utente scalari possono essere compilati in codice macchina per migliorare ulteriormente le prestazioni nelle tabelle ottimizzate per la memoria. Il motore è progettato per una concorrenza elevata senza blocchi.    
  
**Autore:** Kalen Delaney  
  
**Revisori tecnici:** Sunil Agarwal e Jos de Bruijn  
  
**Data di pubblicazione:** Giugno 2016  
  
**Si applica a:** SQL Server 2016  
  
Per leggere l'articolo, scaricare il documento [Caratteristiche interne di OLTP in memoria di SQL Server per SQL Server 2016](https://download.microsoft.com/download/8/3/6/8360731A-A27C-4684-BC88-FC7B5849A133/SQL_Server_2016_In_Memory_OLTP_White_Paper.pdf).   
