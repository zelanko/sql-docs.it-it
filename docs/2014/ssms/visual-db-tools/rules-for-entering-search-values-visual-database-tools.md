---
title: Regole per l'immissione di valori di ricerca (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- time [SQL Server], searches
- date searches
- dates [SQL Server], searches
- embedding apostrophes [SQL Server]
- logical value searches [SQL Server]
- case-sensitive search matches
- search criteria [SQL Server], rules
- text value searches [SQL Server]
- numeric value searches [SQL Server]
ms.assetid: 3c8134b7-83f4-41b4-99c8-e3949a685ff5
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: fc11acccd25dafd811379384bf9975e74e8986b6
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "63070985"
---
# <a name="rules-for-entering-search-values-visual-database-tools"></a>Regole per l'immissione di valori di ricerca (Visual Database Tools)
  In questo argomento sono illustrate le convenzioni da utilizzare quando si immettono i seguenti tipi di valori letterali in una condizione di ricerca:  
  
-   Valori di testo  
  
-   Valori numerici  
  
-   Date  
  
-   Valori logici  
  
> [!NOTE]  
>  Le informazioni contenute in questo argomento derivano dalle regole relative a SQL-92 standard. In ogni database è tuttavia possibile implementare SQL in modo personalizzato. Le indicazioni fornite potrebbero quindi non essere valide per tutti i database. In caso di dubbi su come immettere i valori di ricerca per un particolare database, vedere la documentazione del database in uso.  
  
## <a name="searching-on-text-values"></a>Ricerche su valori di testo  
 Quando si immettono valori di tipo testo nelle condizioni di ricerca, è necessario tenere presente le seguenti indicazioni:  
  
-   **Virgolette** Delimitare i valori di tipo testo tra virgolette semplici, come nell’esempio seguente per un cognome:  
  
    ```  
    'Smith'  
    ```  
  
     Se si immette una condizione di ricerca nel [riquadro Criteri](visual-database-tools.md), è sufficiente specificare il valore di testo. Le virgolette verranno inserite automaticamente.  
  
    > [!NOTE]  
    >  In alcuni database le parole tra virgolette singole vengono interpretate come valori letterali, mentre le parole tra virgolette doppie vengono interpretate come oggetti di database quali riferimenti a colonne o tabelle. Di conseguenza, anche se in Progettazione query e Progettazione viste è possibile accettare parole tra virgolette doppie, l'interpretazione potrebbe essere diversa da quella prevista.  
  
-   **Incorporamento di apostrofi** Se i dati da cercare contengono una virgoletta singola (un apostrofo), è possibile immettere due virgolette singole per indicare che la virgoletta singola deve essere interpretata come un valore letterale e non come delimitatore. La seguente condizione ricerca ad esempio il valore "Swann's Way":  
  
    ```  
    ='Swann''s Way'  
    ```  
  
-   **Limiti di lunghezza** Quando si immettono stringhe lunghe non si deve superare la lunghezza massima delle istruzioni SQL per il database in uso.  
  
-   **Distinzione tra maiuscole e minuscole** È necessario seguire le regole di distinzione tra maiuscole e minuscole per il database che si sta usando. Il database in uso determina se le ricerche di elementi di testo distinguono fra maiuscole e minuscole. Alcuni database interpretano, ad esempio, l'operatore "=" come corrispondenza di maiuscole e minuscole, mentre altri consentono la ricerca di qualsiasi combinazione di caratteri maiuscoli e minuscoli.  
  
     Se non si è certi dell'utilizzo delle maiuscole e delle minuscole nel database in uso, è possibile utilizzare le funzioni UPPER o LOWER nelle condizioni di ricerca per convertire i dati della ricerca, come mostrato nel seguente esempio:  
  
    ```  
    WHERE UPPER(lname) = 'SMITH'  
    ```  
  
## <a name="searching-on-numeric-values"></a>Ricerche su valori numerici  
 Quando si immettono valori numerici nelle condizioni di ricerca, è necessario tenere presente le seguenti indicazioni:  
  
-   **Virgolette** Non racchiudere i numeri tra virgolette.  
  
