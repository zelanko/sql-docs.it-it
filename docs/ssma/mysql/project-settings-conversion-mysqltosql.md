---
title: Impostazioni (conversione) (MySQLToSQL) del progetto | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 7ad5fe44-6445-4ba8-a457-5af792631f11
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 12e2e61c6b55bf3c549c08f2b090059d674ed83d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63162022"
---
# <a name="project-settings-conversion-mysqltosql"></a>Impostazioni del progetto (conversione) (MySQLToSQL)
La pagina di conversione del **impostazioni del progetto** nella finestra di dialogo contiene impostazioni che consentono di personalizzare come SSMA Converte la sintassi di MySQL in sintassi SQL Server o SQL Azure.  
  
Nel riquadro di conversione è disponibile nel **impostazioni del progetto** e **impostazioni di progetto predefinite** finestre di dialogo.  
  
-   Usare la **impostazioni di progetto predefinite** finestra di dialogo per impostare le opzioni di configurazione per tutti i progetti. Per accedere a impostazioni di conversione, scegliere il **strumenti** dal menu **impostazioni di progetto predefinite**, selezionare tipo di progetto di migrazione per i quali impostazioni sono necessarie per essere visualizzati / modificato da  **Versione di destinazione della migrazione** elenco a discesa, fare clic su **generali** nella parte inferiore del riquadro a sinistra e quindi selezionare **conversione**.  
  
-   Per specificare le impostazioni per il progetto corrente, il **strumenti** menu fare clic su **le impostazioni del progetto**, quindi fare clic su **generale** nella parte inferiore del riquadro di sinistra e quindi fare clic su **Conversione**.  
  
## <a name="options"></a>Opzioni  
  
### <a name="collate-clause"></a>Clausola COLLATE  
  
|||  
|-|-|  
|**Nome**|**Definizione**|  
|**Conversione esplicita di clausola COLLATE**|Opzione di conversione esplicita COLLATE clausola specifica come eseguire la conversione esplicitare clausole COLLATE nel codice di MySQL. Scelte possibili: Ignora e contrassegnare con un messaggio di avviso / genera un errore<br /><br />**Modalità predefinita**:  Ignora e contrassegnare con un messaggio di avviso<br /><br />**La modalità ottimistico**:  Ignora e contrassegnare con un messaggio di avviso<br /><br />**Modalità intero**:  Ignora e contrassegnare con un messaggio di avviso|  
  
### <a name="column-constraints"></a>Vincoli di colonna  
  
|||  
|-|-|  
|**Nome**|**Definizione**|  
|**Generare vincoli per le colonne di tipo di dati di Enumerazione**|Genera vincoli per le colonne di tipo di dati di Enumerazione nella tabella di SQL Server o SQL Azure, se non è presente nella tabella di MySQL. In caso affermativo, tutte le colonne convertite del tipo di dati di Enumerazione sono accompagnate dal vincolo CHECK, controllare il valore.<br /><br />**Modalità predefinita**:   No<br /><br />**La modalità ottimistico**:  no<br /><br />**Modalità intero**:   Yes|  
|**Generare vincoli per le colonne di tipo di SET di dati**|Genera i vincoli per le colonne di tipo di SET di dati della tabella di SQL Server o SQL Azure, se non è presente nella tabella di MySQL. In caso affermativo, tutte le colonne convertite della tipo di SET di dati sia associate a vincolo CHECK, controllare il valore.<br /><br />**Modalità predefinita**:   No<br /><br />**La modalità ottimistico**:  No<br /><br />**Modalità intero**:   Yes|  
|**Generare vincoli per le colonne delle colonne di tipo di dati numerico senza segno**|Aggiungi il controllo per un valore non negativo alle colonne dei tipi di dati numerico senza segno.<br /><br />**Modalità predefinita**:   No<br /><br />**La modalità ottimistico**:  no<br /><br />**Modalità intero**:   Yes|  
|**Generazione di vincolo per colonne di tipo anno dei dati**|Genera l'errore di vincolo per colonne di tipo anno dei dati nella tabella SQL Server o SQL Azure, se non è presente nella tabella MySQL. In caso affermativo, tutti convertiti colonne di tipo sia associato a vincolo CHECK, controllare il valore di dati dell'anno.<br /><br />**Modalità predefinita**:   No<br /><br />**La modalità ottimistico**:  No<br /><br />**Modalità intero**:   Yes|  
  
### <a name="data-types"></a>Tipi di dati  
  
|||  
|-|-|  
|**Nome**|**Definizione**|  
|**Conversione del tipo di dati di Enumerazione**|Specifica come tipo di dati MySQL ENUM deve essere convertito come Convert a NVARCHAR o convertito in numerico<br /><br />**Modalità predefinita**:  Converti in NVARCHAR<br /><br />**La modalità ottimistico**:  Converti in NVARCHAR<br /><br />**Modalità intero**:  Converti in NVARCHAR|  
|**Conversione di tipi SET di dati**|Specifica come tipo di dati di MySQL impostata è deve essere convertito, convertire i per NVARCHAR (L) / convertire BINARY(L)<br /><br />**Modalità predefinita**: Converti in NVARCHAR(L)<br /><br />**La modalità ottimistico**: Converti in NVARCHAR(L)<br /><br />**Modalità intero**: Converti in NVARCHAR(L)|  
  
