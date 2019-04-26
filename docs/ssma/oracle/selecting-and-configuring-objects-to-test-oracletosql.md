---
title: Selezione e configurazione degli oggetti da testare (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Selection of Objects to Test,Parameter Comparison Settings
ms.assetid: 29fb6542-5c1f-4b14-a822-87700beb7623
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: d568d1749cd54796072a108e438e448bf2a74578
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62626206"
---
# <a name="selecting-and-configuring-objects-to-test-oracletosql"></a>Selezione e configurazione degli oggetti da testare (OracleToSQL)
In questo passaggio si selezionano oggetti da testare e configurare le impostazioni per il confronto dei parametri di output procedure e funzioni, nonché i valori restituiti di funzioni.  
  
## <a name="selection-of-objects-to-test"></a>Selezione di oggetti a Test  
Nell'albero degli oggetti Oracle che si trova sul lato sinistro della finestra, selezionare gli oggetti che si vuole richiamare durante il processo di test. Visualizzare l'elenco completo degli oggetti testabili nel [Testing di oggetti di Database migrati &#40;OracleToSQL&#41; ](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md) argomento.  
  
Se Tester SSMA non supporta gli oggetti selezionati per il test, verrà visualizzato il collegamento con l'etichetta **alcuni oggetti selezionati contengono errori** sotto l'albero di oggetti. Fare clic su questo collegamento per visualizzare i motivi per cui non è possibile testare questi oggetti e per cancellare la selezione degli oggetti non corretti.  
  
Sul lato destro è possibile visualizzare le pagine diverse il **SQL** pagina Mostra la definizione dell'oggetto corrente. Il **parametri** pagina vengono elencati i parametri se l'oggetto è una stored procedure o una funzione. Il **proprietà** pagina Mostra le caratteristiche aggiuntive dell'oggetto. Vedere la descrizione della **parametro confronti** e **chiamare valori** le pagine seguenti.  
  
## <a name="parameter-comparison-settings"></a>Impostazioni di confronto dei parametri  
Stabilire le regole di confronto per i parametri output e restituire valori nel **confronti parametro** pagina. È possibile apportare le seguenti impostazioni.  
  
### <a name="use-during-test-comparisons"></a>Utilizzo durante i confronti tra Test  
Abilitare l'uso del parametro selezionato nel confronto dei risultati dei test.  
  
-   Se si sceglie **True**, SSMA confronterà il valore di output di questo parametro dopo avere eseguito la procedura in Oracle con il valore corrispondente in SQL Server.
  
-   Se si sceglie**False**, il parametro verrà escluso dalla verifica i risultati.  
  
### <a name="use-custom-scale"></a>Usare scala personalizzata  
Per i parametri di tipo di dati numerici, è possibile impostare una scala personalizzata per il confronto.  
  
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
È possibile specificare i valori di parametro di input nel **chiamare valori** pagina. Il **Aggiungi chiamata** pulsante Aggiunge una nuova chiamata con valori di parametri vuoto. Il **rimuovere le chiamate** pulsante consente di rimuovere la chiamata corrente.  
  
## <a name="next-step"></a>Passaggio successivo  
[Selezione e configurazione degli oggetti interessati &#40;OracleToSQL&#41;](../../ssma/oracle/selecting-and-configuring-affected-objects-oracletosql.md)  
  
## <a name="see-also"></a>Vedere anche  
[Test di oggetti di Database migrati &#40;OracleToSQL&#41;](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md)  
  
