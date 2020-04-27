---
title: Importare i valori da un file di Excel in un dominio | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql12.dqs.kb.failingvalues.f1
- sql12.dqs.kb.importfailing.f1
- sql12.dqs.kb.importselect.f1
ms.assetid: 04cde693-2043-477f-8417-fcc463ca7195
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 74be4b3e924d02f6992b927af35c7774c3ea0ae4
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "65484308"
---
# <a name="import-values-from-an-excel-file-into-a-domain"></a>Importare i valori da un file di Excel in un dominio
  In questo argomento viene descritto come importare i valori da un file di Excel in un dominio in [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS). L'utilizzo di un file di Excel per importare valori di dominio nell'applicazione [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] semplifica il processo della generazione delle informazioni, risparmiando tempo e fatica. In questo modo è possibile di importare un elenco di valori di dati validi da un file di Excel o un file di testo in un dominio. Da un file di Excel è possibile importare i valori di dominio in uno o più domini in una Knowledge Base. Per ulteriori informazioni sull'importazione di domini in una Knowledge base, vedere l'articolo relativo all' [importazione di domini da un file di Excel in individuazione](../../2014/data-quality-services/import-domains-from-an-excel-file-in-knowledge-discovery.md) informazioni. L'esportazione in un file di Excel non è supportata.  
  
 È possibile importare i valori di dati in due modi:  
  
-   Creare un nuovo dominio, quindi importarvi i valori da un file di Excel. In questo caso, tutti i valori vengono aggiunti al dominio.  
  
-   Importare i valori in un dominio popolato esistente. In questo caso, vengono importati solo i nuovi valori. I valori già presenti non verranno importati.  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> Prerequisiti  
 Per importare i domini da un file di Excel, è necessario che Excel sia installato nel computer in cui è installata l'applicazione [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] in modo da potere importare i valori di dominio o un dominio completo. È necessario avere creato un file di Excel con i valori di dominio (vedere [How the import works](#How)). Infine, è necessario avere creato e aperto una Knowledge Base in cui importarvi il dominio.  
  
###  <a name="security"></a><a name="Security"></a> Sicurezza  
  
####  <a name="permissions"></a><a name="Permissions"></a> Autorizzazioni  
 È necessario disporre del ruolo dqs_kb_editor o dqs_administrator nel database DQS_MAIN per importare i valori di dominio da un file di Excel.  
  
##  <a name="import-values-from-an-excel-file-into-a-domain"></a><a name="Import"></a>Importare i valori da un file di Excel in un dominio  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][Eseguire l'applicazione Data Quality Client](../../2014/data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Nella schermata iniziale del [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] aprire una Knowledge Base nell'attività Gestione dominio.  
  
3.  Se si aggiungono valori a un nuovo dominio, creare il nuovo dominio utilizzando l'icona **Crea un dominio** , quindi selezionare il nuovo dominio nell'elenco di domini.  
  
4.  In caso di aggiunta di valori a un dominio esistente, selezionare il dominio nell'elenco di domini.  
  
5.  Fare clic sulla scheda **Valori di dominio** , fare clic sull'icona **Importa valori** nella barra delle icone, quindi fare clic su **Importa valori validi da Excel**.  
  
6.  Nella finestra di dialogo **Importa valori di dominio** fare clic su **Sfoglia**.  
  
7.  Nella finestra di dialogo **Seleziona file** spostarsi nella cartella che contiene il file di Excel dal quale si desidera importare i valori di dominio, selezionare il file (con estensione XLSX, XLS o CSV), quindi fare clic su **Apri**. Il file deve trovarsi nel client dal quale si esegue DQS o in un file della condivisione a cui l'utente può accedere.  
  
8.  Nell'elenco a discesa **Foglio di lavoro** selezionare il foglio di lavoro da cui eseguire l'importazione.  
  
9. Selezionare **Utilizza la prima riga come intestazione** se la prima riga del foglio di calcolo rappresenta il nome di dominio e tutte le altre righe rappresentano valori di dominio validi.  
  
