---
title: ODBC e l'interfaccia della riga di comando Standard | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC [ODBC], CLI
- CLI [ODBC]
- CLI [ODBC], about CLI
- call-level interface [ODBC]
- call-level interface [ODBC], about call-level interface
ms.assetid: 79b9c268-16ac-4b80-b451-f9dcd8c02ca4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5485da176b9bd4aa7afca7afa088e6932d6f0d58
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63273313"
---
# <a name="odbc-and-the-standard-cli"></a>ODBC e l'interfaccia della riga di comando standard
Consente di allineare ODBC con le seguenti specifiche degli standard in grado di gestire con l'interfaccia a livello di chiamata (CLI). (Le funzioni ODBC sono un superset della ognuno di questi standard).  
  
-   La specifica di CAE Open Group "gestione dei dati: SQL a livello di chiamata Interface (CLI)"  
  
-   ISO/IEC 9075-3:1995 (E) Call-Level Interface (SQL/CLI)  
  
 In seguito a questa allineamento, si verifica quanto segue:  
  
-   Un'applicazione scritta per le specifiche di CLI ISO e Open Group funzionerà con un'applicazione ODBC 3. *x* driver o un driver conforme agli standard quando viene compilato con ODBC 3. *x* file di intestazione e collegata con ODBC 3. *x* librerie, e quando riesce ad accedere al driver tramite ODBC 3. *x* gestione Driver.  
  
-   Un driver scritto in base alle specifiche Open Group e ISO CLI funzionerà con un'applicazione ODBC 3 *. x* applicazione o un'applicazione conforme agli standard quando viene compilato con ODBC 3*x* i file di intestazione e collegato con ODBC 3 *. x* librerie, e quando l'applicazione può accedere al driver tramite ODBC 3*x* gestione Driver. (Per altre informazioni, vedere [applicazioni conformi agli standard e i driver](../../odbc/reference/develop-app/standards-compliant-applications-and-drivers.md).  
  
 Il livello di conformità di interfaccia Core comprende tutte le funzionalità di ISO CLI e tutte le funzionalità necessari della riga di comando gruppo aperto. Funzionalità opzionali della riga di comando di gruppo aprire vengono visualizzati nei livelli superiori della conformità di interfaccia. Poiché tutti ODBC 3. *x* i driver devono supportare le funzionalità di livello la conformità di interfaccia di Core, vengono soddisfatte le seguenti:  
  
-   Un database ODBC 3. *x* driver supporterà tutte le funzionalità usate da un'applicazione conforme agli standard.  
  
-   Un database ODBC 3. *x* applicazione usando solo le funzionalità di ISO CLI e le funzionalità necessari della riga di comando di gruppo aprire funzionerà con qualsiasi driver conforme agli standard.  
  
 Oltre alle specifiche di interfaccia a livello di chiamata contenute negli standard ISO/IEC e CLI di gruppo aprire ODBC implementa le funzionalità seguenti. (Alcune di queste funzionalità disponibili nelle versioni di ODBC prima ODBC 3. *x*.)  
  
-   Operazioni di recupero con più righe da una singola chiamata di funzione  
  
-   Associazione a una matrice di parametri  
  
-   Supporto per segnalibro inclusi recupero tramite segnalibro, a lunghezza variabile segnalibri e blocco di aggiornamento ed eliminazione dalle operazioni di segnalibro su righe non contigue  
  
-   Associazione per riga  
  
-   Offset di associazione  
  
-   Supporto per i batch di istruzioni SQL, in una stored procedure o come una sequenza di istruzioni SQL eseguite attraverso **SQLExecute** o **SQLExecDirect**  
  
-   Conteggio delle righe del cursore esatto o approssimativo  
  
-   Eliminazioni e operazioni di eliminazione e gli aggiornamenti in batch e aggiornamento posizionato dalla chiamata di funzione (**SQLSetPos**)  
  
-   Funzioni di catalogo che consentono di estrarre informazioni dallo schema di informazioni senza la necessità di viste degli schemi delle informazioni di supporto  
  
-   Sequenze di escape per gli outer join, funzioni scalari, valori letterali di data/ora, valori letterali intervallo e le stored procedure  
  
-   Librerie di codici traduzione  
  
-   La segnalazione di un driver a livello di conformità ANSI e supporto di SQL  
  
-   On demand il popolamento automatico del descrittore di parametri di implementazione  
  
-   Diagnostica avanzata e le matrici di stato di riga e di parametro  
  
-   Data/ora, intervallo, numerici o decimali e tipi di buffer dell'applicazione a 64 bit  
  
-   Esecuzione asincrona  
  
-   Supporto delle stored procedure, comprese le sequenze di escape, meccanismi di associazione di parametro di output e funzioni di catalogo  
  
-   Miglioramenti alle connessioni, incluso il supporto per gli attributi di connessione e l'esplorazione di attributo
