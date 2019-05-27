---
title: Confrontare e sincronizzare i dati in una o più tabelle e i dati di un database di riferimento | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 96d743b0-b69a-45bb-ae0e-62103dca76e2
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 567855c53848a354ec03c8de7fea1bb37c1c2a21
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/06/2019
ms.locfileid: "65105806"
---
# <a name="compare-and-synchronize-data-in-one-or-more-tables-with-data-in-a-reference-database"></a>Confrontare e sincronizzare i dati in una o più tabelle e i dati di un database di riferimento
È possibile confrontare i dati in un database di *origine* e in un database di *destinazione* e specificare quali tabelle confrontare. È possibile rivedere i dati e decidere quali modifiche sincronizzare. È quindi possibile aggiornare la destinazione per sincronizzare i database o esportare lo script di aggiornamento nell'editor Transact\-SQL o in un file.  
  
Ad esempio, è possibile sincronizzare i database per aggiornare un server temporaneo con una copia dei dati di produzione. È inoltre possibile sincronizzare una o più tabelle per popolarle con dati di riferimento da un altro database. Inoltre, è possibile confrontare i dati prima e dopo l'esecuzione dei test come forma di verifica aggiuntiva.  
  
È possibile confrontare i dati in due database, ma non è possibile specificare un file progetto di database o un file con estensione dacpac di confronto perché non contiene dati.  
  
Questa sezione contiene i seguenti argomenti:  
  
-   [Procedura: Confrontare e sincronizzare i dati di due database](../ssdt/how-to-compare-and-synchronize-the-data-of-two-databases.md)  
  
-   [Procedura: Visualizzare le differenze dei dati](../ssdt/how-to-view-data-differences.md)  
  
## <a name="requirements"></a>Requisiti  
Quando si confrontano i dati in una tabella o una vista, la tabella o la vista nel database di origine deve condividere diversi attributi con una tabella o una vista nel database di destinazione. Tabelle e viste che non soddisfano i criteri seguenti non vengono confrontate e non vengono visualizzate nella seconda pagina della procedura guidata **Nuovo confronto dati**:  
  
-   Le tabelle devono avere nomi di colonna corrispondenti con tipi di dati compatibili.  
  
    I nomi di tabelle, viste e proprietari fanno distinzione tra maiuscole e minuscole.  
  
-   Le tabelle devono avere la stessa chiave primaria, lo stesso indice univoco o lo stesso vincolo univoco.  
  
-   Le viste devono avere lo stesso indice cluster univoco.  
  
-   È possibile confrontare una tabella con una vista solo se hanno lo stesso nome.  
  
Ogni oggetto dispone di una chiave o di un indice che determina gli altri oggetti a cui corrisponde. Tuttavia, ogni tabella o vista può avere più chiavi primarie, più indici univoci o più vincoli univoci. Pertanto, può essere opportuno specificare quale chiave, indice o vincolo utilizzare.  
  
## <a name="common-tasks"></a>Attività comuni  
In questa sezione sono riportate le descrizioni delle attività comuni che supportano questo scenario.  
  
**Impostare le opzioni per controllare il modo in cui i dati vengono confrontati:** quando si confrontano i dati, è possibile ignorare in modo sicuro le colonne Identity, disabilitare i trigger e disabilitare le chiavi esterne. È inoltre possibile eliminare chiavi primarie, indici e vincoli univoci dallo script di aggiornamento.  
  
**Confrontare i dati nelle tabelle e facoltativamente aggiornare la destinazione in modo corrispondente all'origine:** dopo aver specificato un database di origine e di destinazione da confrontare e dopo aver eseguito il confronto, è possibile visualizzare i risultati nella finestra **Confronto dati**. Non solo è possibile visualizzare i dettagli delle differenze, ma anche aggiornare lo script che è possibile utilizzare per sincronizzare i dati. Dopo aver identificato le differenze tra i due database, è possibile specificare un'azione per ogni differenza. È quindi possibile aggiornare la destinazione o esportare lo script di aggiornamento nell'editor Transact\-SQL o in un file. Può essere opportuno esportare lo script per consentirne la revisione prima di applicare le modifiche.  
  
## <a name="UnderstandingDataCompareResults"></a>Informazioni sui risultati del confronto  
Nella tabella seguente vengono descritte le cinque colonne nella finestra **Confronto dati**.  
  
|colonna|Note|  
|----------|---------|  
|Object|Visualizza il nome della tabella o della vista e una casella di controllo che indica se la destinazione deve essere sincronizzata quando si scrivono gli aggiornamenti o quando si esporta lo script di aggiornamento. La casella di controllo non è disponibile per le tabelle o le viste che non contengono dati.|  
|Record diversi|Visualizza il numero di record nella destinazione che presentano la stessa chiave, ma non gli stessi dati dell'origine. Tra parentesi è riportato il numero di record contrassegnati per essere aggiornati quando si scrivono aggiornamenti o si esporta lo script di aggiornamento.|  
|Solo nell'origine|Visualizza il numero di record nell'origine che non sono presenti nella destinazione. Tra parentesi è riportato il numero di record contrassegnati per essere aggiunti quando si scrivono aggiornamenti o si esporta lo script di aggiornamento.|  
|Solo nella destinazione|Visualizza il numero di record nella destinazione che non sono presenti nell'origine. Tra parentesi è riportato il numero di record contrassegnati per essere eliminati quando si scrivono aggiornamenti o si esporta lo script di aggiornamento.|  
|Record identici|Visualizza il numero di record nella destinazione che presentano la stessa chiave e gli stessi dati dell'origine. Questi record non vengono aggiornati quando si scrivono aggiornamenti o si esporta lo script di aggiornamento.|  
  
### <a name="table-and-view-details"></a>Dettagli su viste e tabelle  
Quando si fa clic su qualsiasi tabella o vista nella finestra **Confronto dati**, nel riquadro dei dettagli vengono visualizzate tutte le righe che la tabella o la vista contiene. Ogni scheda nel riquadro dei dettagli visualizza una categoria diversa (Record diversi, Solo nell'origine, Solo nella destinazione, Record identici). Per ogni riga, è possibile selezionare o deselezionare la casella di controllo corrispondente per indicare se si desidera includere tale modifica nello script di aggiornamento.  
  
## <a name="see-also"></a>Vedere anche  
[SQL Server Data Tools](../ssdt/sql-server-data-tools.md)  
[Procedura: Usare il confronto schema per confrontare definizioni di database diverse](../ssdt/how-to-use-schema-compare-to-compare-different-database-definitions.md)  
  
