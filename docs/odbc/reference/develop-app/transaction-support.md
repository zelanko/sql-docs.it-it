---
title: Supporto delle transazioni | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a0b5e33f94c5452a2062f7c18339f27c8da73fa9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68086062"
---
# <a name="transaction-support"></a>Supporto delle transazioni
Il livello di supporto per le transazioni è definito dal driver. ODBC è progettato per essere implementato in un singolo utente o in un database desktop che non è necessario gestire più aggiornamenti ai dati. Inoltre, alcuni database che supportano le transazioni eseguono questa operazione solo per le istruzioni DML (Data Manipulation Language) di SQL. Esistono restrizioni o una semantica di transazione speciale relativa all'utilizzo di DDL (Data Definition Language) quando è attiva una transazione. Ovvero è possibile che esista il supporto delle transazioni per più aggiornamenti simultanei alle tabelle, ma non per modificare il numero e la definizione delle tabelle durante una transazione.  
  
 Un'applicazione determina se le transazioni sono supportate, se DDL può essere incluso in una transazione e qualsiasi effetto speciale dell'inclusione di DDL in una transazione, chiamando **SQLGetInfo** con l'opzione SQL_TXN_CAPABLE. Per ulteriori informazioni, vedere la descrizione della funzione [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) .  
  
 Se il driver non supporta le transazioni, ma l'applicazione ha la possibilità (usando un'API diversa da ODBC) per bloccare e sbloccare i dati, le applicazioni possono ottenere il supporto delle transazioni bloccando e sbloccando i record e le tabelle in base alle esigenze. Per implementare l'esempio di trasferimento di account, l'applicazione blocca i record per entrambi gli account, copia i valori correnti, addebita il primo account, accredita il secondo account e sblocca i record. Se una procedura non riesce, l'applicazione reimposterà gli account usando le copie.  
  
 Anche le origini dati che supportano le transazioni potrebbero non essere in grado di supportare più di una transazione alla volta all'interno di un determinato ambiente. Le applicazioni chiamano **SQLGetInfo** con l'opzione SQL_MULTIPLE_ACTIVE_TXN per determinare se un'origine dati può supportare transazioni attive simultanee in più di una connessione nello stesso ambiente. Poiché è presente una transazione per connessione, questo è interessante solo per le applicazioni che dispongono di più connessioni alla stessa origine dati.
