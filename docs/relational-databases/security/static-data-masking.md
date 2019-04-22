---
title: Maschera dati statica | Microsoft Docs
ms.date: 04/10/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
ms.assetid: a62f4ff9-2953-42ca-b7d8-1f8f527c4d66
author: aliceku
ms.author: aliceku
manager: ajayj
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 91b0fde06d400b2c519e9e6c86854197a2aecd13
ms.sourcegitcommit: 323d2ea9cb812c688cfb7918ab651cce3246c296
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/18/2019
ms.locfileid: "59516467"
---
# <a name="static-data-masking"></a>Maschera dati statica
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

La funzionalità Mascheramento statico dei dati è stata rilasciata come componente di [SQL Server Management Studio](../../ssms/sql-server-management-studio-ssms.md) 18.0 anteprima 5 e versioni successive. È stato deciso che il prototipo corrente non soddisfa le aspettative dei clienti. Questa funzionalità non verrà pertanto sviluppata ulteriormente. Verranno pubblicate informazioni aggiornate sui piani di Microsoft nel caso venga individuato un possibile sostituto.

![Mascheramento dei dati statico](../../relational-databases/security/media/sql-static-data-masking/static_data_masking_intro_image.PNG)


## <a name="what-is-static-data-masking"></a>Cos'è la maschera dati statica? 
La maschera dati statica è una funzionalità di SQL Server Management Studio che consente agli utenti di creare una copia mascherata di un database. La funzionalità è stata sviluppata per le organizzazioni che devono condividere dati, alcuni dei quali sensibili, tra team o con altre organizzazioni. 

Grazie alla sostituzione di dati sensibili (dati pre-maschera) con nuovi dati (dati post-maschera), la maschera dati statica facilita gli scenari seguenti: 
- Sviluppo e test 
- Analisi e creazione di report aziendali 
- Risoluzione dei problemi 
- Condivisione del database con un consulente, un team di ricerca o qualsiasi terza parte 

L'esempio seguente illustra come funziona la maschera dati statica. Prima del mascheramento, la colonna contiene codici fiscali. Dopo il mascheramento, le prime cinque cifre di ogni codice fiscale sono state sostituite da numeri generati in modo casuale.

| Codice fiscale statunitense (pre-maschera)   | Codice fiscale statunitense (post-maschera)  |
| ------------- | ------------- |
| 140-38-9110 | 302-92-9110 |
| 463-34-5535 | 189-70-5535 |
| 116-30-8733 | 201-01-8733 |
| 209-36-1971 | 683-10-1971 |
| 372-38-6948 | 372-38-6948 |
| 267-64-2334 | 100-03-2334 |
| 523-93-4176 | 582-20-4176 |
| 573-91-5137 | 730-20-5137 |
| 612-72-1026 | 369-40-1026 |

Gli utenti della maschera dati statica possono scegliere tra diverse funzioni di maschera. A seconda della funzione di maschera, i dati pre-maschera e quelli post-maschera possono essere altamente correlati o non correlati affatto. Una funzione di maschera che esegue una selezione in ordine casuale determina dati post-maschera altamente correlati ai dati pre-maschera. 

| Codice fiscale statunitense (pre-maschera) | Codice fiscale statunitense (post-maschera) |
| ------------- | ------------- |
| 140-38-9110 | 612-72-1026 |  
| 463-34-5535 | 372-38-6948 | 
| 116-30-8733 | 523-93-4176 |
| 209-36-1971 | 209-36-1971 | 
| 372-38-6948 | 140-38-9110 |
| 267-64-2334 | 463-34-5535 | 
| 523-93-4176 | 573-91-5137 | 
| 573-91-5137 | 267-64-2334 | 
| 612-72-1026 | 116-30-8733 |

Una funzione di maschera che esegue una sostituzione con il valore NULL determina dati post-maschera non correlati ai dati pre-maschera. 
 
| Codice fiscale statunitense (pre-maschera) | Codice fiscale statunitense (post-maschera) |
| ------------- | ------------- |
| 140-38-9110 | NULL |  
| 463-34-5535 | NULL | 
| 116-30-8733 | NULL |
| 209-36-1971 | NULL | 
| 372-38-6948 | NULL |
| 267-64-2334 | NULL | 
| 523-93-4176 | NULL | 
| 573-91-5137 | NULL | 
| 612-72-1026 | NULL |

