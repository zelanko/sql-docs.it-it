---
title: Aggiunta e modifica di origini dati tramite il programma di installazione . Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], adding
- editing data sources [ODBC], ODBC driver for Oracle
- adding data sources [ODBC], ODBC driver for Oracle
- data sources [ODBC], changing
- data sources [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], adding data sources
ms.assetid: 54b2d61d-6ce5-45af-a776-e03180470ecf
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ae76abc902e4687e5d9891871d7d5d60598b3abc
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81281411"
---
# <a name="adding-and-modifying-data-sources-using-setup"></a>Aggiunta e modifica delle origini dati tramite la configurazione
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Utilizzare invece il driver ODBC fornito da Oracle.  
  
 Un'origine dati identifica un percorso ai dati che può includere una libreria di rete, un server, un database e altri attributi, in questo caso l'origine dati è il percorso di un database Oracle. Per connettersi a un'origine dati, Gestione Driver controlla il Registro di sistema di Windows per informazioni di connessione specifiche.  
  
 La voce del Registro di sistema creata da Amministrazione origine dati ODBC viene utilizzata da Gestione driver ODBC e dai driver ODBC. Questa voce contiene informazioni su ogni origine dati e il driver associato. Prima di potersi connettere a un'origine dati, è necessario aggiungere le relative informazioni di connessione al Registro di sistema.  
  
 Per aggiungere e configurare origini dati, utilizzare [Amministrazione origine dati ODBC.](../../odbc/admin/odbc-data-source-administrator.md) L'Amministratore ODBC aggiorna le informazioni di connessione all'origine dati. Quando si aggiungono origini dati, l'Amministratore ODBC aggiorna automaticamente le informazioni del Registro di sistema.  
  
### <a name="to-add-a-data-source-for-windows"></a>Per aggiungere un'origine dati per WindowsTo add a data source for Windows  
  
1.  Aprire Amministrazione origine dati ODBC.  
  
2.  Nella finestra di dialogo Amministratore origine dati ODBC fare clic su Aggiungi. Verrà visualizzata la finestra di dialogo Crea nuova origine dati.  
  
3.  Selezionare Microsoft ODBC per Oracle e quindi fare clic su Fine. Verrà visualizzata la finestra di dialogo Installazione di Microsoft ODBC per Oracle.  
  
4.  Nella casella Nome origine dati digitare il nome dell'origine dati a cui si desidera accedere. Può essere qualsiasi nome che si sceglie.  
  
5.  Nella casella Descrizione digitare la descrizione del driver. Questo campo facoltativo descrive il driver di database a cui si connette l'origine dati. Può essere qualsiasi nome che si sceglie.  
  
6.  Nella casella Nome utente digitare il nome utente del database, ovvero l'ID utente del database.  
  
7.  Nella casella Server digitare l'alias del database o la stringa di connessione per il motore di Oracle Server a cui si desidera accedere.  
  
8.  Fare clic su OK per aggiungere questa origine dati.  
  
> [!NOTE]  
>  Verrà visualizzata la finestra di dialogo Origini dati e l'Amministratore ODBC aggiorna le informazioni del Registro di sistema. Il nome utente e la stringa di connessione digitati diventano i valori di connessione predefiniti per questa origine dati quando ci si connette a essa.  
  
1.  Fare clic su Opzioni per creare ulteriori specifiche sull'installazione del driver ODBC per Oracle:  
  
    -   **Traduzione:** fare clic su Seleziona per scegliere un traduttore di dati caricato. L'impostazione predefinita è \<Nessun> traduttore.  
  
    -   **Prestazioni:** la casella di controllo Includi OSSERVAZIONI nelle funzioni di catalogo specifica se il driver restituisce le colonne Remarks per il set di risultati [SQLColumns.](../../odbc/microsoft/level-1-api-functions-odbc-driver-for-oracle.md) Il driver ODBC per Oracle fornisce un accesso più rapido quando questo valore non è impostato.  
  
         La casella di controllo Includi SYNONYMS nelle colonne SQL specifica se il driver restituisce informazioni sulla colonna. **Dimensione buffer** specifica la dimensione, in byte, allocata per ricevere i dati recuperati. Il driver ottimizza il recupero in modo che un recupero da Oracle Server restituisce un numero sufficiente di righe per riempire un buffer della dimensione specificata. Valori più grandi tendono ad aumentare le prestazioni durante il recupero di una grande mole di dati.  
  
    -   **Personalizzazione:** la casella di controllo Applica standard DayOfWeek ODBC consente di specificare se il set di risultati sarà conforme al formato del giorno della settimana specificato da ODBC (domenica - 1; Sabato 7). Se questa casella di controllo è deselezionata, viene restituito il valore Oracle specifico delle impostazioni locali.  
  
         La casella di controllo SQLDescribeCol **restituisce sempre un valore per la precisione** specifica se il driver deve restituire o meno un valore diverso da zero per l'argomento *cbColDef* di **SQLDescribeCol**. Questo attributo della stringa di connessione si applica solo alle colonne in cui non è presente una scala definita da Oracle, ad esempio le colonne numeriche calcolate e le colonne definite come NUMBER senza precisione o scala. Una chiamata **SQLDescribeCol** restituisce 130 per la precisione quando Oracle non fornisce tali informazioni. Se questa casella di controllo è deselezionata, il driver restituirà 0 per questi tipi di colonne.  
  
2.  Fare clic su Aggiungi per aggiungere un'altra origine dati oppure fare clic su Chiudi per uscire.  
  
### <a name="to-modify-a-data-source-for-windows"></a>Per modificare un'origine dati per WindowsTo modify a data source for Windows  
  
1.  Aprire Amministrazione origine dati ODBC. Fare clic sulla scheda DSN appropriata.  
  
2.  Selezionare l'origine dati Oracle che si desidera modificare e quindi fare clic su Configura. Verrà visualizzata la finestra di dialogo Installazione di Microsoft ODBC per Oracle.  
  
3.  Modificare i campi dell'origine dati applicabili e quindi fare clic su OK.  
  
 Al termine della modifica delle informazioni contenute in questa finestra di dialogo, l'Amministratore ODBC aggiorna le informazioni del Registro di sistema.
