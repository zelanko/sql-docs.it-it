---
title: Completamento della preparazione del test case (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 32f38713-7ae4-48d3-980d-74cadc8545a0
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: bc5693c71ac6061f12ee90386b3c135a45a14e09
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "68266070"
---
# <a name="finishing-test-case-preparation-oracletosql"></a>Completamento della preparazione del test case (OracleToSQL)
Nella pagina finale della procedura guidata vengono visualizzate la descrizione del test case e le informazioni sugli oggetti che coinvolgono il test. Inoltre, in questa pagina è possibile impostare le opzioni di esecuzione dei test.  
  
Nella sezione **informazioni sul test case** vengono visualizzati il nome e la descrizione del test case.  
  
La sezione **oggetti selezionati da testare** contiene l'elenco denominato di oggetti testati raggruppati per tipo di oggetto.  
  
La sezione **oggetti interessati dalla verifica che verrà analizzata** consente di visualizzare l'elenco denominato di oggetti che devono essere confrontati con le modifiche dei dati dopo l'esecuzione di oggetti testati.  
  
## <a name="test-case-settings"></a>Impostazioni test case  
Nella sezione **impostazioni test case** è possibile impostare le opzioni di test di esecuzione seguenti:  
  
### <a name="stop-test-execution-after-first-failure"></a>Interrompi esecuzione del test dopo il primo errore  
Specifica di interrompere il test se si verifica un errore durante l'esecuzione del test.  
  
-   Se si sceglie **Sì**, l'esecuzione del test si interrompe se si verifica un errore.  
  
-   Se si sceglie **No**, l'esecuzione del test continuerà dopo un errore.  
  
### <a name="perform-data-rollback"></a>Eseguire il rollback dei dati  
Abilita il rollback automatico dei dati dopo l'esecuzione del test.  
  
-   Se si sceglie **Sì**, le modifiche ai dati andranno perse dopo l'esecuzione del test.  
  
-   Se si sceglie **No**, verranno salvate tutte le modifiche apportate ai dati di esecuzione dei test.  
  
### <a name="auxiliary-tables-saving-mode"></a>Modalità di salvataggio delle tabelle ausiliarie  
Definisce la modalità di salvataggio per le tabelle ausiliarie create durante l'esecuzione del test. Vedere la descrizione delle tabelle ausiliarie nell'argomento [esecuzione di test case &#40;OracleToSQL&#41;](../../ssma/oracle/running-test-cases-oracletosql.md) .  
  
-   Se si seleziona **Always save**, i dati della tabella ausiliaria verranno sempre archiviati per un uso successivo.  
  
-   Se si seleziona **Salva se il confronto tra tabelle non è riuscito**, i dati della tabella ausiliaria verranno archiviati solo se si verifica un errore.  
  
-   Se si seleziona **Always Delete**, le tabelle ausiliarie verranno sempre eliminate dopo l'esecuzione del test.  
  
-   Se si seleziona **Richiedi utente se il confronto tra tabelle non è riuscito**, l'utente può selezionare l'azione necessaria se si verifica un errore.  
  
Fare clic sul pulsante **fine** per salvare il test case preparato in [utilizzando i repository di test (OracleToSQL)](https://msdn.microsoft.com/f941cce4-d3e3-4aeb-a88a-4f101a97a9f4).  
  
## <a name="see-also"></a>Vedere anche  
[Uso di repository di test &#40;OracleToSQL&#41;](../../ssma/oracle/using-test-repositories-oracletosql.md)  
[Esecuzione di test case &#40;OracleToSQL&#41;](../../ssma/oracle/running-test-cases-oracletosql.md)  
[Test di oggetti di database migrati &#40;OracleToSQL&#41;](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md)  
  
