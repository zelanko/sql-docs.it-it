---
title: Applicazioni verticali | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], vertical applications
- vertical applications [ODBC]
- interoperability [ODBC], levels
ms.assetid: d50ea3e6-7a9e-4fb6-8cd8-1d429d2f7b3c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6d0ed7a5f488765b56b2af0688ca14361590ab44
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68022114"
---
# <a name="vertical-applications"></a>Applicazioni verticali
Applicazioni verticali eseguono in genere un'attività ben definita con un singolo DBMS. Ad esempio, un'applicazione di immissione dell'ordine tiene traccia degli ordini in un'azienda. Ciò che questi tipi di applicazioni hanno in comune è che lo schema del database viene in genere creato dallo sviluppatore dell'applicazione e, mentre l'applicazione potrebbe funzionare con un numero di diversi DBMS, funziona con un DBMS singolo per un singolo cliente.  
  
 Poiché applicazioni verticali richiedono in genere determinate funzionalità, ad esempio cursori scorrevoli o le transazioni, raramente supportano tutti i DBMS. Al contrario, tendono a essere estremamente interoperativi tra un set limitato di DBMS. In genere, gli sviluppatori di applicazioni verticali scelgono di supportare tali DBMS che rappresentano una vasta gamma di mercato e ignorare il resto. Può anche scegliere di supporto di driver specifici per tali DBMS per ridurre i test e i costi di supporto del prodotto.  
  
 Poiché le applicazioni verticali possono supportare un set noto di DBMS, a volte contengono codice specifico del driver o specifici del DBMS. Tuttavia, tale codice è preferibile mantenere al minimo perché richiede tempo aggiuntivo necessario per mantenere.
