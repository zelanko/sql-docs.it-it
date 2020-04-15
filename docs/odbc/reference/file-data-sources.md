---
title: Origini di dati dei file Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], file
- file data sources [ODBC]
ms.assetid: db245c80-981a-4638-bd03-69d04bc67af0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0661aa424a7a118b8b12f4bf8433987ff83bd788
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306652"
---
# <a name="file-data-sources"></a>Origini dati di file
*Le origini dati sui* file vengono archiviate in un file e consentono di utilizzare ripetutamente le informazioni di connessione da parte di un singolo utente o di condivisione tra più utenti. Quando viene utilizzata un'origine dati file, Gestione Driver effettua la connessione all'origine dati utilizzando le informazioni in un file DSN. Questo file può essere manipolato come qualsiasi altro file. Un'origine dati su file non dispone di un nome di origine dati, così come un'origine dati macchina, e non è registrata per un utente o un computer.  
  
 Un'origine dati su file semplifica il processo di connessione, perché il file DSN contiene la stringa di connessione che altrimenti sarebbe necessario compilare per una chiamata alla funzione **SQLDriverConnect.** Un altro vantaggio del file .dsn è che può essere copiato su qualsiasi computer, in modo che origini dati identiche possono essere utilizzati da molti computer, purché siano installati il driver appropriato. Un'origine dati su file può anche essere condivisa dalle applicazioni. Un'origine dati file condisa può essere inserita in una rete e utilizzata contemporaneamente da più applicazioni.  
  
 Un file DSN può anche essere inutilizzabile. Un file DSN non condisabile si trova su un singolo computer e punta a un'origine dati del computer. Esistono principalmente origini dati su file non condivise per consentire la facile conversione delle origini dati macchina in origini dati su file in modo che un'applicazione possa essere progettata per funzionare esclusivamente con le origini dati su file. Quando Gestione Driver viene inviato le informazioni in un'origine dati file non condivida, si connette in base alle esigenze all'origine dati del computer a cui punta il file DSN.  
  
 Per altre informazioni sulle origini dati su file, vedere [Connessione tramite origini dati file](../../odbc/reference/develop-app/connecting-using-file-data-sources.md)o descrizione della funzione [SQLDriverConnect.For](../../odbc/reference/syntax/sqldriverconnect-function.md) more information about file data sources, see Connecting Using File Data Sources o the SQLDriverConnect function description.
