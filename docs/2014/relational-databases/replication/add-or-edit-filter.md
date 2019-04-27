---
title: Aggiungi filtro o Modifica filtro | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.newpubwizard.addeditfilter.f1
ms.assetid: bdd7c71d-1c59-4044-bfe8-c85f908345bb
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: fa12421f39119fbbb5e40c8c2b6dc7f103cd9a45
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62676886"
---
# <a name="add-or-edit-filter"></a>Aggiungi filtro o Modifica filtro
  Le finestre di dialogo **Aggiungi filtro** e **Modifica filtro** consentono di aggiungere e modificare i filtri di riga statica o di riga con parametri.  
  
> [!NOTE]  
>  Per modificare un filtro in una pubblicazione esistente, è necessario un nuovo snapshot per la pubblicazione. Se la pubblicazione dispone di sottoscrizioni, queste ultime devono essere reinizializzate. Per altre informazioni sulle modifiche delle proprietà, vedere [Modificare le proprietà di pubblicazioni e articoli](publish/change-publication-and-article-properties.md).  
  
 In tutti i tipi di pubblicazione possono essere inclusi filtri statici. Nelle pubblicazioni di tipo merge possono essere inoltre inclusi filtri con parametri. Un filtro statico viene valutato al momento della creazione della pubblicazione: tutti i sottoscrittori della pubblicazione ricevono gli stessi dati. Un filtro con parametri viene invece valutato durante la sincronizzazione della replica: Sottoscrittori distinti possono ricevere diverse partizioni di dati, in base al nome dell'account di accesso o del computer di ognuno. Per poter esaminare esempi di ogni tipo di filtro, fare clic sul collegamento **Istruzione di esempio** . Per altre informazioni sulle opzioni di filtro, vedere [Filtrare i dati pubblicati](publish/filter-published-data.md).  
  
 L'applicazione di filtri di riga consente di specificare un subset di righe che devono essere pubblicate da una tabella. I filtri di riga possono essere utilizzati per eliminare le righe che non devono essere visualizzate dagli utenti, ad esempio le righe in cui sono contenute informazioni delicate o riservate, oppure per creare diverse partizioni di dati da inviare ai vari Sottoscrittori. La pubblicazione di diverse partizioni di dati in diversi Sottoscrittori può contribuire a evitare i conflitti che si verificherebbero se più Sottoscrittori aggiornassero gli stessi dati.  
  
## <a name="options"></a>Opzioni  
 Questa finestra di dialogo prevede un processo in due passaggi per le pubblicazioni snapshot e transazionali e un processo in tre passaggi per le pubblicazioni di tipo merge. Per ogni tipo di pubblicazione è necessaria la selezione di una tabella da filtrare e di una o più colonne da includere nel filtro. Quest'ultimo è definito come clausola WHERE standard.  
  
1.  **Selezionare la tabella da filtrare**  
  
     Se è in corso la modifica di un filtro esistente, la selezione della tabella non può essere modificata. Se è in corso l'aggiunta di un nuovo filtro, selezionare una tabella dall'elenco a discesa. Le tabelle vengono visualizzate nella casella di riepilogo solo se sono selezionate nella pagina **Articoli** e non dispongono ancora di un filtro di riga. Per definire un nuovo filtro di riga quando per la tabella ne è già disponibile uno:  
  
    1.  Nella finestra di dialogo **Aggiungi filtro** fare clic su **Annulla** .  
  
    2.  Nella pagina **Filtro righe tabella** selezionare la tabella nel riquadro del filtro e fare clic su **Modifica**.  
  
    3.  Nella finestra di dialogo **Modifica filtro** modificare un filtro esistente.  
  
2.  **Completare l'istruzione per il filtro per identificare le righe della tabella che verranno ricevute dai Sottoscrittori**  
  
     Consente di definire una nuova istruzione per il filtro o di modificarne una esistente. Nella casella di riepilogo **Colonne** vengono elencate tutte le colonne in fase di pubblicazione appartenenti alla tabella selezionata in **Selezionare la tabella da filtrare**. L'area di testo **Istruzione per il filtro** contiene il testo predefinito, nel formato seguente:  
  
     `SELECT <published_columns> FROM [schema].[tablename] WHERE`  
  
     Questo testo non può essere modificato. Digitare la clausola di filtro dopo la parola chiave WHERE utilizzando la sintassi [!INCLUDE[tsql](../../includes/tsql-md.md)] standard. Se il server di pubblicazione è un server di pubblicazione Oracle, la clausola WHERE deve essere conforme alla sintassi delle query Oracle. Se possibile, evitare di usare filtri complessi. I filtri statici e con parametri possono migliorare i tempi di elaborazione per le pubblicazioni ed è pertanto opportuno che le istruzioni per il filtro siano le più semplici possibile.  
  
    > [!IMPORTANT]  
    >  Per motivi di prestazioni, è consigliabile non applicare funzioni ai nomi di colonna, ad esempio `LEFT([MyColumn]) = SUSER_SNAME()`, nelle clausole di filtro di riga con parametri per pubblicazioni di tipo merge. Se si usano HOST_NAME in una clausola di filtro e si sostituisce il valore HOST_NAME, può essere necessario convertire i tipi di dati tramite l'istruzione CONVERT. Per altre informazioni sulle procedure consigliate in questo caso, vedere la sezione relativa alla sostituzione del valore HOST_NAME() nell'argomento [Parameterized Row Filters](merge/parameterized-filters-parameterized-row-filters.md).  
  
3.  **Specificare se i dati di questa tabella dovranno essere inviati a una o più sottoscrizioni**  
  
     Solo[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versioni successive, solo replica di tipo merge. La replica di tipo merge consente di specificare il tipo di partizioni più adatte ai dati e all'applicazione. Se si seleziona **Una riga di questa tabella verrà inviata a una sola sottoscrizione**, viene impostata l'opzione relativa alle partizioni non sovrapposte della replica di tipo merge. Le partizioni non sovrapposte vengono utilizzate insieme alle partizioni pre-calcolate per migliorare le prestazioni per ridurre il costo di caricamento associato alle partizioni pre-calcolate. Il vantaggio a livello di prestazioni delle partizioni non sovrapposte è più evidente quando i filtri con parametri e i filtri join utilizzati sono più complessi. Se si seleziona questa opzione è necessario, tuttavia, verificare che i dati vengano partizionati in modo che una riga non possa essere replicata in più Sottoscrittori. Per altre informazioni, vedere la sezione relativa all'impostazione delle opzioni delle partizioni nell'argomento [Parameterized Row Filters](merge/parameterized-filters-parameterized-row-filters.md).  
  
 Dopo aver aggiunto o modificato un filtro, fare clic su **OK** per salvare le modifiche e chiudere la finestra di dialogo. Il filtro specificato viene analizzato ed eseguito sulla tabella nella clausola SELECT. Se nell'istruzione di filtro sono presenti errori di sintassi o di altro tipo, verrà visualizzato un apposito messaggio di notifica e sarà possibile modificare l'istruzione.  
  
## <a name="see-also"></a>Vedere anche  
 [Create a Publication](publish/create-a-publication.md)   
 [Visualizzare e modificare le proprietà della pubblicazione](publish/view-and-modify-publication-properties.md)   
 [Filtrare i dati pubblicati](publish/filter-published-data.md)   
 [Join Filters](merge/join-filters.md)   
 [Parameterized Row Filters](merge/parameterized-filters-parameterized-row-filters.md)   
 [Pubblicare dati e oggetti di database](publish/publish-data-and-database-objects.md)  
  
  
