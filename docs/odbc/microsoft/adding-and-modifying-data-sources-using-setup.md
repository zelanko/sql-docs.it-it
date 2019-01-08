---
title: Aggiunta e modifica dei dati di origini tramite il programma di installazione | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 953563285d3c62a8523079a604cf607f2e0edf62
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52526853"
---
# <a name="adding-and-modifying-data-sources-using-setup"></a>Aggiunta e modifica delle origini dati tramite la configurazione
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. In alternativa, usare il driver ODBC fornito da Oracle.  
  
 Un'origine dati identifica un percorso ai dati che possono includere una libreria di rete, server, database e altri attributi: in questo caso, l'origine dati è il percorso a un database Oracle. Per connettersi a un'origine dati, gestione Driver controlla il Registro di sistema di Windows per le informazioni di connessione specifico.  
  
 La voce del Registro di sistema creata dall'amministratore origine dati ODBC viene usata dai driver ODBC e di gestione Driver ODBC. Questa voce contiene informazioni su ogni origine dati e il relativo driver. Prima di connettersi a un'origine dati, è necessario aggiungere le informazioni di connessione nel Registro di sistema.  
  
 Per aggiungere e configurare le origini dati, usare il [Amministrazione origine dati ODBC](../../odbc/admin/odbc-data-source-administrator.md). L'amministratore ODBC Aggiorna le informazioni di connessione origine dati. Quando si aggiungono origini dati, l'amministratore ODBC Aggiorna le informazioni del Registro di sistema.  
  
### <a name="to-add-a-data-source-for-windows"></a>Per aggiungere un'origine dati per Windows  
  
1.  Aprire Amministrazione origine dati ODBC.  
  
2.  Nella finestra di dialogo Amministrazione origine dati ODBC, fare clic su Aggiungi. Viene visualizzata la finestra di dialogo per creare nuova origine dati.  
  
3.  Selezionare Microsoft ODBC per Oracle e quindi fare clic su Fine. Verrà visualizzata la finestra di Microsoft ODBC per la finestra di dialogo programma di installazione di Oracle.  
  
4.  Nella casella nome dell'origine dati, digitare il nome dell'origine dati che si desidera accedere. Può essere qualsiasi nome scelto.  
  
5.  Nella finestra di descrizione, digitare la descrizione per il driver. Questo campo facoltativo descrive il driver del database che l'origine dati si connette a. Può essere qualsiasi nome scelto.  
  
6.  Nella casella nome utente, digitare il nome utente del database (ID utente di database).  
  
7.  Nella finestra di Server, digitare l'Alias di Database o stringa per il motore di Oracle Server che si desidera accedere a di connessione.  
  
8.  Fare clic su OK per aggiungere l'origine dati.  
  
> [!NOTE]  
>  Viene visualizzata la finestra di dialogo origini dei dati e l'amministratore ODBC Aggiorna le informazioni del Registro di sistema. L'utente un nome e la stringa digitata di connessione diventano i valori di connessione predefinito per questa origine dati quando ci si connette a esso.  
  
1.  Fare clic su Opzioni Rendi altre specifiche riguardanti il Driver ODBC per l'installazione di Oracle:  
  
    -   **Traduzione** -fare clic su Seleziona per scegliere una funzione di conversione di dati caricati. Il valore predefinito è \<Translator n >.  
  
    -   **Le prestazioni** -note di includere nella casella di controllo di funzioni di catalogo specifica se il driver restituisce le colonne di osservazioni per il [SQLColumns](../../odbc/microsoft/level-1-api-functions-odbc-driver-for-oracle.md) set di risultati. Il Driver ODBC per Oracle fornisce un accesso più veloce quando questo valore non è impostato.  
  
         I SINONIMI includere nella casella di controllo delle colonne SQL specifica se il driver restituisce informazioni sulle colonne. **Le dimensioni del buffer** specifica la dimensione, in byte, allocata per la ricezione dei dati recuperati. Il driver consente di ottimizzare il recupero in modo che un'operazione di recupero da Server Oracle restituisce un numero di righe sufficiente per riempire un buffer della dimensione specificata. I valori maggiori tendono ad aumentare le prestazioni durante il recupero di una grande quantità di dati.  
  
    -   **Personalizzazione** -casella di controllo di imporre ODBC DayOfWeek Standard specifica se il set di risultati sarà conforme nel formato di giorno della settimana specificato ODBC (domenica = 1. Sabato = 7). Se questa casella di controllo è deselezionata, viene restituito il valore di Oracle locali specifiche.  
  
         Il SQLDescribeCol **restituisce sempre un valore per la precisione** casella di controllo specifica se il driver deve restituire un valore diverso da zero per il *cbColDef* argomento di **SQLDescribeCol**. Questo attributo di stringa di connessione si applica solo alle colonne in cui non sono presente alcuna scalabilità definito Oracle, ad esempio calcolata numeriche colonne e le colonne definite come numero senza una precisione o scala. Oggetto **SQLDescribeCol** chiamata restituisce 130 per la precisione quando Oracle non fornisce tali informazioni. Se questa casella di controllo è deselezionata, il driver restituirà 0 per questi tipi di colonne.  
  
2.  Fare clic su Aggiungi per aggiungere un'altra origine dati oppure fare clic su Chiudi per uscire.  
  
### <a name="to-modify-a-data-source-for-windows"></a>Per modificare un'origine dati per Windows  
  
1.  Aprire Amministrazione origine dati ODBC. Fare clic sulla scheda DSN appropriata.  
  
2.  Selezionare l'origine dati Oracle che si desidera modificare e quindi fare clic su Configura. Verrà visualizzata la finestra di Microsoft ODBC per la finestra di dialogo programma di installazione di Oracle.  
  
3.  Modificare i campi dell'origine dati applicabile e quindi fare clic su OK.  
  
 Dopo avere completato la modifica le informazioni contenute in questa finestra di dialogo, l'amministratore ODBC Aggiorna le informazioni del Registro di sistema.
