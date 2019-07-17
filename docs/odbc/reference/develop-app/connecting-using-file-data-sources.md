---
title: Connessione tramite origini dati dei File | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: aa340c64f6eb92d803d8918bc99ecf112b19f1e7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68083112"
---
# <a name="connecting-using-file-data-sources"></a>Connessione tramite origini dati dei file
Informazioni di connessione per un'origine dati file viene archiviate in un file DSN. Di conseguenza, la stringa di connessione usata più volte da un singolo utente o condiviso da più utenti se hanno il driver appropriato installato. Il file contiene un nome del driver (o un altro nome dell'origine dati nel caso di un'origine dati file condivisibili) e, facoltativamente, una stringa di connessione che può essere utilizzata da **SQLDriverConnect**. Gestione Driver compila la stringa di connessione per la chiamata a **SQLDriverConnect** tra le parole chiave nel file DSN.  
  
 Un'origine dati file consente a un'applicazione specificare le opzioni di connessione senza dover compilare una stringa di connessione per l'uso con **SQLDriverConnect**. File dell'origine dati in genere viene creato specificando il **SAVEFILE** parola chiave, che fa sì che Gestione Driver per salvare la stringa di connessione di output creata da una chiamata a **SQLDriverConnect** per il file DSN. Stringa di connessione può essere utilizzata più volte chiamando **SQLDriverConnect** con il **FILEDSN** (parola chiave). Questo semplifica il processo di connessione e fornisce un'origine permanente della stringa di connessione.  
  
 Origini dati dei file possono anche essere create chiamando **SQLCreateDataSource** nel programma di installazione DLL. È possibile scrivere informazioni nel file DSN mediante la chiamata **SQLWriteFileDSN**e letti dal file DSN chiamando **SQLReadFileDSN**; entrambe queste funzioni sono riportate anche nella DLL di installazione. Per informazioni sul programma di installazione DLL, vedere [configurazione di origini dati](../../../odbc/reference/install/configuring-data-sources.md).  
  
 Le parole chiave utilizzate per le informazioni di connessione sono disponibili nella sezione [ODBC] di un file DSN. Le informazioni minime che potrebbe avere un file DSN condivisibile nella sezione [ODBC] sono la parola chiave DRIVER:  
  
```  
DRIVER = SQL Server  
```  
  
 Il file DSN condivisibile contiene in genere una stringa di connessione, come indicato di seguito:  
  
```  
DRIVER = SQL Server  
UID = Larry  
DATABASE = MyDB  
```  
  
 Quando l'origine dati di file sia condivisibile, il file DSN contiene solo un **DSN** (parola chiave). Quando Gestione Driver viene inviata le informazioni in un'origine dati file condivisibile, si connette se necessario, per l'origine dati indicata tramite le **DSN** (parola chiave). Un file DSN condivisibili contiene la parola chiave seguente:  
  
```  
DSN = MyDataSource  
```  
  
 La stringa di connessione usata per un'origine dati file rappresenta l'unione tra le parole chiave specificate nel file DSN e le parole chiave specificate nella stringa di connessione nella chiamata a **SQLDriverConnect**. Se la parola chiave nel file DSN in conflitto con le parole chiave nella stringa di connessione, gestione Driver decide quale valore parola chiave deve essere utilizzato. Per altre informazioni, vedere [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md).  
  
## <a name="see-also"></a>Vedere anche  
 [https://support.microsoft.com/kb/165866](https://support.microsoft.com/kb/165866)