10. Fare clic su **OK**. Verrà visualizzato un indicatore di stato in cui è riportato il numero di valori importati e non importati e il numero totale di valori. Fare clic sul pulsante **Annulla** per annullare il processo.  
  
11. Verificare che nella finestra di dialogo **Importa valori di dominio** sia visualizzato "Importazione completata". Controllare in questa finestra di dialogo quali valori sono stati importati e quali non lo sono stati. La finestra indica il nome e il percorso del file, lo stato di completamento dell'operazione, il numero di valori importati e non importati e il numero totale di valori elaborati.  
  
12. Per i valori che non sono stati importati, fare clic su **Log** per visualizzare la finestra di dialogo **Importa valori di dominio - Valori errati** per vedere il motivo per cui l'operazione di importazione non è riuscita. Nella colonna **Valore errato** vengono visualizzati i valori di cui non è stato possibile eseguire l'importazione da un file di Excel in un dominio e nella colonna **Motivo** viene descritto il motivo per cui l'importazione non è riuscita. Fare clic su **Copia negli Appunti** per copiare la tabella **Valore errato** negli Appunti da cui è possibile copiarla in un altro programma, ad esempio un foglio di calcolo di Excel o un file di Blocco note. Fare clic su **OK** per chiudere la finestra di dialogo **Valori errati** .  
  
13. Fare clic su **OK** per completare l'operazione di importazione e chiudere la finestra di dialogo. Al termine dell'importazione, l'elenco di valori di dominio nella pagina **Valori di dominio** viene aggiornato per includere i nuovi valori importati. Il filtro viene modificato in **Tutti i valori** e viene selezionato **Mostra solo nuovi** . Quando dopo l'operazione di importazione si seleziona **Mostra solo nuovi** , verranno visualizzati solo i valori importati dal file di Excel.  
  
14. Fare clic su **Fine** per aggiungere i valori alla Knowledge Base.  
  
