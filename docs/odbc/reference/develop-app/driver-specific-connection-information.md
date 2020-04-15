---
title: Informazioni di connessione specifiche del driver Documenti Microsoft
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305792"
---
# <a name="driver-specific-connection-information"></a>Informazioni di connessione specifiche del driver
**SQLConnect** presuppone che il nome, l'ID utente e la password di un'origine dati siano sufficienti per connettersi a un'origine dati e che tutte le altre informazioni di connessione possano essere archiviate nel sistema. Questo non è spesso il caso. Ad esempio, un driver potrebbe essere necessario un ID utente e una password per accedere a un server e un ID utente e una password diversi per accedere a un DBMS. Poiché **SQLConnect** accetta un singolo ID utente e una password, ciò significa che l'altro ID utente e la password devono essere archiviati con le informazioni sull'origine dati nel sistema se **SQLConnect** deve essere utilizzato. Si tratta di una potenziale violazione della sicurezza e dovrebbe essere evitato a meno che la password non sia crittografata.  
  
 **SQLDriverConnect** consente al driver di definire una quantità arbitraria di informazioni di connessione nelle coppie parola chiave-valore della stringa di connessione. Si supponga, ad esempio, che un driver richieda un nome di origine dati, un ID utente e una password per il server e un ID utente e una password per il DBMS. Un programma personalizzato che utilizza sempre l'origine dati XY-Corp potrebbe richiedere all'utente ID e password e creare il seguente set di coppie parola chiave-valore, o stringa di *connessione,* da passare a **SQLDriverConnect**:  
  
> [!NOTE]  
>  Se ci si connette a un provider di origini `Trusted_Connection=yes` dati che supporta l'autenticazione di Windows, è necessario specificare al posto delle informazioni relative all'ID utente e alla password nella stringa di connessione.  
  
```  
DSN={MyDataSourceName};UID={MyUserID};PWD={MyServerPassword};UIDDBMS={MyDBMSUserID};PWDDBMS={MyDBMSUserPassword};  
```  
  
 La parola chiave **DSN** (Data Source Name) denomina l'origine dati, le parole **chiave UID** e **PWD** specificano l'ID utente e la password per il server, quindi le parole chiave **UIDDBMS** e **PWDDBMS** specificano l'ID utente e la password per il DBMS. Si noti che il punto e virgola finale è facoltativo. **SQLDriverConnect** analizza questa stringa; utilizza il nome dell'origine dati XY-Corp per recuperare informazioni di connessione aggiuntive dal sistema, ad esempio l'indirizzo del server; e accede al server e DBMS utilizzando gli ID utente e le password specificati.  
  
 Le coppie parola chiave-valore in **SQLDriverConnect** devono seguire determinate regole di sintassi. Le parole chiave e i relativi valori non devono contenere **[]{}(),;? caratteri \*** . Il valore della parola chiave **DSN** non può essere costituito solo da spazi vuoti e non deve contenere spazi vuoti iniziali. A causa della grammatica del Registro di sistema,\\le parole chiave e i nomi delle origini dati non possono contenere il carattere barra rovesciata ( ). Gli spazi non sono consentiti intorno al segno di uguale nella coppia parola chiave-valore.  
  
 La parola chiave **FILEDSN** può essere utilizzata in una chiamata a **SQLDriverConnect** per specificare il nome di un file contenente informazioni sull'origine dati (vedere [Connessione tramite origini dati file](../../../odbc/reference/develop-app/connecting-using-file-data-sources.md)più avanti in questa sezione). La parola chiave **SAVEFILE** può essere utilizzata per specificare il nome di un file DSN in cui verranno salvate le coppie parola chiave-valore di una connessione stabilita dalla chiamata a **SQLDriverConnect.** Per altre informazioni sulle origini dati su file, vedere la descrizione della funzione [SQLDriverConnect.For](../../../odbc/reference/syntax/sqldriverconnect-function.md) more information about file data sources, see the SQLDriverConnect function description.
