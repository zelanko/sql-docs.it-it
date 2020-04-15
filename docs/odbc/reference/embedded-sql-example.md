---
title: Esempio di Embedded SQL - Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 39ec504c423817c6a3e11bc954555b201b8b09c6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81294172"
---
# <a name="embedded-sql-example"></a>Esempio di SQL incorporato
Il codice seguente è un semplice programma SQL incorporato, scritto in C.The following code is a simple embedded SQL program, written in C. Il programma illustra molte, ma non tutte, le tecniche SQL incorporate. Il programma richiede all'utente un numero di ordine, recupera il numero cliente, il venditore e lo stato dell'ordine e visualizza le informazioni recuperate sullo schermo.  
  
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
  
-   **Variabili host** Le variabili host vengono dichiarate in una sezione racchiusa dalle parole chiave **BEGIN DECLARE SECTION** e END DECLARE **SECTION.** Ogni nome di variabile host è preceduto da due punti (:) quando viene visualizzato in un'istruzione SQL incorporata. I due punti consentono al precompilatore di distinguere tra variabili host e oggetti di database, ad esempio tabelle e colonne, che hanno lo stesso nome.  
  
-   **Tipi di dati** I tipi di dati supportati da un DBMS e da un linguaggio host possono essere molto diversi. Ciò influisce sulle variabili host perché svolgono un ruolo doppio. Da un lato, le variabili host sono variabili di programma, dichiarate e manipolate dalle istruzioni del linguaggio host. D'altra parte, vengono utilizzati nelle istruzioni SQL incorporate per recuperare i dati del database. Se non esiste alcun tipo di linguaggio host che corrisponde a un tipo di dati DBMS, il DBMS converte automaticamente i dati. Tuttavia, poiché ogni DBMS ha le proprie regole e idiosincrasie associate al processo di conversione, i tipi di variabile host devono essere scelti con attenzione.  
  
-   **Gestione degli errori** Il DBMS segnala gli errori di runtime al programma applicazioni tramite un'area di comunicazione SQL o SQLCA. Nell'esempio di codice precedente, la prima istruzione SQL incorporata è INCLUDE SQLCA. Ciò indica al precompilatore di includere la struttura SQLCA nel programma. Questa operazione è necessaria ogni volta che il programma elaborerà gli errori restituiti dal DBMS. L'WHENEVER... L'istruzione GOTO indica al precompilatore di generare il codice di gestione degli errori che si dirama in un'etichetta specifica quando si verifica un errore.  
  
-   **Select Singleton** L'istruzione utilizzata per restituire i dati è un'istruzione SELECT singleton. vale a dire, restituisce solo una singola riga di dati. Pertanto, l'esempio di codice non dichiara né utilizza i cursori.
