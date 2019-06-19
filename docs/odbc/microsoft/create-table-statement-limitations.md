---
title: TABELLA limitazioni dell'istruzione CREATE | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- CREATE TABLE statement limitations [ODBC]
- ODBC SQL grammar, CREATE TABLE statement limitations
ms.assetid: c5067855-20c9-456f-8d63-f375b4297f2e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f5eab1c3bf6891f10c897966035dced2ffdc10ba
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63232213"
---
# <a name="create-table-statement-limitations"></a>Limitazioni dell'istruzione CREATE TABLE
Quando viene utilizzato l'accesso Microsoft, Microsoft Excel o Paradoxdriver e la lunghezza di una colonna di testo o binari non è specificata (o è specificata come 0), verrà impostata la lunghezza della colonna su 255.  
  
 Quando viene usato il driver dBASE e la lunghezza di una colonna di testo o binari non è specificata (o è specificata come 0), verrà impostata la lunghezza della colonna e 254.  
  
 È supportato un massimo di 255 colonne.  
  
 Quando si usa il driver di Microsoft Excel in un Microsoft Excel provenienti 5.0, 7.0, o un'origine 97 dati, un foglio di lavoro non può essere creato con lo stesso nome di un foglio di lavoro che è stato eliminato in precedenza. Quando il driver di Microsoft Excel viene utilizzato per accedere a un foglio di lavoro versione 5.0, versione 7.0 o 97, un'istruzione DROP TABLE Cancella il foglio di lavoro, ma non elimina il nome del foglio di lavoro.  
  
 Quando viene usato il driver Paradox, non è possibile aggiungere colonne dopo aver definito un indice su una tabella. Se la prima colonna dell'elenco di argomenti di un'istruzione CREATE TABLE consente di creare un indice, una seconda colonna non può essere incluso nell'elenco di argomenti.
