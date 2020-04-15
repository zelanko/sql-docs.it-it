---
title: Interfaccia di programmazione Standard Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC [ODBC], database access
- SQL [ODBC], database access
- database access [ODBC]
- standardizing database access [ODBC], programming interface
- programming interface standardization [ODBC]
ms.assetid: a2fa727e-51f2-4123-ae25-0ee28e611231
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c7767f113d0f70569ce253f0200cd35cb83915a4
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81279997"
---
# <a name="standard-programming-interface"></a>Interfaccia di programmazione standard
L'interfaccia di programmazione è forse il candidato più ovvio per la standardizzazione. Infatti, quando ODBC era in fase di sviluppo, ANSI e ISO già fornito standard per i moduli SQL e SQL incorporati. Sebbene non esistesseno standard per una CLI di database, il gruppo di accesso SQL - un consorzio industriale di fornitori di database - stava valutando se crearne uno; parti di ODBC in seguito divenne la base per il loro lavoro.  
  
 Uno dei requisiti per ODBC era che un singolo file binario dell'applicazione doveva funzionare con più DBS. È per questo motivo che ODBC non utilizza SQL incorporato o linguaggi di modulo. Anche se il linguaggio nei linguaggi SQL e modulo incorporati è standardizzato, ognuno è legato ai precompilatori specifici di DBMS. Pertanto, le applicazioni devono essere ricompilate per ogni DBMS e i file binari risultanti funzionano solo con un singolo DBMS. Mentre questo è accettabile per le applicazioni a basso volume che si trovano nel mondo dei minicomputer e dei mainframe, è inaccettabile nel mondo dei personal computer. In primo luogo, è un incubo logistico fornire più versioni di software ad alto volume e ridotto ai clienti; in secondo luogo, le applicazioni per personal computer spesso devono accedere a più DBS contemporaneamente.  
  
 D'altra parte, un'interfaccia a livello di chiamata può essere implementata tramite librerie, o driver di database, che risiedono su ogni computer locale; è necessario un driver diverso per ogni DBMS. Poiché i sistemi operativi moderni possono caricare tali librerie (ad esempio librerie a collegamento dinamico in Microsoft® sistema operativo Windows®) in fase di esecuzione, una singola applicazione può accedere ai dati da DBS diversi senza ricompilazione e può anche accedere ai dati da più database contemporaneamente. Man mano che diventano disponibili nuovi driver di database, gli utenti possono semplicemente installarli nei propri computer senza dover modificare, ricompilare o ricollegare le applicazioni di database. Inoltre, un'interfaccia a livello di chiamata era un buon candidato per ODBC perché Windows - la piattaforma per cui ODBC è stato originariamente sviluppato - già fatto ampio uso di tali librerie.
