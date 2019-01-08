---
title: Selezione e configurazione di oggetti (SybaseToSQL) interessati | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Tester Component,Affected Objects
ms.assetid: a219df74-543a-4aec-aeeb-79f90ac3e2ee
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 48d5305854d214e61036e00ca23a94b85313138a
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/27/2018
ms.locfileid: "52402259"
---
# <a name="selecting-and-configuring-affected-objects-sybasetosql"></a>Selezione e configurazione degli oggetti interessati (SybaseToSQL)
In questa pagina è possibile selezionare tabelle e le chiavi esterne, le modifiche in cui devono essere confrontate quando SSMA verifica i risultati dell'esecuzione per gli oggetti scelto nel passaggio precedente. Inoltre, è possibile personalizzare i parametri di verifica.  
  
## <a name="selection-of-affected-objects"></a>Selezione degli oggetti interessati  
Nell'albero degli oggetti Sybase che si trova sul lato sinistro della finestra, selezionare le tabelle e le chiavi esterne, le modifiche in cui devono essere confrontate per identici.  
  
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
  
## <a name="table-comparison-settings"></a>Impostazioni di confronto di tabella  
Stabilire le regole di confronto per tabella on **confronti di tabelle** pagina. È possibile apportare le seguenti impostazioni.  
  
### <a name="comparison-mode"></a>Modalità di confronto  
Definisce il contenuto della tabella in cui verrà eseguito il confronto.  
  
-   Se si seleziona **solo modifiche**, verrà eseguito un confronto completo delle righe di tabella.  
  
-   Se si seleziona **completo**, verrà eseguito il confronto solo per le righe che sono state modificate.  
  
## <a name="column-comparison-settings"></a>Impostazioni di confronto delle colonne  
Stabilire le regole di confronto per le colonne della tabella nel **confronti colonna** pagina. È possibile apportare le seguenti impostazioni.  
  
### <a name="use-during-test-comparisons"></a>Utilizzo durante i confronti tra Test  
Determinare se la verifica dei risultati del test farà parte questa colonna.  
  
-   Se si sceglie **True**, SSMA confronterà il contenuto di questa colonna dopo l'esecuzione del test in Sybase con il contenuto della colonna in SQL Server.
  
-   Se si sceglie **False**, la colonna verrà esclusi da verifica i risultati.  
  
### <a name="use-custom-scale"></a>Usare scala personalizzata  
Per le colonne di tipo di dati numerici, è possibile impostare una scala personalizzata per il confronto.  
  
-   Se si sceglie **True**, i valori numerici saranno arrotondati in base al **confronto scalabilità** valore prima che vengano confrontati.  
  
-   Se si sceglie **False**, il confronto numerico sarà esatto.  
  
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
È possibile visualizzare le istruzioni SELECT generate dal Tester SSMA sul **confrontare SQL** pagina. Il Tester confronterà il set di risultati di tali istruzioni in base a una riga per riga. Deve essere uguale alla riga successiva del set di risultati restituito in ogni riga successiva di un set di risultati Sybase [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
È possibile modificare tali istruzioni SELECT per fornire la verifica personalizzata. Per salvare le modifiche in Sybase e nella [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (istruzioni), usare il **applica** pulsanti sotto l'origine e la destinazione SQL, di conseguenza.  
  
## <a name="next-step"></a>Passaggio successivo  
[Personalizzazione dell'ordine delle chiamate &#40;SybaseToSQL&#41;](../../ssma/sybase/customizing-calls-order-sybasetosql.md)  
  
## <a name="see-also"></a>Vedere anche  
[Esecuzione di Test case &#40;SybaseToSQL&#41;](../../ssma/sybase/running-test-cases-sybasetosql.md)  
[Test di oggetti di Database migrati &#40;SybaseToSQL&#41;](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  
