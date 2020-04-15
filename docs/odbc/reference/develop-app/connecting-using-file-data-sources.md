---
title: Connessione tramite origini dati di file Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connecting to driver [ODBC], file data sources
- SQLDriverConnect function [ODBC], connecting using file data sources
- connecting to data source [ODBC], SQLDriverConnect
- connecting to driver [ODBC], SQLDriverConnect
- connecting to data source [ODBC], file data sources
- file data sources [ODBC]
ms.assetid: 3003f8c2-8be6-41cc-8d9c-612e9bd0f3ae
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8c752fc3b09c06c68dcc216cacac63744dc3101b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81287411"
---
# <a name="connecting-using-file-data-sources"></a>Connessione tramite origini dati dei file
Le informazioni di connessione per un'origine dati file vengono archiviate in un file DSN. Di conseguenza, la stringa di connessione può essere utilizzata ripetutamente da un singolo utente o condivisa tra più utenti se è installato il driver appropriato. Il file contiene un nome di driver (o un altro nome di origine dati nel caso di un'origine dati file non condivida) e, facoltativamente, una stringa di connessione che può essere utilizzata da **SQLDriverConnect**. Gestione Driver compila la stringa di connessione per la chiamata a **SQLDriverConnect** dalle parole chiave nel file DSN.  
  
 Un'origine dati su file consente a un'applicazione di specificare le opzioni di connessione senza dover compilare una stringa di connessione da utilizzare con **SQLDriverConnect**. L'origine dati file viene in genere creata specificando il **SAVEFILE** (parola chiave), che fa sì che Gestione Driver per salvare la stringa di connessione di output creata da una chiamata a **SQLDriverConnect** al file DSN. Tale stringa di connessione può essere utilizzata ripetutamente chiamando **SQLDriverConnect** con la parola chiave **FILEDSN.** Questo semplifica il processo di connessione e fornisce un'origine persistente della stringa di connessione.  
  
 Le origini dati file possono essere create anche chiamando **SQLCreateDataSource** nella DLL del programma di installazione. Le informazioni possono essere scritte nel file DSN chiamando **SQLWriteFileDSN**e lette dal file DSN chiamando **SQLReadFileDSN**; entrambe queste funzioni si trovano anche nella DLL del programma di installazione. Per informazioni sulla DLL del programma di installazione, vedere [Configurazione delle origini dati](../../../odbc/reference/install/configuring-data-sources.md).  
  
 Le parole chiave utilizzate per le informazioni di connessione si trovano nella sezione [ODBC] di un file DSN. Le informazioni minime che un file DSN condisabile avrebbe nella sezione [ODBC] sono la parola chiave DRIVER:  
  
```  
DRIVER = SQL Server  
```  
  
 Il file DSN condisabile contiene in genere una stringa di connessione, come indicato di seguito:The shareable .dsn file usually contains a connection string, as follows:  
  
```  
DRIVER = SQL Server  
UID = Larry  
DATABASE = MyDB  
```  
  
 Quando l'origine dati file non è condivisibile, il file DSN contiene solo una parola chiave **DSN.** Quando Gestione Driver viene inviato le informazioni in un'origine dati file non condivise, si connette come necessario all'origine dati indicata dalla parola chiave **DSN.** Un file DSN non condivida conterrà la seguente parola chiave:  
  
```  
DSN = MyDataSource  
```  
  
 La stringa di connessione utilizzata per un'origine dati su file è l'unione delle parole chiave specificate nel file DSN e delle parole chiave specificate nella stringa di connessione nella chiamata a **SQLDriverConnect**. Se una delle parole chiave nel file DSN è in conflitto con le parole chiave nella stringa di connessione, Gestione Driver decide quale valore della parola chiave deve essere utilizzato. Per ulteriori informazioni, vedere [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md).  
  
## <a name="see-also"></a>Vedere anche  
 [https://support.microsoft.com/kb/165866](https://support.microsoft.com/kb/165866)
