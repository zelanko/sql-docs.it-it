---
title: Combinare condizioni quando OR ha la precedenza (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- search conditions [SQL Server], combining
- precedence [SQL Server], Criteria pane
- search criteria [SQL Server], combining conditions
- combining search conditions
- OR operator
ms.assetid: b30f5ac9-25e7-4163-80ed-44e4bccb455d
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 5757d32093ab6547092d967f1d9fcf8c94323cf0
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/06/2019
ms.locfileid: "65093351"
---
# <a name="combine-conditions-when-or-has-precedence-visual-database-tools"></a>Combinare condizioni quando OR ha la precedenza (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Per collegare condizioni con OR e attribuire loro la precedenza sulle condizioni collegate con AND, è necessario ripetere la condizione AND per ogni condizione OR.  
  
Per trovare, ad esempio, i dipendenti che hanno lavorato nell'azienda per più di cinque anni con mansioni di basso livello o che sono in pensione, occorre creare una query con tre condizioni, un'unica condizione collegata ad altre due mediante AND:  
  
-   I dipendenti assunti da più di cinque anni e  
  
-   I dipendenti con livello pari a 100 o il cui stato sia "R" (retired, pensionato).  
  
Nella procedura riportata di seguito viene illustrato come creare questo tipo di query nel riquadro Criteri.  
  
### <a name="to-combine-conditions-when-or-has-precedence"></a>Per combinare condizioni quando OR ha la precedenza  
  
1.  Nel [riquadro Criteri](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md)aggiungere le colonne di dati da includere nella ricerca. Per eseguire la ricerca sulla stessa colonna utilizzando due o più condizioni collegate con AND, è necessario aggiungere alla griglia il nome della colonna di dati per ciascun valore da includere nella ricerca.  
  
2.  Creare le condizioni da collegare con OR immettendo la prima nella colonna **Filtro** della griglia e la seconda (e le successive) in colonne **OR…** separate. Ad esempio, per collegare con OR condizioni per l'esecuzione della ricerca nelle colonne `job_lvl` e `status` , immettere `= 100` nella colonna **Filtro** per `job_lvl` e `= 'R'` nella colonna **OR...** per `status`.  
  
    Immettendo questi valori nella griglia, verrà prodotta la seguente clausola WHERE nell'istruzione del riquadro SQL:  
  
    ```  
    WHERE (job_lvl = 100) OR (status = 'R')  
    ```  
  
3.  Creare la condizione AND immettendola una volta per ciascuna condizione OR. Collocare ogni voce nella stessa colonna della griglia in cui è presente la corrispondente condizione OR. Ad esempio, per aggiungere una condizione AND che consenta di eseguire la ricerca nella colonna `hire_date` e sia valida per entrambe le condizioni OR, immettere `< '1/1/91'` nella colonna Criteri e nella colonna **OR...** .  
  
    Immettendo questi valori nella griglia, verrà prodotta la seguente clausola WHERE nell'istruzione del riquadro SQL:  
  
    ```  
    WHERE (job_lvl = 100) AND   
      (hire_date < '01/01/91' ) OR  
      (status = 'R') AND   
      (hire_date < '01/01/91' )  
    ```  
  
    > [!TIP]  
    > Per ripetere una condizione AND, aggiungerla una volta, quindi usare i comandi **Taglia** e **Incolla** del menu **Modifica** per ripeterla per altre condizioni OR.  
  
La clausola WHERE creata da Progettazione query e Progettazione viste è equivalente alla clausola WHERE riportata di seguito, in cui le parentesi consentono di specificare la precedenza di OR su AND:  
  
```  
WHERE (job_lvl = 100 OR status = 'R') AND  
   (hire_date < '01/01/91')  
```  
  
> [!NOTE]  
> Se le condizioni di ricerca vengono immesse nel formato indicato sopra nel [riquadro SQL](../../ssms/visual-db-tools/sql-pane-visual-database-tools.md)e la query viene poi modificata nel riquadro Diagramma o Criteri, in Progettazione query e Progettazione viste l'istruzione SQL verrà ricreata per assicurare la corrispondenza tra il formato in uso e la condizione AND distribuita esplicitamente a entrambe le condizioni OR.  
  
## <a name="see-also"></a>Vedere anche  
[Convenzioni per la combinazione delle condizioni di ricerca nel riquadro Criteri &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/conventions-combine-search-conditions-in-criteria-pane-visual-db-tools.md)  
[Specifica dei criteri di ricerca &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)  
  
