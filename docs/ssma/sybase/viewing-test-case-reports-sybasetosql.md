---
title: Visualizzazione dei report di Test Case (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Tester Component,Test Case Reports
ms.assetid: cb75d281-43ef-4f4a-b754-2c4ee3b62ae7
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 8a6d45f7e621f9b6516d4cc1211a8627174ae9b3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67944601"
---
# <a name="viewing-test-case-reports-sybasetosql"></a>Visualizzazione di report dei test case (SybaseToSQL)
Il Report di Test Case Mostra i risultati della verifica di test e informazioni generali del test. In caso di errore di test, viene visualizzate anche informazioni su tutti i dati non corrispondenti negli oggetti di verifica.  
  
## <a name="report-structure"></a>Struttura del report  
Nella parte superiore del report visualizzato queste statistiche:  
  
-   Numero totale di oggetti testati e il numero di oggetti per il quale il test ha avuto esito positivo.  
  
-   Il numero totale di tabelle di verifica e le chiavi esterne e il numero di tabelle e le chiavi esterne corrispondente correttamente.  
  
-   L'ora di inizio, ora di fine del test case e il tempo totale impiegato per l'esecuzione.  
  
Il resto del report mostra le informazioni in quattro categorie:  
  
**Errori dei prerequisiti**  
Mostra gli errori che si è verificato il **prerequisiti** passaggio. In genere, viene ignorato.  
  
**Inizializzazione**  
Mostra lo stato di esecuzione **Success** oppure **errore**.  
  
**Gli oggetti risultato del test**  
Confronto dei risultati (esito positivo o negativo) e le mancate corrispondenze tra Tester SSMA rilevati in caso di errore.  
  
**Finalizzazione**  
Mostra lo stato di esecuzione **Success** oppure **errore**.  
  
## <a name="see-also"></a>Vedere anche  
[Esecuzione di Test case &#40;SybaseToSQL&#41;](../../ssma/sybase/running-test-cases-sybasetosql.md)  
[Test di oggetti di Database migrati &#40;SybaseToSQL&#41;](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  