## <a name="how-does-static-data-masking-work"></a>Come funziona la maschera dati statica?
La maschera dati statica opera a livello di colonna. Gli utenti selezionano le colonne da mascherare e, per ogni colonna selezionata, la funzione di maschera da applicare. È possibile scegliere tra diverse funzioni di maschera che sono descritte in dettaglio in [Funzioni di maschera](#masking-functions). 

La maschera dati statica crea quindi una copia del database. Per il database SQL di Azure, la copia viene eseguita tramite la [funzione di copia](https://azure.microsoft.com/blog/static-data-masking-preview/). Per SQL Server viene eseguita tramite un'operazione di backup seguita da un'operazione di ripristino. Quindi, per ogni colonna, la maschera dati statica inizia a sostituire i dati pre-maschera con i dati post-maschera in base alla funzione di maschera selezionata. 

La sostituzione avviene a livello di archiviazione. Di conseguenza, non sarà possibile recuperare i dati pre-maschera dalla copia mascherata del database dopo il completamento della maschera dati statica.

## <a name="how-to-guide"></a>Guida pratica

Di seguito è riportata una guida dettagliata per l'esecuzione della maschera dati statica. 
 
1. Avviare SQL Server Management Studio. Connettersi al database. Nel riquadro **Esplora oggetti** sul lato sinistro espandere la cartella Database. Fare clic con il pulsante destro del mouse sul database da mascherare. Fare clic su **Attività**. Fare clic su **Maschera database... (anteprima)**.
 
 ![Menu Attività](../../relational-databases/security/media/sql-static-data-masking/task_data_masking.PNG)
 
2. Verrà aperta la finestra di configurazione maschera in cui sono visualizzate tutte le tabelle presenti nel database. Le tabelle sono presentate in base allo schema e quindi in ordine alfabetico all'interno di uno schema. 
 
 ![Interfaccia utente](../../relational-databases/security/media/sql-static-data-masking/ui_dropdown.PNG)
 
3. Fare clic sull'icona a discesa accanto al nome di tabella per ottenere un elenco di tutte le colonne della tabella. Per ogni colonna della tabella è specificato il tipo di dati della colonna e se la colonna ammette i valori NULL. Questo tipo di colonna è una colonna che può ricevere il valore NULL. 
 
 ![Elenco a discesa della tabella](../../relational-databases/security/media/sql-static-data-masking/ui_dropdown_column.png)
 
4. Selezionare tutte le colonne da mascherare e la funzione di maschera da applicare. I tipi di maschera disponibili sono maschera **Shuffle** (Ordine casuale), maschera **Group Shuffle** (Ordine casuale gruppo), maschera **Single value** (Valore singolo), maschera **NULL**, maschera **String Composite** (Stringa composita). 
 
 ![Elenco a discesa delle funzioni di maschera](../../relational-databases/security/media/sql-static-data-masking/masking_functions.PNG)
 
 NOTA: la maggior parte di queste funzioni di maschera ha parametri di configurazione aggiuntivi. Per la maschera selezionata in ordine casuale, la maschera dati statica include un parametro predefinito. Per la maschera selezionata in ordine casuale gruppo, la maschera a valore singolo e la maschera con stringa composita, i parametri di configurazione devono essere specificati dall'utente. Per modificare o specificare i parametri di configurazione, fare clic sull'opzione **Configura…** e specificare un valore (alternativo) per il parametro nella finestra di dialogo visualizzata. Descrizioni dettagliate di ogni funzione di maschera sono disponibili in [Funzioni di maschera](#masking-functions).
 
 ![Pulsante di configurazione delle funzioni di maschera](../../relational-databases/security/media/sql-static-data-masking/masking_functions_configure.png)
 
 Per errori e avvisi correlati alla configurazione e allo schema, le scelte di configurazione della maschera vengono convalidate istantaneamente.  Ogni rilevamento viene visualizzato a sinistra come icona su cui è possibile passare il puntatore del mouse per ottenere dettagli aggiuntivi. 
 
 L'esempio seguente illustra la maschera NULL selezionata dall'utente per una colonna che non ammette i valori NULL (vincolo NOT NULL).
 
 ![Errore del meccanismo di convalida](../../relational-databases/security/media/sql-static-data-masking/validation_mechanism_error_message.PNG)
 
 L'esempio seguente illustra la maschera selezionata in ordine casuale gruppo selezionata dall'utente per una sola colonna. La selezione in ordine casuale gruppo richiede un minimo di due colonne. Viene pertanto emesso un avviso. 
 
 ![Avviso del meccanismo di convalida](../../relational-databases/security/media/sql-static-data-masking/validation_warning.PNG)
 
5. È possibile salvare la configurazione di maschera completa in un file XML per un uso successivo.  Nei database SQL di Azure e in quelli locali la configurazione delle funzioni di maschera è identica, ma esistono alcune lievi differenze nel modo in cui altre proprietà, ad esempio il percorso del file di backup, vengono salvate. Per salvare la configurazione, fare clic su **Save Config** (Salva configurazione), specificare un nome di file e fare clic su Salva.  Gli utenti possono in seguito caricare un file di configurazione esistente usando **Load Config** (Carica configurazione). È consigliabile usare file di configurazione per le tabelle con un numero elevato di colonne. 
 
 ![File di configurazione](../../relational-databases/security/media/sql-static-data-masking/load_save_config.PNG)
 
6. La maschera dati statica crea una cartella denominata Maschera dati statica all'interno della cartella **Documenti** dell'utente e vi inserisce i file di log. I file di log possono essere utili per le attività di debug. Il nome del file di log è indicato nella parte inferiore della finestra di configurazione. 
  
 
7. (Solo SQL Server) Se si usa la maschera dati statica in un database locale, questa eseguirà un'operazione di backup/ripristino. In **Step 2: Clone .BAK file Location** (Passaggio 2: Percorso del file .BAK clone) specificare il percorso nel server in cui verrà archiviato il file di backup. 

## <a name="masking-functions"></a>Funzioni di maschera

### <a name="null-masking"></a>Maschera NULL

La maschera NULL sostituisce tutti i valori nella colonna con NULL. Se la colonna non ammette i valori NULL, lo strumento di maschera dati statica restituisce un errore. 

### <a name="single-value-masking"></a>Maschera a valore singolo

La maschera a valore singolo sostituisce tutti i valori nella colonna con un singolo valore fisso. Questo valore è specificato dall'utente. Il formato dell'input deve essere convertibile nel tipo della colonna selezionata. Per specificare il valore, fare clic su **Configura...**, specificare un valore e quindi fare clic su **Okay**. 

![Parametro della maschera a valore singolo](../../relational-databases/security/media/sql-static-data-masking/single_value_parameter.PNG)


### <a name="shuffle-masking"></a>Maschera selezionata in ordine casuale

Tutti i valori della colonna vengono disposti in ordine casuale in nuove righe. Non vengono generati nuovi dati. La maschera selezionata in ordine casuale consente di mantenere le voci NULL nella colonna. A tale scopo, fare clic su **Configura...**  e selezionare la casella Maintain NULL positions (Mantieni posizioni NULL).

![Parametro della maschera selezionata in ordine casuale](../../relational-databases/security/media/sql-static-data-masking/shuffle_parameter.PNG)

Di seguito è riportato un esempio di maschera selezionata in ordine casuale con valori NULL prima non mantenuti e poi mantenuti.


| Codice fiscale statunitense (pre-maschera) | Codice fiscale statunitense (post-maschera con voci NULL in ordine casuale) | Codice fiscale statunitense (post-maschera con voci NULL non in ordine casuale) |
| ------------- | ------------- | ------------- |
| 116-30-8733 | 612-72-1026 | 463-34-5535 |
| 140-38-9110 | NULL | 573-91-5137  |
| 209-36-1971 | 523-93-4176 | 140-38-9110 |
| NULL | 209-36-1971 | NULL |
| 463-34-5535 | 140-38-9110 | 116-30-8733  |
| 523-93-4176 | 463-34-5535 | 612-72-1026  |
| NULL | 573-91-5137 | NULL |
| 573-91-5137 | NULL | 523-93-4176 |
| 612-72-1026  | 116-30-8733  | 209-36-1971 |  

### <a name="group-shuffle-masking"></a>Maschera selezionata in ordine casuale gruppo
La selezione in ordine casuale gruppo associa diverse colonne in un gruppo di ordine casuale. Le colonne in un gruppo di ordine casuale verranno ordinate in modo casuale. L'utente deve specificare il nome del gruppo di ordine casuale usando l'opzione **Configura...** .

![Parametro della maschera selezionata in ordine casuale gruppo](../../relational-databases/security/media/sql-static-data-masking/group_shuffle_parameter.PNG)

Le selezioni in ordine casuale gruppo avvengono all'interno della stessa tabella. Se lo stesso nome di gruppo di ordine casuale viene usato in più tabelle, le due selezioni in ordine casuale gruppo sono azioni indipendenti. Il nome del gruppo deve essere lo stesso per ogni colonna da includere nel gruppo. Per il nome è rilevante la distinzione tra maiuscole e minuscole. Più gruppi di ordine casuale (con nomi diversi) possono essere presenti nella stessa tabella. 

### <a name="string-composite-masking"></a>Maschera con stringa composita

La maschera con stringa composita genera stringhe casuali in base a un modello. È stata progettata per stringhe che per essere una voce valida devono seguire un modello predefinito. Ad esempio, i codici fiscali statunitensi hanno il formato 123-45-6789. La sintassi per la maschera con stringa composita è specificata nella finestra di dialogo in cui l'utente deve immettere il modello.

![Parametro della maschera con stringa composita](../../relational-databases/security/media/sql-static-data-masking/string_composite.PNG)

La maschera con stringa composita offre tre modelli di esempio che è possibile testare facendo clic su di essi. Se si fa clic sul numero di telefono, la casella del modello viene automaticamente popolata con la formula necessaria per generare numeri di telefono statunitensi casuali.

![Esempio di parametro della maschera con stringa composita](../../relational-databases/security/media/sql-static-data-masking/string_composite_phone_example.PNG)

La maschera con stringa composita include anche una modalità avanzata che consente di sostituire le sottosezioni dei dati esistenti con stringhe generate dal modello. La parte sostituita della stringa viene determinata dal gruppo Capture in un'espressione regolare. Ad esempio, è possibile sostituire la parte relativa al nome utente di un indirizzo di posta elettronica mantenendo il dominio oppure sostituire il numero di telefono mantenendo l'indicativo di località. Altre informazioni sulle espressioni regolari sono disponibili [qui](https://docs.microsoft.com/dotnet/standard/base-types/regular-expression-language-quick-reference).

![Esempio di parametro della maschera con stringa composita avanzata](../../relational-databases/security/media/sql-static-data-masking/string_composite_advanced.PNG)

La maschera con stringa composita e la relativa modalità avanzata possono essere usate solo per le colonne con [tipi di dati](../../t-sql/data-types/data-types-transact-sql.md) char, varchar, text, nchar, nvarchar, ntext.

## <a name="limitations"></a>Limitazioni 

La maschera dati statica presenta le limitazioni seguenti:

- La maschera dati statica non supporta i database con [tabelle temporali](../../relational-databases/tables/temporal-tables.md).

- La maschera dati statica non maschera le tabelle [ottimizzate per la memoria](../../relational-databases/in-memory-oltp/introduction-to-memory-optimized-tables.md).

- La maschera dati statica non maschera le [colonne calcolate](../../relational-databases/tables/specify-computed-columns-in-a-table.md) e le colonne [Identity](../../t-sql/statements/create-table-transact-sql-identity-property.md).

- La maschera dati statica non supporta i database Hyperscale SQL di Azure.

- La maschera dati statica non supporta i tipi di dati Geometry e Geography. 

La maschera dati statica presenta inoltre tre limitazioni nelle capacità di mascheramento:

- La maschera dati statica non aggiorna le [statistiche di istogramma](../../relational-databases/statistics/statistics.md). Di conseguenza, dopo il completamento della maschera dati statica, la copia mascherata del database potrebbe ancora contenere dati sensibili nelle statistiche di istogramma. Valutare l'esecuzione di [UPDATE STATISTICS](../../t-sql/statements/update-statistics-transact-sql.md) per porre rimedio a questo problema. 

- Se la maschera dati statica restituisce un errore, tutte le operazioni di mascheramento vengono sospese. La copia del database non viene eliminata e può contenere informazioni riservate. L'utente è responsabile dell'eliminazione della copia del database se la maschera dati statica restituisce un errore. 

- (Solo SQL Server) Dopo il completamento della maschera dati statica, i [file di dati](../../relational-databases/databases/database-files-and-filegroups.md) e il [file di log](../../relational-databases/logs/the-transaction-log-sql-server.md) possono ancora contenere parti di dati sensibili nella memoria non allocata. Questi dati sensibili possono essere recuperabili con un editor hex a cui sia stato concesso l'accesso ai file di dati e al file di log.

## <a name="see-also"></a>Vedere anche  
 [Maschera dati dinamica](../../relational-databases/security/dynamic-data-masking.md)   
 [Introduzione alla maschera dati statica del database SQL](https://azure.microsoft.com/documentation/articles/sql-database-static-data-masking-get-started/)  
