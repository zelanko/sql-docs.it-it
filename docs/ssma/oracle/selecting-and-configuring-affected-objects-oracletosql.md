---
title: Selezione e configurazione di oggetti (OracleToSQL) interessati | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Columns Comparison Settings
- Selection of Affected Objects
ms.assetid: 545eeda2-9829-4187-a858-619a96b4b71d
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: fbd151b0fa8682865e44615c22a9fdd7577014ea
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62626525"
---
# <a name="selecting-and-configuring-affected-objects-oracletosql"></a>Selezione e configurazione degli oggetti interessati (OracleToSQL)
In questa pagina è possibile selezionare tabelle e le chiavi esterne, le modifiche in cui devono essere confrontate quando SSMA verifica i risultati dell'esecuzione per gli oggetti scelto nel passaggio precedente. Inoltre, è possibile personalizzare i parametri di verifica.  
  
## <a name="selection-of-affected-objects"></a>Selezione degli oggetti interessati  
Nell'albero degli oggetti Oracle che si trova sul lato sinistro della finestra, selezionare le tabelle e le chiavi esterne, le modifiche in cui devono essere confrontate per identici.  
  
Se non è possibile verificare il Tester di SSMA uno di questi oggetti, verrà visualizzato il collegamento con l'etichetta **alcuni oggetti selezionati contengono errori** sotto l'albero di oggetti. Fare clic su questo collegamento per visualizzare i motivi per cui non è possibile confrontare questi oggetti e per cancellare la selezione degli oggetti non corretti.  
  
## <a name="table"></a>Tabella  
Scheda della tabella contiene la visualizzazione griglia della tabella selezionata. La griglia contiene le informazioni seguenti relative alla tabella selezionata:  
  
-   Nome colonna  
  
-   Tipo di dati  
  
-   Precisione  
  
-   Scala  
  
-   Regola  
  
-   Impostazione predefinita  
  
-   identità  
  
-   Ammette valori Null  
  
## <a name="sql"></a>Sql  
Scheda SQL contiene la tabella"Crea" SQL della tabella selezionata.  
  
## <a name="data"></a>Dati  
Scheda dati consente di visualizzare i dati presenti nella tabella selezionata.  
  
## <a name="properties"></a>Proprietà  
Scheda proprietà Visualizza le proprietà della tabella selezionata. I campi seguenti sono presenti nella scheda delle proprietà:  
  
-   Creazione o dell'ultima modifica  
  
-   Nome oggetto  
  
## <a name="columns-comparison-settings"></a>Impostazioni di confronto di colonne  
Stabilire le regole di confronto per le colonne della tabella nel **confronto tra colonne** pagina. È possibile apportare le seguenti impostazioni.  
  
### <a name="use-during-test-comparisons"></a>Utilizzo durante i confronti tra Test  
Determinare se la verifica dei risultati del test farà parte questa colonna.  
  
-   Se si sceglie **True**, SSMA confronterà il contenuto di questa colonna dopo l'esecuzione del test in Oracle con il contenuto della colonna in SQL Server. 
  
-   Se si sceglie**False**, la colonna verrà esclusi da verifica i risultati.  
  
### <a name="use-custom-scale"></a>Usare scala personalizzata  
Per le colonne di tipo di dati numerici, è possibile impostare una scala personalizzata per il confronto.  
  
-   Se si sceglie **True**, i valori numerici saranno arrotondati in base al **confronto scalabilità** valore prima che vengano confrontati.  
  
-   Se si sceglie**False**, il confronto numerico sarà esatto.  
  
### <a name="comparing-scale"></a>Confronto di scalabilità  
  
-   È disponibile solo se il **Use Custom Scale** opzione è impostata su **True**. Questa è la precisione per un confronto numerico.  
  
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
  
-   Se si sceglie **False**, il confronto terrà in considerazione per maiuscole/minuscole.  
  
## <a name="comparing-sql"></a>Confronto di SQL  
È possibile visualizzare le istruzioni SELECT generate dal Tester SSMA sul **confronto tra SQL** pagina. Il Tester confronterà il set di risultati di tali istruzioni in base a una riga per riga. Ogni riga successiva di un set di risultati Oracle deve essere uguale alla riga successiva del set di risultati prodotto in SQL Server.
  
È possibile modificare tali istruzioni SELECT per fornire la verifica personalizzata. Per salvare le modifiche in Oracle e nelle istruzioni SQL Server, usare il **applica** pulsanti sotto l'origine e la destinazione SQL, di conseguenza.  
  
## <a name="next-step"></a>Passaggio successivo  
[Personalizzazione dell'ordine delle chiamate &#40;OracleToSQL&#41;](../../ssma/oracle/customizing-calls-order-oracletosql.md)  
  
## <a name="see-also"></a>Vedere anche  
[Finishing Test Case Preparation &#40;OracleToSQL&#41;](../../ssma/oracle/finishing-test-case-preparation-oracletosql.md)  
[Esecuzione di Test case &#40;OracleToSQL&#41;](../../ssma/oracle/running-test-cases-oracletosql.md)  
[Test di oggetti di Database migrati &#40;OracleToSQL&#41;](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md)  
  
