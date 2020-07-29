---
title: Opzioni (finestre di progettazione/pagina Progettazione tabelle e database)
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.Designers.Table_Designer
ms.assetid: b43f4b97-17b9-4004-a824-f77b9e145741
author: markingmyname
ms.author: maghan
ms.openlocfilehash: d7b15f63893dfc052902f245cbb4a52220fd00c5
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/06/2020
ms.locfileid: "86001608"
---
# <a name="options-designers---table-and-database-designers-page"></a>Opzioni (finestre di progettazione/pagina Progettazione tabelle e database)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
Utilizzare questa pagina per determinare il comportamento predefinito della finestra di progettazione. Per accedere alla impostazioni scegliere **Opzioni** dal menu **Strumenti**, espandere la cartella **Finestre di progettazione** e fare clic su **Progettazione tabelle**.  
  
## <a name="ui-element-list"></a>Elenco di elementi dell'interfaccia utente  
**Esegui override del valore di timeout della stringa di connessione per gli aggiornamenti di Progettazione tabelle**  
Consente di impostare un nuovo valore di timeout per le azioni di Progettazione tabelle. Ciò risulta utile quando le azioni di Progettazione tabelle interessano una tabella di grandi dimensioni e necessitano di tempo aggiuntivo per il completamento della modifica della tabella.  
  
**Timeout transazioni dopo**  
Consente di impostare un valore di timeout per Progettazione tabelle.  
  
**Genera automaticamente script delle modifiche**  
Consente di creare automaticamente uno script per l'implementazione delle modifiche definite in Progettazione tabelle.  
  
**Avvisa in caso di chiave primaria Null**  
Consente di visualizzare una finestra di dialogo di avviso quando un campo selezionato per una chiave primaria può contenere valori Null.  
  
**Avvisa in caso siano rilevate differenze**  
Se questa casella di controllo è selezionata, durante il salvataggio delle proprie modifiche verrà visualizzata una finestra di messaggio contenente un elenco degli eventuali conflitti tra le proprie modifiche e le modifiche apportate da un altro utente.  
  
**Avvisa in caso le tabelle siano modificate**  
Consente di visualizzare una finestra di dialogo di avviso in cui vengono elencate le tabelle interessate dall'azione e viene richiesta la conferma all'utente.  
  
**Impedisci il salvataggio delle modifiche per cui è necessario ricreare la tabella**  
Impedisce un utente di apportare modifiche per cui è necessario ricreare la tabella. Per le azioni seguenti può essere necessario ricreare una tabella:  
  
-   Aggiunta di una nuova colonna a metà tabella  
  
-   Eliminazione di una colonna  
  
-   Modifica dell'ammissione di valori Null nella colonna  
  
-   Modifica dell'ordine delle colonne  
  
-   Modifica del tipo di dati di una colonna  
  
**Visualizzazione tabella predefinita**  
Selezionare la modalità di visualizzazione desiderata per le tabelle nelle finestra di progettazione:  
  
-   **Standard**  
  
    Consente di visualizzare l'intestazione di tabella, tutti i nomi di colonna, i tipi di dati e l'impostazione Consenti valori Null.  
  
-   **Nomi di colonna**  
  
    Consente di visualizzare i nomi di colonna.  
  
-   **Chiave**  
  
    Consente di visualizzare l'intestazione di tabella e le colonne chiave primaria.  
  
-   **Solo nome**  
  
    Consente di visualizzare solo l'intestazione di tabella con il relativo nome.  
  
-   **Impostazione personalizzata**  
  
    Consente di scegliere le colonne da visualizzare.  
  
**Apri la finestra Aggiungi tabella con nuovo diagramma**  
Apre automaticamente la finestra di dialogo **Aggiungi tabella** all'apertura delle finestre di progettazione.  
  