### <a name="generic"></a>Generico  
  
|||  
|-|-|  
|**Nome**|**Definizione**|  
|**Colonne senza un valore predefinito di inserimento e sostituzione**|In caso affermativo, tutte le istruzioni che fanno riferimento a tabelle utilizzando stored motori diversi da MyISAM e InnoDb devono essere contrassegnate con messaggi di avviso di conversione.<br /><br />**Modalità predefinita**:  Aggiungere all'elenco di colonne<br /><br />**La modalità ottimistico**:  Aggiungere all'elenco di colonne<br /><br />**Modalità intero**:   Aggiungere all'elenco di colonne|  
|**Divisione per Zero genera la conversione**|Specifica se emulare MySQL senza comportamento ERROR_FOR_DIVISION_BY_ZERO o meno.<br /><br />**Modalità predefinita**:   Errore<br /><br />**La modalità ottimistico**:  Errore<br /><br />**Modalità intero**:   NULL|  
|**Operatore IN**|Specifica come convertire operatore IN MySQL.<br /><br />**Modalità predefinita**:   Converti sempre a nella<br /><br />**La modalità ottimistico**:  Converti sempre a nella<br /><br />**Modalità intero**:   Espandere, se necessario|  
|**Conversione di MySQL (funzione)**|Specifica come convertire le funzioni standard di MySQL.<br /><br />**Modalità predefinita**:   Optimistic<br /><br />**La modalità ottimistico**:  Optimistic<br /><br />**Modalità intero**:   Preciso|  
|**Non supportati motori di archiviazione**|In caso affermativo, tutte le istruzioni che fanno riferimento a tabelle utilizzando stored motori diversi da MyISAM e InnoDb devono essere contrassegnate con messaggi di avviso di conversione.<br /><br />**Modalità predefinita**:   No<br /><br />**La modalità ottimistico**:  No<br /><br />**Modalità intero**:   Yes|  
|**Eliminare la generazione di colonna ausiliario ROWID**|In caso affermativo, impedisce la creazione della creazione di colonne ausiliario ROWD nelle tabelle di destinazione. Potrebbero influire sulla migrazione di alcune strutture.<br /><br />**Modalità predefinita**:   No<br /><br />**La modalità ottimistico**:  No<br /><br />**Modalità intero**:   No|  
|**Conversione di istruzioni TRUNCATE**|Specifica come eseguire la conversione di istruzioni TRONCATE.<br /><br />**Modalità predefinita**:   TRUNCATE<br /><br />**La modalità ottimistico**:  TRUNCATE<br /><br />**Modalità intero**:   TRUNCATE|  
  
### <a name="misc"></a>Varie  
  
|||  
|-|-|  
|**Nome**|**Definizione**|  
|**Mapping dello Schema predefinito**|Specifica come eseguire il mapping di database MySQL in schemi di SQL Server.<br /><br />**Modalità predefinita**:  Database in un Database<br /><br />**La modalità ottimistico**:  Database in un Database<br /><br />**Modalità intero**:  Database in un Database|  
  
### <a name="procedures-and-functions"></a>Procedure e funzioni  
  
|||  
|-|-|  
|**Nome**|**Definizione**|  
|**Conversione di funzione predefinita**|Specifica se le funzioni devono essere per impostazione predefinita essere convertiti in funzioni T-SQL o alle stored procedure.<br /><br />**Modalità predefinita**:  Converti in (funzione)<br /><br />**La modalità ottimistico**:  Converti in (funzione)<br /><br />**Modalità intero**:  Converti in (funzione)|  
|**Generare SET XACT_ABORT su**|Specifica se SET XACT_ABORT su ON deve essere aggiunto all'inizio della procedura convertito o del trigger.<br /><br />**Modalità predefinita**:  Yes<br /><br />**La modalità ottimistico**:  Yes<br /><br />**Modalità intero**:  Yes|  
|**Generare SET NOCOUNT su**|Specifica se SET NOCOUNT ON deve essere aggiunto all'inizio della procedura convertito o del trigger.<br /><br />**Modalità predefinita**:  Yes<br /><br />**La modalità ottimistico**:  Yes<br /><br />**Modalità intero**:  Yes|  
  
### <a name="spatial-data-types"></a>Tipi di dati spaziali  
  
