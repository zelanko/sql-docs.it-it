---
title: Esempio di SQL incorporato | Microsoft Docs
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
ms.openlocfilehash: 966962bdda79a57e83a0bce06b9254267efb474c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68068663"
---
# <a name="embedded-sql-example"></a>Esempio di SQL incorporato
Il codice seguente è un semplice programma SQL incorporato, scritto in C. Nel programma sono illustrate molte, ma non tutte, le tecniche di SQL embedded. Il programma richiede all'utente un numero di ordine, recupera il numero del cliente, il venditore e lo stato dell'ordine e visualizza le informazioni recuperate sullo schermo.  
  
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
  
 Tenere presente quanto segue per questo programma:  
  
-   **Variabili host** Le variabili host sono dichiarate in una sezione racchiusa tra le parole chiave della sezione **BEGIN DECLARE** e **end Declare** . Ogni nome di variabile host è preceduto dai due punti (:) Quando viene visualizzato in un'istruzione SQL incorporata. I due punti consentono al precompilatore di distinguere tra variabili host e oggetti di database, ad esempio tabelle e colonne, che hanno lo stesso nome.  
  
-   **Tipi di dati** I tipi di dati supportati da un sistema DBMS e un linguaggio host possono essere molto diversi. Ciò influiscono sulle variabili host perché svolgono un ruolo doppio. Da un lato, le variabili host sono variabili di programma, dichiarate e modificate dalle istruzioni del linguaggio host. D'altra parte, vengono usati nelle istruzioni SQL incorporate per recuperare i dati del database. Se non è presente alcun tipo di linguaggio host corrispondente a un tipo di dati DBMS, il sistema DBMS converte automaticamente i dati. Tuttavia, poiché ogni DBMS ha regole e idiosincrasie proprie associate al processo di conversione, è necessario scegliere con attenzione i tipi di variabili host.  
  
-   **Gestione degli errori** Il sistema DBMS segnala gli errori di run-time al programma applicazioni tramite un'area di comunicazione SQL, o SQLCA. Nell'esempio di codice precedente, la prima istruzione SQL incorporata è INCLUDE SQLCA. Indica al precompilatore di includere la struttura SQLCA nel programma. Questa operazione è necessaria ogni volta che il programma elabora gli errori restituiti dal sistema DBMS. Oggetto quando... L'istruzione GOTO indica al precompilatore di generare codice di gestione degli errori che si dirama a un'etichetta specifica quando si verifica un errore.  
  
-   **Selezione singleton** L'istruzione utilizzata per restituire i dati è un'istruzione SELECT singleton; ovvero restituisce solo una singola riga di dati. Pertanto, l'esempio di codice non dichiara né utilizza i cursori.
