---
title: Aggiunta e modifica di origini dati tramite il programma di installazione | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 621d10c3c602b2f406461a24e53b2302e45835eb
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67901408"
---
# <a name="adding-and-modifying-data-sources-using-setup"></a>Aggiunta e modifica delle origini dati tramite la configurazione
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Utilizzare invece il driver ODBC fornito da Oracle.  
  
 Un'origine dati identifica un percorso dei dati che può includere una libreria di rete, un server, un database e altri attributi. in questo caso, l'origine dati è il percorso di un database Oracle. Per connettersi a un'origine dati, gestione driver controlla il registro di sistema di Windows per ottenere informazioni specifiche sulla connessione.  
  
 La voce del registro di sistema creata da Amministrazione origine dati ODBC viene utilizzata da Gestione driver ODBC e driver ODBC. Questa voce contiene informazioni su ogni origine dati e il driver associato. Prima che sia possibile connettersi a un'origine dati, è necessario aggiungere le relative informazioni di connessione al registro di sistema.  
  
 Per aggiungere e configurare origini dati, utilizzare [Amministrazione origine dati ODBC](../../odbc/admin/odbc-data-source-administrator.md). L'amministratore ODBC aggiorna le informazioni di connessione all'origine dati. Quando si aggiungono origini dati, l'amministratore ODBC aggiorna le informazioni del registro di sistema.  
  
### <a name="to-add-a-data-source-for-windows"></a>Per aggiungere un'origine dati per Windows  
  
1.  Aprire Amministrazione origine dati ODBC.  
  
2.  Nella finestra di dialogo Amministrazione origine dati ODBC fare clic su Aggiungi. Verrà visualizzata la finestra di dialogo Crea nuova origine dati.  
  
3.  Selezionare Microsoft ODBC per Oracle e quindi fare clic su fine. Verrà visualizzata la finestra di dialogo installazione di Microsoft ODBC per Oracle.  
  
4.  Nella casella nome origine dati digitare il nome dell'origine dati a cui si vuole accedere. Può essere qualsiasi nome scelto.  
  
5.  Nella casella Descrizione digitare la descrizione del driver. Questo campo facoltativo descrive il driver di database a cui si connette l'origine dati. Può essere qualsiasi nome scelto.  
  
6.  Nella casella nome utente digitare il nome utente del database, ovvero l'ID utente del database.  
  
7.  Nella casella Server digitare l'alias del database o la stringa di connessione per il motore del server Oracle a cui si vuole accedere.  
  
8.  Fare clic su OK per aggiungere l'origine dati.  
  
> [!NOTE]  
>  Viene visualizzata la finestra di dialogo origini dati e l'amministratore ODBC aggiorna le informazioni del registro di sistema. Il nome utente e la stringa di connessione digitati diventano i valori di connessione predefiniti per questa origine dati quando ci si connette.  
  
1.  Fare clic su opzioni per ottenere ulteriori specifiche sul driver ODBC per il programma di installazione di Oracle:  
  
    -   **Traduzione** : fare clic su Seleziona per scegliere un convertitore di dati caricato. Il valore predefinito \<non è> Translator.  
  
    -   **Prestazioni** : la casella di controllo Includi note in funzioni di catalogo specifica se il driver restituisce colonne di osservazioni per il set di risultati [SQLColumns](../../odbc/microsoft/level-1-api-functions-odbc-driver-for-oracle.md) . Il driver ODBC per Oracle consente un accesso più rapido quando questo valore non è impostato.  
  
         La casella di controllo Includi SINONIMi nelle colonne SQL specifica se il driver restituisce le informazioni sulla colonna. **Dimensioni buffer** specifica la dimensione, in byte, allocata per la ricezione dei dati recuperati. Il driver ottimizza il recupero in modo che un recupero dal server Oracle restituisca un numero di righe sufficiente a riempire un buffer con le dimensioni specificate. I valori più grandi tendono a migliorare le prestazioni durante il recupero di una grande quantità di dati.  
  
    -   **Personalizzazione** : la casella di controllo applica ODBC DayOfWeek standard specifica se il set di risultati è conforme al formato di giorno della settimana specificato da ODBC (domenica = 1; Sabato = 7). Se questa casella di controllo è deselezionata, viene restituito il valore Oracle specifico delle impostazioni locali.  
  
         SQLDescribeCol **restituisce sempre un valore per la precisione** la casella di controllo specifica se il driver deve restituire un valore diverso da zero per l'argomento *cbColDef* di **SQLDescribeCol**. Questo attributo della stringa di connessione si applica solo alle colonne in cui non è presente alcuna scala definita da Oracle, ad esempio colonne numeriche calcolate e colonne definite come numeri senza precisione o scala. Una chiamata **SQLDescribeCol** restituisce 130 per la precisione quando Oracle non fornisce tali informazioni. Se questa casella di controllo è deselezionata, il driver restituirà 0 per questi tipi di colonne.  
  
2.  Fare clic su Aggiungi per aggiungere un'altra origine dati oppure fare clic su Chiudi per uscire.  
  
### <a name="to-modify-a-data-source-for-windows"></a>Per modificare un'origine dati per Windows  
  
1.  Aprire Amministrazione origine dati ODBC. Fare clic sulla scheda DSN appropriata.  
  
2.  Selezionare l'origine dati Oracle che si desidera modificare e quindi fare clic su Configura. Verrà visualizzata la finestra di dialogo installazione di Microsoft ODBC per Oracle.  
  
3.  Modificare i campi dell'origine dati applicabili, quindi fare clic su OK.  
  
 Al termine della modifica delle informazioni in questa finestra di dialogo, l'amministratore ODBC aggiorna le informazioni del registro di sistema.
