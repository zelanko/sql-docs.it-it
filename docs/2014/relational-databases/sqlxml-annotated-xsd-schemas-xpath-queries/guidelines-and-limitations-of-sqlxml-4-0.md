---
title: Linee guida e limitazioni di SQLXML 4.0 | Documenti di Microsoft
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- SQLXML, about SQLXML
ms.assetid: fe433d30-90a1-421e-85c6-af13294dc18d
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: ffe5c84f4ac76fe339735b50843185d122b1cb70
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63127690"
---
# <a name="guidelines-and-limitations-of-sqlxml-40"></a>Linee guida e limitazioni di SQLXML 4.0
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Quando si utilizza SQLXML 4.0, tenere presenti le considerazioni seguenti:  
  
-   Il codice XML restituito come risultato della query non viene convalidato rispetto allo schema di mapping che lo ha generato.  
  
-   In SQLXML 4.0 sono inclusi i PROGID dipendenti e quelli indipendenti dalla versione. Per tutte le applicazioni di produzione è consigliabile utilizzare i PROGID dipendenti dalla versione. Questo aspetto è particolarmente importante perché SQLXML 4.0 non è completamente compatibile con le versioni precedenti. L'utilizzo di PROGID dipendenti dalla versione protegge da possibili errori di produzione quando si installano le versioni più recenti. Nelle diverse versioni il comportamento del programma può cambiare per molti motivi, ad esempio per correzioni di bug, per possibili modifiche di progettazione e così via. L'utilizzo di PROGID dipendenti dalla versione protegge da errori imprevisti quando si installano le versioni più recenti. Grazie ai PROGID dipendenti dalla versione, quando si installa una versione più recente, l'applicazione continuerà a funzionare senza errori. Se si decide di modificare i PROGID dipendenti dalla versione precedenti e di utilizzare quelli recenti di una versione più nuova, è necessario testare l'applicazione prima di inserirli in produzione. Ad esempio, le applicazioni che utilizzando i PROGID indipendenti dalla versione possono generare errori nello scenario seguente:  
  
     Si esegue un'applicazione che utilizza SQLXML 4.0 e i PROGID indipendenti dalla versione e si decide di installare un altro programma software. Questo programma potrebbe installare una versione precedente di SQLXML. L'applicazione può avere esito negativo poiché i PROGID indipendenti dalla versione dell'applicazione puntano ora alla versione precedente di SQLXML che può disporre o meno della caratteristica SQLXML utilizzata dall'applicazione.  
  
-   Se per qualsiasi motivo non vuole usare il provider SQLXMLOLEDB e invece si vuole usare il provider SQLOLEDB provider per le funzionalità SQLXML, impostare il **SQLXML Version** proprietà su "SQLXML.4.0".  
  
  
