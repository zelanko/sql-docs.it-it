---
title: Completamento della preparazione del Test Case (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Tester Component,Test Case Settings
ms.assetid: 8b2a49b0-4296-4f3f-9e56-323aa6a6fa8e
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: b31739bb4db23ccd2159ec8146ef857d7a5d66e5
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62631550"
---
# <a name="finishing-test-case-preparation-sybasetosql"></a>Completamento della preparazione del test case (SybaseToSQL)
Pagina finale della procedura guidata visualizza la descrizione del Test Case e le informazioni sugli oggetti coinvolti nel test. Inoltre, in questa pagina è possibile impostare il test di opzioni di esecuzione.  
  
Il **le informazioni di Test Case** sezione mostra il nome del Test Case e la descrizione.  
  
Il **oggetti Test** sezione contiene l'elenco di oggetti testati raggruppati per tipo di oggetto denominato.  
  
Il **Affected Objects da analizzare** sezione consente di visualizzare l'elenco di oggetti quali modifiche di dati devono essere confrontati dopo l'esecuzione di oggetti testati denominato.  
  
## <a name="test-case-settings"></a>Impostazioni di test Case  
Nel **delle impostazioni di Test Case** sezione è possibile impostare le opzioni di test l'esecuzione della seguente:  
  
### <a name="stop-test-execution-after-first-failure"></a>Arrestare l'esecuzione di test dopo il primo errore  
Specifica per interrompere l'esecuzione del test se si verifica un errore durante l'esecuzione di test.  
  
-   Se si sceglie **Sì**, l'esecuzione di interrompe di test se si verifica un errore.  
  
-   Se si sceglie **No**, l'esecuzione di test continua dopo un errore.  
  
### <a name="perform-data-rollback"></a>Eseguire il rollback di dati  
Abilitare il rollback automatico dei dati dopo l'esecuzione di test.  
  
-   Se si sceglie **Sì**, le modifiche ai dati andranno persi dopo l'esecuzione di test.  
  
-   Se si sceglie **No**, tutti i test verranno salvate le modifiche ai dati di esecuzione.  
  
### <a name="auxiliary-tables-saving-mode"></a>Tabelle ausiliarie modalità risparmio  
Definisce la modalità di salvataggio delle tabelle ausiliarie creato durante l'esecuzione di test. Vedere la descrizione delle tabelle ausiliarie nel [esecuzione di Test case &#40;SybaseToSQL&#41; ](../../ssma/sybase/running-test-cases-sybasetosql.md) argomento.  
  
-   Se si seleziona **salvare sempre**, verranno sempre archiviati dati di tabelle ausiliari per un uso successivo.  
  
-   Se si seleziona **se il confronto di tabella non è stato possibile salvare**, verranno archiviati i dati di tabelle ausiliari solo se si verifica un errore.  
  
-   Se si seleziona **sempre eliminare**, tabelle ausiliarie sempre eliminato dopo l'esecuzione di test.  
  
-   Se si seleziona **porre utente se non è stato possibile confronto tra le tabelle**, l'utente può selezionare le azioni necessarie se si verifica un errore.  
  
Fare clic sui **Finish** consente di salvare il Test Case preparata in [usando i repository di Test &#40;SybaseToSQL&#41;](../../ssma/sybase/using-test-repositories-sybasetosql.md).  
  
## <a name="see-also"></a>Vedere anche  
[Uso di repository Test &#40;SybaseToSQL&#41;](../../ssma/sybase/using-test-repositories-sybasetosql.md)  
[Esecuzione di Test case &#40;SybaseToSQL&#41;](../../ssma/sybase/running-test-cases-sybasetosql.md)  
[Test di oggetti di Database migrati &#40;SybaseToSQL&#41;](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  
