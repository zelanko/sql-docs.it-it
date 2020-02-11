---
title: Applicazioni | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- off-the-shelf applications [ODBC]
- ODBC architecture [ODBC], applications
- shrink-wrapped applications [ODBC]
- application development [ODBC], types
- custom applications [ODBC]
- virtual applications [ODBC]
- generic applications [ODBC]
ms.assetid: 39d6461f-0d24-4b7d-a723-843ade15ad73
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f15b5e8eb6eb7c63ab771030f0c31e8c9ff92724
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68135681"
---
# <a name="applications"></a>APPLICAZIONI
Un' *applicazione* è un programma che chiama l'API ODBC per accedere ai dati. Sebbene sia possibile utilizzare molti tipi di applicazioni, la maggior parte di essi rientrano in tre categorie, che vengono utilizzate come esempi in questa guida.  
  
-   **Applicazioni generiche** Queste sono anche denominate applicazioni con incapsulamento ridotto o applicazioni non ridotte. Le applicazioni generiche sono progettate per funzionare con un'ampia gamma di sistemi DBMS diversi. Gli esempi includono un foglio di calcolo o un pacchetto di statistiche che usa ODBC per importare i dati per un'ulteriore analisi e un elaboratore di testo che usa ODBC per ottenere una lista di distribuzione da un database.  
  
     Una sottocategoria importante di applicazioni generiche è costituita da ambienti di sviluppo di applicazioni, ad esempio PowerBuilder o Microsoft® Visual Basic®. Sebbene le applicazioni costruite con questi ambienti funzioneranno probabilmente solo con un singolo sistema DBMS, l'ambiente deve funzionare con più DBMS.  
  
     Ciò che tutte le applicazioni generiche hanno in comune è che sono altamente interoperabili tra DBMS e che devono usare ODBC in modo relativamente generico. Per ulteriori informazioni sull'interoperabilità, vedere [scelta di un livello di interoperabilità](../../odbc/reference/develop-app/choosing-a-level-of-interoperability.md).  
  
-   **Applicazioni verticali** Le applicazioni verticali eseguono un solo tipo di attività, ad esempio l'immissione degli ordini o il rilevamento dei dati di produzione, e utilizzano uno schema di database controllato dallo sviluppatore dell'applicazione. Per un cliente specifico, l'applicazione funziona con un singolo sistema DBMS. Ad esempio, una piccola azienda potrebbe utilizzare l'applicazione con dBase, mentre una grande azienda potrebbe utilizzarla con Oracle.  
  
     L'applicazione utilizza ODBC in modo tale che l'applicazione non sia associata a un DBMS, sebbene possa essere legata a un numero limitato di DBMS che forniscono funzionalità simili. Lo sviluppatore di applicazioni può quindi vendere l'applicazione indipendentemente dal sistema DBMS. Le applicazioni verticali sono interoperative quando vengono sviluppate, ma vengono talvolta modificate per includere il codice noninteroperable dopo che il cliente ha scelto un sistema DBMS.  
  
-   **Applicazioni personalizzate** Le applicazioni personalizzate vengono usate per eseguire un'attività specifica in un'unica azienda. Ad esempio, un'applicazione in una grande azienda potrebbe raccogliere dati di vendita da diverse divisioni (ognuno dei quali utilizza un DBMS diverso) e creare un singolo report. Viene utilizzato ODBC perché si tratta di un'interfaccia comune che consente ai programmatori di dover apprendere più interfacce. Tali applicazioni non sono in genere interoperative e vengono scritte in DBMS e driver specifici.  
  
 Diverse attività sono comuni a tutte le applicazioni, indipendentemente dal modo in cui usano ODBC. Insieme, definiscono in gran parte il flusso di qualsiasi applicazione ODBC. Le attività sono:  
  
-   Selezione di un'origine dati e connessione.  
  
-   Invio di un'istruzione SQL per l'esecuzione.  
  
-   Recupero dei risultati, se presenti.  
  
-   Errori di elaborazione.  
  
-   Esecuzione del commit o del rollback della transazione che include l'istruzione SQL.  
  
-   Disconnessione dall'origine dati.  
  
 Poiché la maggior parte delle operazioni di accesso ai dati viene eseguita con SQL, l'attività principale per la quale le applicazioni utilizzano ODBC è l'invio di istruzioni SQL e il recupero dei risultati, se presenti, generati da tali istruzioni. Altre attività per le quali le applicazioni utilizzano ODBC includono l'individuazione e la regolazione delle funzionalità del driver e l'esplorazione del catalogo del database.
