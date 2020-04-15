---
title: Funzioni di catalogo - Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- catalog functions [ODBC], about catalog functions
- data dictionary [ODBC]
- catalog functions [ODBC]
- functions [ODBC], catalog functions
ms.assetid: 81ba9453-c085-47c0-b411-90ca6a5ee428
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: eb28ec6f4ea299dae8737fc707fd53e4d102442d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305202"
---
# <a name="catalog-functions"></a>Funzioni di catalogo
Tutti i database hanno una struttura che descrive come i dati verranno archiviati nel database. Ad esempio, un database degli ordini cliente semplice potrebbe avere la struttura illustrata nella figura seguente, in cui le colonne ID vengono utilizzate per collegare le tabelle.  
  
 ![Struttura di un database semplice](../../../odbc/reference/develop-app/media/pr19.gif "Pr19 (informazioni in stato di")  
  
 Questa struttura, insieme ad altre informazioni quali i privilegi, viene memorizzata in un set di tabelle di sistema denominato catalogo del *database,* noto anche come *dizionario dei dati.*  
  
 Un'applicazione può individuare questa struttura tramite chiamate alle funzioni di *catalogo*. Le funzioni di catalogo restituiscono informazioni nei set di risultati e vengono in genere implementate tramite istruzioni **SELECT** sulle tabelle del catalogo. Un'applicazione potrebbe ad esempio richiedere un set di risultati contenente informazioni su tutte le tabelle del sistema o tutte le colonne di una particolare tabella.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Utilizzi dei dati del catalogo](../../../odbc/reference/develop-app/uses-of-catalog-data.md)  
  
-   [Funzioni di catalogo in ODBC](../../../odbc/reference/develop-app/catalog-functions-in-odbc.md)
