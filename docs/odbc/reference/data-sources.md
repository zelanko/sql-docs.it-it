---
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
ms.openlocfilehash: 9b7e464963471b0cad41c5b93d50507d0fa9bf96
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306512"
---
# <a name="data-sources"></a>Origini dati
*Un'origine dati* è semplicemente l'origine dei dati. Può essere un file, un particolare database in un DBMS o anche un feed di dati attivi. I dati potrebbero trovarsi sullo stesso computer del programma o su un altro computer da qualche parte in una rete. Ad esempio, un'origine dati potrebbe essere un sistema operativo Oracle DBMS in esecuzione su un sistema operativo ® sistema operativo, accessibile da Novell® Netware; un DBMS IBM DB2 accessibile tramite un gateway; una raccolta di file Xbase in una directory del server; o un file di database locale ® Access.  
  
 Lo scopo di un'origine dati è raccogliere tutte le informazioni tecniche necessarie per accedere ai dati - il nome del driver, l'indirizzo di rete, il software di rete e così via - in un'unica posizione e nasconderli all'utente. L'utente deve essere in grado di esaminare un elenco che include le retribuzioni, l'inventario e il personale, scegliere Retribuzioni dall'elenco e fare in modo che l'applicazione si connetta ai dati delle retribuzioni, il tutto senza sapere dove risiedono i dati delle retribuzioni o come l'applicazione ha ottenuto ad esso.  
  
 Il termine *origine dati* non deve essere confuso con termini simili. In questo manuale, *DBMS* o *database* si riferisce a un programma di database o motore. Viene effettuata un'ulteriore distinzione tra i *database desktop,* progettati per essere eseguiti su personal computer e spesso privi di supporto completo di SQL e transazioni, e i *database server,* progettati per essere eseguiti in una situazione client/server e caratterizzati da un motore di database autonomo e da un supporto completo di SQL e transazioni. *Database* si riferisce anche a una particolare raccolta di dati, ad esempio una raccolta di file Xbase in una directory o un database in SQL Server. È in genere equivalente al termine *catalogo,* utilizzato altrove in questo manuale o il termine *qualificatore* nelle versioni precedenti di ODBC.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Tipi di origini dati](../../odbc/reference/types-of-data-sources.md)  
  
-   [Uso delle origini dati](../../odbc/reference/using-data-sources.md)  
  
-   [Esempio di origine dati](../../odbc/reference/data-source-example.md)
