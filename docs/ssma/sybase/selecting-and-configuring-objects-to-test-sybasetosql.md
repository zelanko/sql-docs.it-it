---
title: Selezione e configurazione degli oggetti da testare (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Tester Component,Parameter Comparision Setting
- Tester Component,Selecting Objects
ms.assetid: 89c23aad-bfee-4917-bc16-175288390ac0
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 2951d4c3bf1eae73ffd066d796b0e3dda4d28cf6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68020959"
---
# <a name="selecting-and-configuring-objects-to-test-sybasetosql"></a>Selezione e configurazione degli oggetti da testare (SybaseToSQL)
In questo passaggio si selezionano oggetti da testare e configurare le impostazioni per il confronto dei parametri di output procedure e funzioni, nonché i valori restituiti di funzioni.  
  
## <a name="selection-of-objects-to-test"></a>Selezione di oggetti a Test  
Nell'albero degli oggetti Sybase che si trova sul lato sinistro della finestra, selezionare gli oggetti che si vuole richiamare durante il processo di test. Visualizzare l'elenco completo degli oggetti testabili nel [Testing di oggetti di Database migrati &#40;SybaseToSQL&#41; ](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md) argomento.  
  
Se Tester SSMA non supporta gli oggetti selezionati per il test, verrà visualizzato il collegamento con l'etichetta **alcuni oggetti selezionati contengono errori** sotto l'albero di oggetti. Fare clic su questo collegamento per visualizzare i motivi per cui non è possibile testare questi oggetti e per cancellare la selezione degli oggetti non corretti.  
  
Sul lato destro è possibile visualizzare le pagine diverse il **SQL** pagina Mostra la definizione dell'oggetto corrente. Nel **precedenti SQL** e **Post SQL** pagine è possono specificare script eseguiti prima e dopo la chiamata dell'avvio di oggetto test. Si tratta di può essere utile quando l'oggetto richiede ulteriori oggetti tali tabelle temporanee o cursori. Il **parametri** pagina vengono elencati i parametri se l'oggetto è una stored procedure o una funzione. Il **proprietà** pagina Mostra le caratteristiche aggiuntive dell'oggetto. Vedere la descrizione della **parametri Comparsions** e **chiamare valori** le pagine seguenti.  
  
## <a name="parameter-comparison-settings"></a>Impostazioni di confronto dei parametri  
Stabilire le regole di confronto per i parametri output e restituire valori nel **confronto tra i parametri** pagina. È possibile apportare le seguenti impostazioni.  
  
### <a name="use-during-comparisons"></a>Utilizzo durante i confronti  
Abilitare l'uso del parametro selezionato nel confronto dei risultati dei test.  
  
-   Se si sceglie **True**, SSMA confronterà il valore di output di questo parametro dopo avere eseguito la procedura in Sybase con il valore corrispondente in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   Se si sceglie**False**, il parametro verrà escluso dalla verifica i risultati.  
  
### <a name="use-custom-scale"></a>Usare scala personalizzata  
Per i parametri del tipo di dati numerici di lunghezza fissa e approssimativo, è possibile impostare una scala personalizzata per il confronto.  
  
-   Se si sceglie **True**, i valori numerici saranno arrotondati in base al **confronto scalabilità** valore prima che vengano confrontati.  
  
-   Se si sceglie**False**, il confronto numerico sarà esatto.  
  
### <a name="comparing-scale"></a>Confronto di scalabilità  
È disponibile solo se il **Use Custom Scale** opzione è impostata su **True**. Questa è la precisione per un confronto numerico.  
  
### <a name="date-time-comparing"></a>Confronto tra ora di date  
Definisce come data/ora vengono confrontati i valori.  
  
-   Se si seleziona **Confronta intero data**, verrà eseguito un confronto completo di valori da entrambe le piattaforme.  
  
-   Se si seleziona **confrontare solo data**, ora parte verrà ignorata.  
  
-   Se si seleziona **confrontare solo ora**, la data parte verrà ignorata.  
  
-   Se si seleziona **ignorare millisecondi**, i risultati verranno confrontato con un massimo di secondi.  
  
-   Se si seleziona **ignorare Date e i millisecondi**, il risultato sarà confrontate solo da parte dell'ora e ignorando le parti frazionarie di un secondo.  
  
### <a name="ignore-strings-case"></a>Ignora maiuscole/minuscole stringhe  
Controlla distinzione maiuscole/minuscole del confronto.  
  
-   Se si sceglie **True**, il confronto sarà maiuscole e minuscole.  
  
-   Se si sceglie **False**, il confronto sarà distinzione maiuscole / minuscole.  
  
### <a name="ignore-trailing-spaces"></a>Ignora spazi finali  
Controlla gli spazi finali come vengono considerati durante il confronto.  
  
-   Se si sceglie **True**, le stringhe confrontate saranno tagliati a destra prima di confrontare.  
  
-   Se si sceglie **False**, le stringhe confrontate conserverà lo spazio vuoto finale.  
  
## <a name="specify-input-values-for-procedures-and-functions-call-values"></a>Specificare i valori di input per le procedure e funzioni (chiamare valori)  
È possibile specificare i valori di parametro di input nel **chiamare valori** pagina. Il **Aggiungi chiamata** pulsante Aggiunge una nuova chiamata con valori di parametri vuoto. Il **rimuovere chiamare** pulsante consente di rimuovere la chiamata corrente.  
  
## <a name="next-step"></a>Passaggio successivo  
[Selezione e configurazione degli oggetti interessati &#40;SybaseToSQL&#41;](../../ssma/sybase/selecting-and-configuring-affected-objects-sybasetosql.md)  
  
## <a name="see-also"></a>Vedere anche  
[Test di oggetti di Database migrati &#40;SybaseToSQL&#41;](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  
