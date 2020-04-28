---
title: Informazioni di connessione specifiche del driver | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLConnect function [ODBC], driver-specific connection information
- connecting to driver [ODBC], SQLConnect
- SQLDriverConnect function [ODBC], driver specific connection information
- connecting to data source [ODBC], SQLDriverConnect
- connecting to driver [ODBC], SQLDriverConnect
- connecting to data source [ODBC], SQLConnect
- connecting to driver [ODBC], driver-specific information
ms.assetid: 3748758a-f16a-4f3b-9c40-06f2e300704e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 16c8c5fc4fd3ac63aa3613b41e530446dffec118
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305792"
---
# <a name="driver-specific-connection-information"></a>Informazioni di connessione specifiche del driver
**SQLConnect** presuppone che il nome dell'origine dati, l'ID utente e la password siano sufficienti per connettersi a un'origine dati e che tutte le altre informazioni di connessione possano essere archiviate nel sistema. Spesso non è il caso. Un driver, ad esempio, potrebbe richiedere un ID utente e una password per accedere a un server e un ID utente e una password diversi per accedere a un sistema DBMS. Poiché **SQLConnect** accetta un ID utente e una password singoli, questo significa che l'altro ID utente e la password devono essere archiviati con le informazioni sull'origine dati nel sistema, se è necessario utilizzare **SQLConnect** . Si tratta di una potenziale violazione della sicurezza e deve essere evitata a meno che la password non sia crittografata.  
  
 **SQLDriverConnect** consente al driver di definire una quantità arbitraria di informazioni di connessione nelle coppie parola chiave/valore della stringa di connessione. Si supponga, ad esempio, che un driver richieda un nome dell'origine dati, un ID utente e una password per il server e un ID utente e una password per il sistema DBMS. Un programma personalizzato che usa sempre l'origine dati XYZ Corp potrebbe richiedere all'utente ID e password e compilare il seguente set di coppie parola chiave/valore, o *stringa di connessione,* da passare a **SQLDriverConnect**:  
  
> [!NOTE]  
>  Se ci si connette a un provider dell'origine dati che supporta l'autenticazione di Windows, `Trusted_Connection=yes` è necessario specificare al posto delle informazioni sull'ID utente e sulla password nella stringa di connessione.  
  
```  
DSN={MyDataSourceName};UID={MyUserID};PWD={MyServerPassword};UIDDBMS={MyDBMSUserID};PWDDBMS={MyDBMSUserPassword};  
```  
  
 La parola chiave **DSN** (Data Source Name) denomina l'origine dati, le parole chiave **UID** e **pwd** specificano l'ID utente e la password per il server e le parole chiave **UIDDBMS** e **PWDDBMS** specificano l'ID utente e la password per il sistema DBMS. Si noti che il punto e virgola finale è facoltativo. **SQLDriverConnect** analizza la stringa; Usa il nome dell'origine dati Corp XYZ per recuperare informazioni aggiuntive sulla connessione dal sistema, ad esempio l'indirizzo del server. e accedono al server e al sistema DBMS usando gli ID utente e le password specificati.  
  
 Le coppie parola chiave/valore in **SQLDriverConnect** devono seguire determinate regole di sintassi. Le parole chiave e i relativi valori non devono contenere **[{}] (),;? = \*! @** caratteri. Il valore della parola chiave **DSN** non può essere costituito solo da spazi vuoti e non deve contenere spazi vuoti iniziali. Grazie alla grammatica del registro di sistema, le parole chiave e i nomi delle origini\\dati non possono contenere il carattere barra rovesciata (). Gli spazi non sono consentiti intorno al segno di uguale nella coppia parola chiave/valore.  
  
 La parola chiave **FileDSN** può essere usata in una chiamata a **SQLDriverConnect** per specificare il nome di un file che contiene informazioni sull'origine dati. vedere [connessione tramite origini dati file](../../../odbc/reference/develop-app/connecting-using-file-data-sources.md), più avanti in questa sezione. La parola chiave **SaveFile** può essere usata per specificare il nome di un file con estensione DSN in cui verranno salvate le coppie parola chiave/valore di una connessione riuscita effettuata dalla chiamata a **SQLDriverConnect** . Per ulteriori informazioni sulle origini dati dei file, vedere la descrizione della funzione [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) .