##  <a name="follow-up-after-importing-values-from-an-excel-file-into-a-domain"></a><a name="FollowUp"></a>Completamento: dopo l'importazione di valori da un file di Excel in un dominio  
 Dopo avere importato i valori in un dominio, è possibile eseguire ulteriori attività di gestione sul dominio, quali l'individuazione delle informazioni per aggiungere informazioni al dominio o l'aggiunta di criteri di corrispondenza al dominio. Per altre informazioni, vedere [Eseguire l'individuazione delle informazioni](../../2014/data-quality-services/perform-knowledge-discovery.md), [Gestione di un dominio](../../2014/data-quality-services/managing-a-domain.md) o [Creare criteri di corrispondenza](../../2014/data-quality-services/create-a-matching-policy.md).  
  
##  <a name="importing-synonyms"></a><a name="Synonyms"></a>Importazione di sinonimi  
 I sinonimi vengono importati come segue:  
  
-   In primo luogo vengono importati tutti i valori, quindi viene stabilita la connessione ai sinonimi.  
  
-   Se non è possibile connettersi ai sinonimi, verrà visualizzato un errore nella schermata del log. È possibile che i valori iniziali e i sinonimi nel file vengano importati nel dominio, ma che non vengano impostati come sinonimi.  
  
 Al processo di impostazione delle connessioni ai sinonimi vengono applicate le condizioni seguenti:  
  
-   Se il valore iniziale nel file di Excel esiste già nel dominio come sinonimo di un altro valore, sarà necessario impostare i sinonimi manualmente, ad esempio nel file di Excel sarà necessario impostare che il valore A è il valore iniziale per il valore B, ma nel valore di dominio A è sinonimo del valore C. Oltre a impostare i sinonimi manualmente al termine dell'importazione, è inoltre possibile scollegare i valori che al momento sono sinonimi, ad esempio scollegare i valori A e C sopra riportati, quindi importare il file.  
  
-   Se il sinonimo è già connesso a un altro valore iniziale, sarà necessario impostare i sinonimi manualmente.  
  
-   Se per qualsiasi motivo i valori non possono essere connessi manualmente nell'applicazione, l'operazione non potrà essere eseguita tramite l'operazione di importazione.  
  
##  <a name="how-the-import-works"></a><a name="How"></a>Funzionamento dell'importazione  
 Con questa operazione vengono importati i valori seguenti:  
  
 In DQS l'operazione di importazione da un file di Excel viene effettuata come segue:  
  
-   Vengono importati i valori corretti e i valori nuovi. Se uno o più dei valori di dominio importati esistono già, i valori non verranno importati.  
  
-   Un valore in contrasto con una regola di dominio verrà importato come valore non valido.  
  
-   Se un valore non è del tipo di dati del dominio o è Null, non verrà importato dal file.  
  
-   I valori vengono importati nell'ordine in cui vengono visualizzati nel file.  
  
-   Ogni riga rappresenta un valore di dominio.  
  
-   La prima riga rappresenta nomi di dominio o è il primo record o valore di dati, a seconda dell'impostazione della casella di controllo **Utilizza la prima riga come intestazione** . Se si seleziona **Utilizza la prima riga come intestazione** con un file XLSX o XLS, tutti i nomi di colonna null verranno convertiti automaticamente in F*n*e a tutte le colonne duplicate verrà aggiunto un numero.  
  
-   Se si annulla l'operazione di importazione prima del completamento, verrà eseguito il rollback dell'operazione e non verrà importato alcun dato.  
  
-   I valori nella prima colonna vengono importati nel dominio. Se oltre alla prima colonna, vengono popolate una o più colonne aggiuntive, i valori in tali colonne verranno aggiunti come sinonimi (vedere [Importazione di sinonimi](#Synonyms)).  
  
    -   Il formato previsto è che i valori della prima colonna saranno valori iniziali, mentre dalla seconda colonna in poi saranno sinonimi.  
  
    -   È possibile importare più sinonimi nella stessa riga o in righe diverse. Se ad esempio si desidera importare "NYC" e "New York City" come sinonimi per "New York", è possibile importare una sola riga con "New York" nella colonna 1, "NYC" nella colonna 2 e "New York City" nella colonna 3. In alternativa, è possibile importare una riga con "New York" nella colonna 1 e "NYC" nella colonna 2 e un'altra riga con "New York" nella colonna 1 e "New York City" nella colonna 2. Si noti che se il valore "New York" è già presente nel dominio, verranno aggiunti solo i sinonimi e durante il processo di importazione non verrà visualizzato alcun messaggio di errore in cui si indica che il valore esiste già. Se il primo valore non esiste già, verrà aggiunto al dominio.  
  
 Al file di Excel utilizzato per l'importazione vengono applicate le regole seguenti:  
  
-   L'estensione del file di Excel può essere XLSX, XLS o CSV. È necessario che Microsoft Excel sia installato nel computer in cui è installata l'applicazione [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] per poter importare i valori di dominio o un dominio completo. Sono supportate le versioni di Excel dalla 2003 in poi. Se viene utilizzata la versione a 64 bit di Excel, sono supportati solo i file di Excel 2003, mentre non sono supportati i file di Excel 2007 o 2010.  
  
-   I file di Excel di tipo XLSX non sono supportati per un'installazione di Excel a 64 bit. Se si utilizza una versione di Excel a 64 bit, salvare il foglio di calcolo come file XLS o CSV oppure installare una versione di Excel a 32 bit.  
  
-   Nei file XLSX e XLS il tipo di dati della colonna viene determinato dalle prime otto righe. Se il tipo di dati della colonna delle prime otto righe è misto, la colonna sarà di tipo stringa. Se una cella dalla riga 9 in poi non è conforme a tale tipo di dati, verrà fornito un valore null.  
  
-   Nei file CSV il tipo di dati viene determinato dal tipo di dati più prevalente nelle prime otto righe.  
  
-   Se il formato del file di Excel non è corretto o è danneggiato, l'operazione di importazione genererà un errore.  
  
  
