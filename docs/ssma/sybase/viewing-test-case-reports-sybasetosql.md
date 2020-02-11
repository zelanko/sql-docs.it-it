---
title: Visualizzazione di report dei test case (SybaseToSQL) | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67944601"
---
# <a name="viewing-test-case-reports-sybasetosql"></a>Visualizzazione di report dei test case (SybaseToSQL)
Il report test case Mostra i risultati della verifica di test e le informazioni generali sul test. In caso di errore del test, vengono visualizzate anche le informazioni relative a eventuali dati non corrispondenti negli oggetti verificati.  
  
## <a name="report-structure"></a>Struttura del report  
Nella parte superiore del report vengono visualizzate le statistiche seguenti:  
  
-   Il numero totale di oggetti testati e il numero di oggetti per i quali il test ha avuto esito positivo.  
  
-   Il numero totale di tabelle e chiavi esterne verificate e il numero di tabelle e chiavi esterne correttamente corrispondenti.  
  
-   L'ora di inizio, l'ora di fine dell'test case e il tempo totale impiegato per l'esecuzione.  
  
Il resto del report Mostra le informazioni in quattro categorie:  
  
**Errori dei prerequisiti**  
Mostra tutti gli errori che si sono verificati durante il passaggio dei **prerequisiti** . Normalmente viene ignorato.  
  
**Inizializzazione**  
Mostra lo stato di esecuzione in caso di **esito positivo** o **negativo**.  
  
**Risultato oggetti di test**  
Un confronto dei risultati (esito positivo o negativo) e le mancate corrispondenze rilevate da SSMA tester in caso di errore.  
  
**Finalizzazione**  
Mostra lo stato di esecuzione in caso di **esito positivo** o **negativo**.  
  
## <a name="see-also"></a>Vedere anche  
[Esecuzione di test case &#40;SybaseToSQL&#41;](../../ssma/sybase/running-test-cases-sybasetosql.md)  
[Test di oggetti di database migrati &#40;SybaseToSQL&#41;](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  
