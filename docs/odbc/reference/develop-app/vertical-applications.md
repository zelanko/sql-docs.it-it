---
description: Applicazioni verticali
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a12be9247af3f273526dd08ee99ff7cc301af822
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421405"
---
# <a name="vertical-applications"></a>Applicazioni verticali
Le applicazioni verticali eseguono in genere un'attività ben definita in un singolo sistema DBMS. Un'applicazione Order entry, ad esempio, tiene traccia degli ordini in una società. Questo tipo di applicazioni in comune è che lo schema del database è in genere progettato dallo sviluppatore di applicazioni e, mentre l'applicazione potrebbe funzionare con una serie di DBMS diversi, funziona con un singolo sistema DBMS per un singolo cliente.  
  
 Poiché le applicazioni verticali richiedono in genere determinate funzionalità, ad esempio cursori scorrevoli o transazioni, supportano raramente tutti i DBMS. Al contrario, tendono a essere altamente interoperabili tra un set limitato di sistemi DBMS. In genere, gli sviluppatori di applicazioni verticali scelgono di supportare i sistemi DBMS che rappresentano una frazione elevata del mercato e ignorano il resto. Potrebbero anche scegliere di supportare driver specifici per i sistemi DBMS per ridurre i costi di test e supporto del prodotto.  
  
 Poiché le applicazioni verticali possono supportare un set noto di DBMS, a volte contengono codice specifico del driver o DBMS. Tuttavia, tale codice è più adatto al minimo perché richiede tempo aggiuntivo per la manutenzione.
