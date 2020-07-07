---
title: Applicazioni multithread | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- threads [SQL Server], multithreaded applications
- ODBC applications, multithreaded applications
- asynchronous operations [SQL Server Native Client]
- SQL Server Native Client ODBC driver, multithreaded applications
- multithreaded applications [SQL Server Native Client]
ms.assetid: d352c91a-6e08-4e50-9f3e-a37892d9c2cc
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9c64c45331ec5f8efe11ee75abb065201cda0714
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: it-IT
ms.lasthandoff: 07/06/2020
ms.locfileid: "86009787"
---
# <a name="creating-a-driver-application---multithreaded-applications"></a>Creazione di un'applicazione driver - Applicazioni multithreading
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Il driver ODBC di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client è un driver a thread multipli. La scrittura di un'applicazione a thread multipli costituisce un'alternativa all'utilizzo di chiamate asincrone per elaborare più chiamate ODBC. Un thread può effettuare una chiamata ODBC asincrona e altri thread possono eseguire l'elaborazione mentre il primo thread è bloccato in attesa della risposta alla chiamata. Questo modello è più efficiente dell'esecuzione di chiamate asincrone, in quanto elimina l'overhead quale il traffico di rete e l'esecuzione di test di chiamate a funzioni ODBC ripetute per SQL_STILL_EXECUTING.  
  
 La modalità asincrona non rappresenta ancora un metodo efficace per l'elaborazione. I miglioramenti nelle prestazioni di un modello a thread multipli non sono sufficienti a giustificare la riscrittura delle applicazioni asincrone. Se gli utenti convertono applicazioni DB-Library che utilizzano il modello asincrono DB-Library, sarà più semplice convertirle nel modello asincrono ODBC.  
  
## <a name="see-also"></a>Vedere anche  
 [Creazione di un'applicazione driver ODBC di SQL Server Native Client](../../../relational-databases/native-client/odbc/creating-a-driver-application.md)  
  
  