|||  
|-|-|  
|**Nome**|**Definizione**|  
|**Rettangolo delimitatore predefinito {XMAX&#124;XMIN&#124;YMAX&#124;YMIN} per gli indici spaziali**|Definisce il valore predefinito per {XMAX&#124;XMIN&#124;YMAX&#124;YMIN} parametro del rettangolo utilizzate negli indici spaziali.<br /><br />**Modalità predefinita**<br /><br />XMAX: 100<br /><br />XMIN: 0<br /><br />YMAX: 100<br /><br />YMIN: 0<br /><br />**Modalità ottimistico**<br /><br />XMAX: 100<br /><br />XMIN: 0<br /><br />YMAX:  100<br /><br />YMIN: 0<br /><br />**Modalità completa**<br /><br />XMAX: 100<br /><br />XMIN: 0<br /><br />YMAX: 100<br /><br />YMIN: 0|  
|**Densità della griglia predefinita per gli indici spaziali**|Definisce il valore predefinito per LEVEL_1, LEVEL_2, LEVEL_3 e LEVEL_4 di densità della griglia utilizzate negli indici spaziali.<br /><br />**Modalità predefinita**<br /><br />LEVEL_1: Impostazione predefinita<br /><br />LEVEL_2: Impostazione predefinita<br /><br />LEVEL_3: Impostazione predefinita<br /><br />LEVEL_4: Impostazione predefinita<br /><br />**Modalità ottimistico**<br /><br />LEVEL_1: Impostazione predefinita<br /><br />LEVEL_2: Impostazione predefinita<br /><br />LEVEL_3: Impostazione predefinita<br /><br />LEVEL_4: Impostazione predefinita<br /><br />**Modalità completa**<br /><br />LEVEL_1: Impostazione predefinita<br /><br />LEVEL_2: Impostazione predefinita<br /><br />LEVEL_3: Impostazione predefinita<br /><br />LEVEL_4: Impostazione predefinita|  
  
### <a name="transactions"></a>Transazioni  
  
|||  
|-|-|  
|**Nome**|**Definizione**|  
|**Tabelle non transazionale**|Specifica se tutti i riferimenti alla tabella che non supportano le transazioni devono essere contrassegnati con messaggi di avviso di conversione.<br /><br />**Modalità predefinita**: No<br /><br />**La modalità ottimistico**: No<br /><br />**Modalità intero**: Yes|  
|**Livello di isolamento delle transazioni**|Specifica il livello di isolamento delle transazioni deve essere utilizzato per le nuove transazioni.<br /><br />**Modalità predefinita**:   Impostazione predefinita<br /><br />**La modalità ottimistico**:  Impostazione predefinita<br /><br />**Modalità intero**:   Repeatable Read|  
  
### <a name="value-control"></a>Controllo valore  
  
|||  
|-|-|  
|**Nome**|**Definizione**|  
|**Carattere per la conversione numerica**|Specifica come gestire la conversione implicita ed esplicita dal tipo di dati Character a tipi di dati numerici.<br /><br />**Modalità predefinita**:   Optimistic<br /><br />**La modalità ottimistico**:  Optimistic<br /><br />**Modalità intero**:   Preciso|  
|**Controllare i valori numerici senza segno**|Controllo assegnazione di valori per parametri e variabili numeriche senza segno.<br /><br />**Modalità predefinita**:   No<br /><br />**La modalità ottimistico**:  No<br /><br />**Modalità intero**:   Yes|  
|**Controllare la sottrazione non FIRMATA**|Modificare i valori negativi inseriti nelle colonne di tabella del tipo di dati senza segno.<br /><br />**Modalità predefinita**:   Converti ' come-è '<br /><br />**La modalità ottimistico**:  Converti ' come-è '<br /><br />**Modalità intero**:   Contrassegnare con un messaggio di avviso|  
|**Conversione da e verso il tipo di dati binari**|Specifica come gestire le conversioni implicite ed esplicite dal tipo di dati binari.<br /><br />**Modalità predefinita**:   Optimistic<br /><br />**La modalità ottimistico**:  Optimistic<br /><br />**Modalità intero**:   Preciso|  
|**Tipo di conversione in dati di data/ora**|Specifica la modalità di conversione impliciti ed espliciti a data/ora di gestire tipi di dati.<br /><br />**Modalità predefinita**:   Emulare formato MySQL<br /><br />**La modalità ottimistico**:  Usare il formato di SQL Server<br /><br />**Modalità intero**:   Emulare formato MySQL|  
|**Valori letterali numerici con precisione superiore a 38**|Specifica come convertire i valori letterali numerici con precisione superiore a 38.<br /><br />**Modalità predefinita**:   Se possibile arrotondare<br /><br />**La modalità ottimistico**:  Se possibile arrotondare<br /><br />**Modalità intero**:   Se possibile arrotondare|  
|**Zero-date nelle colonne NOT NULL**|Specifica come gestire l'assegnazione per le colonne NOT NULL di Zero-date, Zero-in-date o valori data/ora non valido.<br /><br />**Modalità predefinita**:   GETDATE)<br /><br />**La modalità ottimistico**:  GETDATE)<br /><br />**Modalità intero**:   GETDATE)|  
  
## <a name="see-also"></a>Vedere anche  
[Riferimento all'interfaccia utente &#40;MySQLToSQL&#41;](../../ssma/mysql/user-interface-reference-mysqltosql.md)  
  
