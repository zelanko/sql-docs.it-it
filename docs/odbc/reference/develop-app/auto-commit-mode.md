---
title: Modalità di commit automatico Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- rolling back transactions [ODBC]
- auto-commit mode [ODBC]
- transactions [ODBC], commit modes
- committing transactions [ODBC]
- commit modes [ODBC]
- transactions [ODBC], rolling back
ms.assetid: c8de5b60-d147-492d-b601-2eeae8511d00
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6f19053eec7a48eba7a51425b01744f3acd10015
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285111"
---
# <a name="auto-commit-mode"></a>Modalità autocommit
*In modalità di commit automatico,* ogni operazione di database è una transazione di cui viene eseguito il commit quando viene eseguito. Questa modalità è adatta per molte transazioni reali costituite da una singola istruzione SQL. Non è necessario delimitare o specificare il completamento di queste transazioni. Nei database senza supporto delle transazioni, la modalità di commit automatico è l'unica modalità supportata. In tali database, viene eseguito il commit delle istruzioni quando vengono eseguite e non è possibile eseguirne il rollback. sono quindi sempre in modalità di commit automatico.  
  
 Se il sistema DBMS sottostante non supporta le transazioni in modalità di commit automatico, il driver può emularle eseguendo manualmente il commit di ogni istruzione SQL durante l'esecuzione.  
  
 Se un batch di istruzioni SQL viene eseguito in modalità di commit automatico, è specifico dell'origine dati quando viene eseguito il commit delle istruzioni nel batch. È possibile eseguirle durante l'esecuzione o nel suo insieme dopo l'esecuzione dell'intero batch. Alcune origini dati possono supportare entrambi questi comportamenti e possono fornire un modo per selezionare uno o gli altri. In particolare, se si verifica un errore nel mezzo del batch, è specifico dell'origine dati se viene eseguito il commit o il rollback delle istruzioni già eseguite. Pertanto, le applicazioni interoperabili che utilizzano i batch e ne richiedono il commit o il rollback nel suo complesso devono eseguire i batch solo in modalità di commit manuale.
