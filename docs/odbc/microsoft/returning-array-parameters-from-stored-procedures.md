---
title: Restituzione di parametri di matrice da stored procedure | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- stored procedures [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], stored procedures
ms.assetid: 2018069b-da5d-4cee-a971-991897d4f7b5
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bc998dadc0e0c4a4bfe054bfd1d40296bc176393
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81292861"
---
# <a name="returning-array-parameters-from-stored-procedures"></a>Restituzione dei parametri di matrice dalle stored procedure
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Utilizzare invece il driver ODBC fornito da Oracle.  
  
 In Oracle 7,3 non esiste alcun modo per accedere a un tipo di record PL/SQL, tranne che per un programma PL/SQL. Se una procedura o una funzione in pacchetto ha un argomento formale definito come tipo di record PL/SQL, non è possibile associare tale argomento formale come parametro. Utilizzare il tipo di tabella PL/SQL in Microsoft ODBC driver for Oracle per richiamare parametri di matrice da routine contenenti le sequenze di escape corrette.  
  
 Per richiamare la procedura, usare la sintassi seguente:  
  
```  
{call  <package-name>.<proc-or-func>;  
(..., {resultset <max-records-requested> ,<formal-array-param_1>,;  
 <formal-array-param_2>,...,<formal-array-param_n> }, ... ) }  
```  
  
> [!NOTE]  
>  Il \<parametro> Max-record richiesto deve essere maggiore o uguale al numero di righe presenti nel set di risultati. In caso contrario, Oracle restituisce un errore che viene passato all'utente dal driver.  
>   
>  I record PL/SQL non possono essere usati come parametri di matrice. Ogni parametro di matrice può rappresentare solo una colonna di una tabella di database.  
  
 Nell'esempio seguente viene definito un pacchetto contenente due procedure che restituiscono set di risultati diversi, quindi vengono forniti due modi per restituire i set di risultati dal pacchetto.  
  
## <a name="package-definition"></a>Definizione del pacchetto:  
  
```  
CREATE OR REPLACE PACKAGE SimplePackage AS  
  
TYPE t_id is TABLE of  NUMBER(5)  
    INDEX BY BINARY_INTEGER;  
  
TYPE t_Course is TABLE of VARCHAR2(10)  
    INDEX BY BINARY_INTEGER;  
  
TYPE t_Dept is TABLE of VARCHAR2(5)  
    INDEX BY BINARY_INTEGER;  
  
PROCEDURE proc1  
   (  
   o_id             OUT    t_id,  
   ao_course       OUT    t_Course,  
   ao_dept         OUT    t_Dept  
   );  
  
TYPE t_pk1Type1 IS TABLE OF VARCHAR2(100) INDEX BY BINARY_INTEGER;  
TYPE t_pk1Type2 IS TABLE OF NUMBER INDEX BY BINARY_INTEGER;  
PROCEDURE proc2  
   (  
   i_Arg1         IN    NUMBER,  
   ao_Arg2         OUT   t_pk1Type1,  
   ao_Arg3         OUT   t_pk1Type2  
   );  
  
END SimplePackage;  
  
CREATE OR REPLACE PACKAGE BODY SimplePackage AS  
    PROCEDURE  proc1 ( o_id OUT t_id,  
    ao_course OUT t_Course, ao_dept OUT t_Dept   ) AS  
    BEGIN  
          o_id(1):= 200;  
          ao_course(1) :=  'M101';  
          ao_dept(1) :=  'EEE' ;  
  
          o_id(2) := 201;  
          ao_course(2) :=  'PHY320';  
          ao_dept(2) :=  'ECE' ;  
  
     END proc1;  
PROCEDURE proc2  
   (  
   i_Arg1         IN    NUMBER,  
   ao_Arg2         OUT   t_pk1Type1,  
   ao_Arg3         OUT   t_pk1Type2  
   )  
AS  
   i   NUMBER;  
BEGIN  
   FOR i IN 1 .. i_Arg1 LOOP  
      ao_Arg2(i) := 'Row Number ' || to_char(i);  
   END LOOP;  
   FOR i IN 1 .. i_Arg1 LOOP  
      ao_Arg3(i) := i;  
   END LOOP;  
END proc2;  
END SimplePackage;  
```  
  
#### <a name="to-invoke-procedure-proc1"></a>Per richiamare la procedura PROC1  
  
1.  Restituisce tutte le colonne in un singolo set di risultati:  
  
    ```  
    {call SimplePackage.Proc1( {resultset  3, o_id , ao_course, ao_dept  } ) }  
    ```  
  
2.  Restituisce ogni colonna come singolo set di risultati:  
  
    ```  
    {call SimplePackage.Proc1( {resultset 3, o_id},  {resultset 3, ao_course}, {resultset 3, ao_dept} ) }  
    ```  
  
     Restituisce tre set di risultati, uno per ogni colonna.  
  
#### <a name="to-invoke-procedure-proc2"></a>Per richiamare la procedura PROC2  
  
1.  Restituisce tutte le colonne in un singolo set di risultati:  
  
    ```  
    {call SimplePackage.Proc2( 5 , {resultset  5, ao_Arg2, ao_Arg3} ) }  
    ```  
  
2.  Restituisce ogni colonna come singolo set di risultati:  
  
    ```  
    {call SimplePackage.Proc2( 5 , {resultset 5, ao_Arg2}, {resultset 5, ao_Arg3} ) }  
    ```  
  
 Assicurarsi che le applicazioni recuperino tutti i set di risultati usando l'API [SQLMoreResults](../../odbc/microsoft/level-2-api-functions-odbc-driver-for-oracle.md) . Per ulteriori informazioni, fare riferimento a *ODBC Programmer ' s Reference*.  
  
> [!NOTE]  
>  Nel driver ODBC per Oracle versione 2,0, le funzioni Oracle che restituiscono matrici PL/SQL non possono essere utilizzate per restituire i set di risultati.
