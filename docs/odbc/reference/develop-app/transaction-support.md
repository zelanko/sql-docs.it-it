---
title: Supporto per le transazioni Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- transactions [ODBC], degree of support
ms.assetid: d56e1458-8da2-4d73-a777-09e045c30a33
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a5b9d731d12329a4ef663b1ea66cdc59a0b153fa
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81297979"
---
# <a name="transaction-support"></a>Supporto delle transazioni
Il grado di supporto per le transazioni è definito dal driver. ODBC è progettato per essere implementato in un database desktop o utente singolo che non è necessario gestire più aggiornamenti ai propri dati. Inoltre, alcuni database che supportano le transazioni lo fanno solo per le istruzioni DML (Data Manipulation Language) di SQL; esistono restrizioni o una semantica di transazione speciale per quanto riguarda l'utilizzo di DDL (Data Definition Language) quando una transazione è attiva. In altre parte, potrebbe essere disponibile il supporto delle transazioni per più aggiornamenti simultanei alle tabelle, ma non per la modifica del numero e della definizione delle tabelle durante una transazione.  
  
 Un'applicazione determina se le transazioni sono supportate, se DDL può essere incluso in una transazione ed eventuali effetti speciali dell'inclusione di DDL in una transazione, chiamando **SQLGetInfo** con l'opzione SQL_TXN_CAPABLE. Per altre informazioni, vedere la descrizione della funzione [SQLGetInfo.For](../../../odbc/reference/syntax/sqlgetinfo-function.md) more information, see the SQLGetInfo function description.  
  
 Se il driver non supporta le transazioni ma l'applicazione ha la possibilità (utilizzando un'API diversa da ODBC) per bloccare e sbloccare i dati, le applicazioni possono ottenere il supporto delle transazioni bloccando e sbloccando record e tabelle in base alle esigenze. Per implementare l'esempio di trasferimento di account, l'applicazione blocca i record per entrambi gli account, copia i valori correnti, addebita il primo conto, accredita il secondo account e sblocca i record. Se alcuni passaggi non sono riusciti, l'applicazione reimposterà gli account utilizzando le copie.  
  
 Anche le origini dati che supportano le transazioni potrebbero non essere in grado di supportare più di una transazione alla volta all'interno di un particolare ambiente. Le applicazioni chiamano **SQLGetInfo** con l'opzione SQL_MULTIPLE_ACTIVE_TXN per determinare se un'origine dati può supportare transazioni attive simultanee su più connessioni nello stesso ambiente. Poiché esiste una transazione per connessione, questo è interessante solo per le applicazioni che dispongono di più connessioni alla stessa origine dati.
