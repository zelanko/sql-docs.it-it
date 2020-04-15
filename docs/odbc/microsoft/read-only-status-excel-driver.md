---
title: Stato di sola lettura (Driver di Excel) Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- read-only status for Excel driver [ODBC]
- Excel driver [ODBC], read-only status
ms.assetid: ef5d773b-4f8f-4005-b985-84b53d8e9f9b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: eb585d4712b6cac5e09b65ee8e13604763cd0164
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304022"
---
# <a name="read-only-status-excel-driver"></a>Stato di sola lettura (driver Excel)
Quando viene utilizzato il driver di Microsoft Excel, le tabelle dell'origine dati vengono aperte in sola lettura per impostazione predefinita e possono essere aperte da un solo utente alla volta. Anche se le tabelle hanno lo stato di sola lettura, tuttavia, le applicazioni possono eseguire inserimenti e aggiornamenti per le tabelle di Microsoft Excel.  
  
 Quando un'applicazione esegue un comando Salva con nome sui dati di Microsoft Excel tramite il driver di Microsoft Excel, l'applicazione deve creare una nuova tabella e inserire i dati da salvare nella nuova tabella. Inserisce il risultato in un'aggiunta alla tabella. Non è possibile eseguire altre operazioni sulla tabella finché non viene chiusa e riaperta. Una volta chiusa la tabella, non è possibile eseguire alcun inserimento successivo perché la tabella è quindi una tabella di sola lettura.  
  
 È possibile aggiornare i valori quando si utilizza il driver di Microsoft Excel, ma non è possibile eliminare una riga da una tabella basata su un foglio di calcolo di Microsoft Excel, pertanto gli aggiornamenti non vengono considerati ufficialmente supportati dal driver di Microsoft Excel.
