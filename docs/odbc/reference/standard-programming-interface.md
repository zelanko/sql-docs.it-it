---
title: Interfaccia di programmazione standard | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a241ea92af6c1273039cc45daab232a1fbe763a3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68081845"
---
# <a name="standard-programming-interface"></a>Interfaccia di programmazione standard
L'interfaccia di programmazione è probabilmente il candidato più ovvio per la standardizzazione. Infatti, durante lo sviluppo di ODBC, ANSI e ISO hanno già fornito gli standard per i moduli SQL e SQL incorporati. Sebbene non esistano standard per un'interfaccia della riga di comando del database, il gruppo di accesso SQL, un consorzio di settore di fornitori di database, stava valutando se crearne uno. in seguito, le parti di ODBC diventeranno la base del proprio lavoro.  
  
 Uno dei requisiti per ODBC era che un singolo file binario dell'applicazione doveva funzionare con più DBMS. Per questo motivo, ODBC non utilizza le lingue incorporate di moduli o SQL. Sebbene il linguaggio nei linguaggi SQL e modulo incorporati sia standardizzato, ognuno è associato a compilatori specifici del sistema DBMS. Pertanto, le applicazioni devono essere ricompilate per ogni DBMS e i file binari risultanti funzionano solo con un singolo sistema DBMS. Sebbene sia accettabile per le applicazioni con volumi limitati presenti in minicomputer e nei mondi mainframe, è inaccettabile nel mondo personal computer. In primo luogo, si tratta di un incubo logistico per la distribuzione di più versioni di software a elevato volume e compattato ai clienti; in secondo luogo, le applicazioni personal computer spesso devono accedere a più DBMS simultaneamente.  
  
 D'altra parte, un'interfaccia a livello di chiamata può essere implementata tramite le librerie o i driver del database che risiedono in ogni computer locale; per ogni DBMS è necessario un driver diverso. Poiché i sistemi operativi moderni possono caricare tali librerie, ad esempio le librerie a collegamento dinamico sul sistema operativo Microsoft® Windows®, in fase di esecuzione, una singola applicazione può accedere ai dati da DBMS diversi senza ricompilarli e può accedere anche ai dati da più database contemporaneamente. Man mano che diventano disponibili nuovi driver di database, gli utenti possono semplicemente installarli nei propri computer senza dover modificare, ricompilare o ricollegare le applicazioni di database. Inoltre, un'interfaccia a livello di chiamata era un buon candidato per ODBC perché Windows, la piattaforma per cui ODBC è stato originariamente sviluppato, ha già utilizzato in modo estensivo tali librerie.
