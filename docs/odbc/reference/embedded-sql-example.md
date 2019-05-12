---
title: Embedded SQL riportato di seguito | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL [ODBC], embedded SQL
- SQL statements [ODBC], embedded SQL
- embedded SQL [ODBC]
ms.assetid: b8a26e05-3c82-4c5f-8f01-9de0edb645e9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: eeab20c5385b02a874908cc941c1c69910efa228
ms.sourcegitcommit: 7a3243c45830cb3f49a7fa71c2991a9454fd6f5a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/11/2019
ms.locfileid: "65536666"
---
# <a name="embedded-sql-example"></a>Esempio di SQL incorporato
Il codice seguente è un programma SQL incorporato semplice, scritto in C. Il programma illustra le tecniche SQL molte, ma non tutti, l'oggetto incorporato. Il programma richiede l'immissione di un numero di ordine, recupera il numero di cliente, venditore e lo stato dell'ordine e visualizza le informazioni recuperate sullo schermo.  
  
```cpp  
int main() {  
   EXEC SQL INCLUDE SQLCA;  
   EXEC SQL BEGIN DECLARE SECTION;  
      int OrderID;         /* Employee ID (from user)         */  
      int CustID;            /* Retrieved customer ID         */  
      char SalesPerson[10]   /* Retrieved salesperson name      */  
      char Status[6]         /* Retrieved order status        */  
   EXEC SQL END DECLARE SECTION;  
  
   /* Set up error processing */  
   EXEC SQL WHENEVER SQLERROR GOTO query_error;  
   EXEC SQL WHENEVER NOT FOUND GOTO bad_number;  
  
   /* Prompt the user for order number */  
   printf ("Enter order number: ");  
   scanf_s("%d", &OrderID);  
  
   /* Execute the SQL query */  
   EXEC SQL SELECT CustID, SalesPerson, Status  
      FROM Orders  
      WHERE OrderID = :OrderID  
      INTO :CustID, :SalesPerson, :Status;  
  
   /* Display the results */  
   printf ("Customer number:  %d\n", CustID);  
   printf ("Salesperson: %s\n", SalesPerson);  
   printf ("Status: %s\n", Status);  
   exit();  
  
query_error:  
   printf ("SQL error: %ld\n", sqlca->sqlcode);  
   exit();  
  
bad_number:  
   printf ("Invalid order number.\n");  
   exit();  
}  
```  
  
 Tenere presente quanto segue su questo programma:  
  
-   **Ospitare variabili** vengono dichiarate le variabili di host in una sezione racchiusa tra il **BEGIN sezione dichiarare** e **sezioni finali dichiarare** parole chiave. Ogni nome di variabile host è preceduto da due punti (:) quando viene visualizzata in un'istruzione SQL. I due punti consente precompilatore distinguere tra le variabili di host e gli oggetti di database, ad esempio tabelle e colonne, che hanno lo stesso nome.  
  
-   **Tipi di dati** possono essere piuttosto diversi tipi di dati supportati da un sistema DBMS e un linguaggio host. Questo influisce sulle variabili host poiché essi svolgono un duplice ruolo. Un lato, le variabili di host sono variabili di programma, dichiarato e manipolato dalla istruzioni del linguaggio host. D'altra parte, vengono utilizzati in istruzioni SQL incorporate per recuperare i dati del database. Se è disponibile alcun tipo di linguaggio host che corrisponde a un tipo di dati DBMS, il sistema DBMS converte automaticamente i dati. Tuttavia, poiché ogni DBMS presenta regole e peculiarità associata al processo di conversione, i tipi di variabili host devono essere scelta attentamente.  
  
-   **Gestione degli errori** il sistema DBMS segnala errori di run-time per il programma di applicazioni tramite un'Area di comunicazioni SQL, o SQLCA. Nell'esempio di codice precedente, la prima istruzione SQL incorporata è SQLCA INCLUDONO. In questo modo il precompilatore per includere la struttura SQLCA nel programma. Ciò è necessario ogni volta che il programma elaborerà gli errori restituiti dal sistema DBMS. WHENEVER... Istruzione GOTO indica precompilatore per generare il codice di gestione degli errori che si verifica un'etichetta specifica quando un errore dei rami.  
  
-   **Singleton selezionare** l'istruzione utilizzata per restituire i dati è un'istruzione SELECT singleton; ovvero, restituisce solo una singola riga di dati. Di conseguenza, l'esempio di codice non dichiara o utilizzare i cursori.
