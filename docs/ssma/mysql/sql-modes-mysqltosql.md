---
title: Modalità SQL (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: d840ee51-b863-4e77-84aa-37d3f094bfed
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 6965d67b6dae484b3fa72f215446682f9aa6760c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63028368"
---
# <a name="sql-modes-mysqltosql"></a>Modalità SQL (MySQLToSQL)
SSMA per MySQL può funzionare in modalità diverse di SQL che è possibile applicare queste modalità in modo diverso per diversi client.  
  
Modalità di definizione della sintassi SQL che devono supportare MySQL e controlla il tipo di convalida dei dati che deve eseguire. Questo rende più semplice per usare MySQL in ambienti diversi e usare MySQL con SQL Server.  
  
## <a name="sql-modes-grid"></a>Griglia di modalità SQL:  
  
-   SQL modalità griglia a livello di radice contiene le colonne seguenti: **Nome modalità SQL**, **caricato modalità SQL**, e **modalità SQL efficace**.  
  
-   Griglia di modalità SQL al database categoria, Database, tabella categoria, categoria di istruzioni, categoria di viste, tabella, vista, funzioni, procedure, funzione definita dall'utente e a livello di oggetto evento contiene le colonne seguenti: **Nome modalità SQL**, **ereditato modalità SQL**, e **modalità SQL efficace**.  
  
-   Griglia di modalità SQL a livello di Stored Procedure, funzione archiviati e Trigger contiene le colonne seguenti: **Nome della modalità SQL**, **modalità SQL originale**, e **modalità SQL efficace**.  
  
> [!NOTE]  
> Modalità gruppo verrà visualizzata in grassetto, sotto la colonna 'SQL modalità Name'.  
  
## <a name="loaded-sql-modes"></a>Modalità SQL caricato  
Queste sono le modalità di SQL, che vengono IMPOSTATE a livello di sessione o radice. Le modalità SQL una volta caricate nel database di destinazione non può essere modificate o modificate.  
  
## <a name="inherited-sql-modes"></a>Modalità SQL ereditati  
Queste sono le modalità di SQL, che vengono ereditate dal nodo padre corrispondente.  
  
Ad eccezione di categorie di funzioni, procedure, categoria di eventi e trigger, tali modalità SQL sono presenti tutti i livelli (oggetto di database, tabella categoria, categoria di istruzioni, viste categoria, tabella, vista, funzioni, procedure, funzione definita dall'utente ed evento).  
  
> [!NOTE]  
> Selezionando il **eredita da padre** casella di controllo ereditate modalità SQL può essere ereditata dal nodo padre. Per impostazione predefinita, questa casella di controllo rimanga selezionata.  
  
## <a name="original-sql-modes"></a>Modalità SQL originale  
Queste sono le modalità di SQL presenti solo i livelli funzioni, Procedure e Trigger.  
  
> [!NOTE]  
> Selezionando il **Usa originale** controllare, le modalità di SQL che sono stati utilizzati originariamente nella funzione corrispondente o è possibile utilizzare procedure o trigger. Per impostazione predefinita, questa casella di controllo rimanga selezionata.  
  
## <a name="effective-sql-modes"></a>Modalità SQL efficace  
Modalità SQL effettivo può essere definita a vari livelli nel modo seguente:  
  
-   **A livello di sessione:**  
  
    1.  Tutte le modalità di SQL caricato può essere chiamate, "Modalità efficace di SQL".  
  
    2.  A questo livello, le modalità SQL effettive possono essere direttamente e in modo esplicito modificate.  
  
    3.  La modalità SQL effettivo che viene impostata in modo esplicito non vengono riportata come modalità di caricamento di SQL e infine viene applicata all'oggetto.  
  
-   **A livello di funzione o procedura o del trigger:**  
  
    1.  Tutte le modalità SQL originale può essere chiamato, "Modalità efficace di SQL".  
  
    2.  A questo livello, la modalità SQL effettiva può essere esplicitamente modificata solo quando la **Usa originale** casella di controllo è deselezionata.  
  
    3.  La modalità SQL effettivo che viene impostata in modo esplicito non vengono riportata come modalità SQL originale e infine viene applicata all'oggetto.  
  
-   **In nodi diversi da quelli a livello di funzione o procedura o del trigger:**  
  
    1.  Tutte le modalità di SQL ereditata può essere chiamate, "Modalità efficace di SQL".  
  
    2.  A questo livello, la modalità SQL effettiva può essere esplicitamente modificata solo quando la **eredita da padre** casella di controllo è deselezionata.  
  
    3.  La modalità di SQL effettivo che viene impostata in modo esplicito non vengono riportata come modalità SQL ereditata e infine viene applicata all'oggetto.  
  
