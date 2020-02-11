---
title: Modalità autocommit | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a8a02d58309f123e6cc8b29d41188ba5bebb26f7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67909896"
---
# <a name="auto-commit-mode"></a>Modalità autocommit
*In modalità autocommit,* ogni operazione di database è una transazione di cui viene eseguito il commit al momento dell'esecuzione. Questa modalità è adatta per molte transazioni reali costituite da una singola istruzione SQL. Non è necessario delimitare o specificare il completamento di queste transazioni. Nei database senza supporto delle transazioni, la modalità di commit automatico è l'unica modalità supportata. In tali database, viene eseguito il commit delle istruzioni quando vengono eseguite e non è possibile eseguirne il rollback; sono pertanto sempre in modalità autocommit.  
  
 Se il sistema DBMS sottostante non supporta le transazioni in modalità autocommit, il driver può emularle eseguendo manualmente il commit di ogni istruzione SQL durante l'esecuzione.  
  
 Se un batch di istruzioni SQL viene eseguito in modalità autocommit, si tratta di un'origine dati specifica quando viene eseguito il commit delle istruzioni nel batch. È possibile eseguirne il commit durante l'esecuzione o nel suo complesso dopo l'esecuzione dell'intero batch. Alcune origini dati possono supportare entrambi questi comportamenti e possono fornire un modo per selezionarne una o le altre. In particolare, se si verifica un errore all'interno del batch, è specifica dell'origine dati se viene eseguito il commit o il rollback delle istruzioni già eseguite. Pertanto, le applicazioni interoperative che usano batch e richiedono il commit o il rollback nel suo complesso devono eseguire batch solo in modalità di commit manuale.