-   **Caratteri non numerici** Non inserire caratteri non numerici, tranne il separatore decimale (come definito nella finestra di dialogo **Impostazioni internazionali** del Pannello di controllo di Windows) e il segno negativo (-). Non inserire simboli di raggruppamento di cifre (quale il separatore delle migliaia) o simboli di valuta.  
  
-   **Separatore decimale** Se si stanno immettendo numeri interi, è possibile inserire un separatore decimale, sia che il valore che si sta cercando sia un valore intero sia che si tratti di un numero reale.  
  
-   **Notazione scientifica** È possibile immettere numeri molto grandi o molto piccoli usando la notazione scientifica, come nell’esempio seguente:  
  
    ```  
    > 1.23456e-9  
    ```  
  
## <a name="searching-on-dates"></a>Ricerche su date  
 Il formato da utilizzare per immettere le date dipende dal database in uso e dal riquadro di Progettazione query e Progettazione viste in cui si sta immettendo la data.  
  
> [!NOTE]  
>  Se non si conosce il formato utilizzato dall'origine dati, digitare una data nella colonna Filtro del riquadro Criteri in un formato conosciuto. La maggior parte di queste voci verrà convertita automaticamente nel formato appropriato.  
  
 È possibile utilizzare i seguenti formati di data:  
  
-   **Specifico delle impostazioni locali** Formato specificato per le date nella finestra di dialogo delle **Proprietà delle impostazioni internazionali di Windows** .  
  
-   **Specifico del database** Qualsiasi formato supportato dal database.  
  
-   **Data standard ANSI** Formato che usa parentesi graffe, il marcatore "d" per identificare la data e una stringa della data come nell’esempio seguente:  
  
    ```  
    { d '1990-12-31' }  
    ```  
  
-   **Data/ora standard ANSI** Analogo alla data standard ANSI, ma usa "ts" al posto di 'd' e aggiunge le ore, i minuti e i secondi alla data (usando una notazione di 24 ore), come nell'esempio seguente per 31 dicembre 1990:  
  
    ```  
    { ts '1990-12-31 00:00:00' }  
    ```  
  
     In generale, il formato di data standard ANSI viene utilizzato con i database che rappresentano le date con un tipo di date reali. Il formato datetime viene invece utilizzato con database che supportano un tipo di dati datetime.  
  
 Nella tabella riportata di seguito sono elencati i formati di data utilizzabili nei diversi riquadri di Progettazione query e Progettazione viste.  
  
|**Riquadro**|**Formato data**|  
|--------------|---------------------|  
|Criteri|Specifico delle impostazioni locali? Specifico del database ?Standard ANSI<br /><br /> Le date immesse nel [riquadro Criteri](visual-database-tools.md) vengono convertite in un formato compatibile con il database nel riquadro SQL.|  
|SQL|Specifico del database ?Standard ANSI|  
|Risultati|Specifico delle impostazioni locali|  
  
## <a name="searching-on-logical-values"></a>Ricerche su valori logici  
 Il formato dei dati logici varia da database a database. Molto spesso, un valore False viene memorizzato come zero (0). Un valore True viene generalmente archiviato come 1 e talvolta come -1. Quando si immettono valori logici nelle condizioni di ricerca, è consigliabile attenersi alle indicazioni seguenti:  
  
-   Per cercare un valore False, utilizzare uno zero, come nel seguente esempio:  
  
    ```  
    SELECT * FROM authors  
    WHERE contract = 0  
    ```  
  
-   Se non si è certi del formato da utilizzare quando si cerca un valore True, provare a utilizzare 1, come nel seguente esempio:  
  
    ```  
    SELECT * FROM authors  
    WHERE contract = 1  
    ```  
  
-   In alternativa, è possibile ampliare l'ambito della ricerca cercando tutti i valori diversi da zero, come nel seguente esempio:  
  
    ```  
    SELECT * FROM authors  
    WHERE contract <> 0  
    ```  
  
## <a name="see-also"></a>Vedere anche  
 [Specifica dei criteri di ricerca &#40;Visual Database Tools&#41;](specify-search-criteria-visual-database-tools.md)  
  
  
