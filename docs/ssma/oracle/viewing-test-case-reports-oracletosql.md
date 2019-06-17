---
title: Visualizzazione dei report di Test Case (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 8da14323-9dd6-4019-bf79-3e8b972a9bc0
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 2d40fd986c68968680bcd39821d762101723b87b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63283639"
---
# <a name="viewing-test-case-reports-oracletosql"></a>Visualizzazione di report dei test case (OracleToSQL)
Il Report di Test Case Mostra i risultati della verifica di test e informazioni generali del test. In caso di errore di test, viene visualizzate anche informazioni su tutti i dati non corrispondenti negli oggetti di verifica.  
  
## <a name="report-structure"></a>Struttura del report  
Nella parte superiore del report visualizzato queste statistiche:  
  
-   Numero totale di oggetti testati e il numero di oggetti per il quale il test ha avuto esito positivo.  
  
-   Il numero totale di tabelle di verifica e le chiavi esterne e il numero di tabelle e le chiavi esterne corrispondente correttamente.  
  
-   L'ora di inizio, ora di fine del test case e il tempo totale impiegato per l'esecuzione.  
  
Il resto del report mostra le informazioni in quattro categorie:  
  
**Errori dei prerequisiti**  
Mostra gli errori che si è verificato il **passaggio dei prerequisiti.** In genere, viene ignorato.  
  
**Inizializzazione**  
Mostra lo stato di esecuzione **Success** oppure **errore**.  
  
**Gli oggetti risultato del test**  
Confronto dei risultati (esito positivo o negativo) e le mancate corrispondenze tra Tester SSMA rilevati in caso di errore.  
  
**Finalizzazione**  
Mostra lo stato di esecuzione **Success** oppure **errore**.  
  
## <a name="see-also"></a>Vedere anche  
[Esecuzione di Test case &#40;OracleToSQL&#41;](../../ssma/oracle/running-test-cases-oracletosql.md)  
[Test di oggetti di Database migrati &#40;OracleToSQL&#41;](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md)  
  
