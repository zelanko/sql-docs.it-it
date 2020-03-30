---
title: Usare una destinazione recordset | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Recordset destination
ms.assetid: a7b143dc-8008-404f-83b0-b45ffbca6029
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 94c1d149dd152a9cf83e5464cde2c56ec9b42af7
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "71290993"
---
# <a name="use-a-recordset-destination"></a>Utilizzo di una destinazione recordset

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  La destinazione recordset non salva i dati in un'origine dati esterna, ma in un recordset in memoria archiviato in una variabile del pacchetto [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] del tipo di dati **Object** . Dopo che la destinazione recordset ha salvato i dati, in genere si utilizza un contenitore Ciclo Foreach con l'enumeratore Foreach ADO per elaborare una riga del recordset alla volta. L'enumeratore Foreach ADO salva il valore di ogni colonna della riga corrente in una variabile del pacchetto distinta. Quindi, le attività configurate nel contenitore Ciclo Foreach leggono tali valori dalle variabili ed eseguono alcune azioni.  
  
 È possibile utilizzare la destinazione recordset in molti scenari diversi. Di seguito sono riportati alcuni esempi:  
  
-   È possibile usare un'attività Invia messaggi e il linguaggio delle espressioni di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] per inviare un messaggio di posta elettronica personalizzato per ogni riga del recordset.  
  
-   È possibile utilizzare un componente script configurato come origine, all'interno di un'attività Flusso di dati, per leggere i valori delle colonne del flusso di dati. Quindi, è possibile utilizzare trasformazioni e destinazioni per trasformare e salvare la riga. In questo esempio l'attività Flusso di dati viene eseguita una volta per ogni riga.  
  
 Nelle sezioni seguenti viene descritto il processo generale di utilizzo della destinazione recordset e viene quindi illustrato un esempio specifico di utilizzo della destinazione.  
  
## <a name="general-steps-to-using-a-recordset-destination"></a>Passaggi generali per l'utilizzo di una destinazione recordset  
 Nella procedura seguente sono riepilogati i passaggi necessari per salvare dati in una destinazione recordset e quindi utilizzare il contenitore Ciclo Foreach per elaborare ogni riga.  
  
#### <a name="to-save-data-to-a-recordset-destination-and-process-each-row-by-using-the-foreach-loop-container"></a>Per salvare dati in una destinazione recordset ed elaborare ogni riga tramite il contenitore Ciclo Foreach  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]creare o aprire un pacchetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
2.  Creare una variabile che conterrà il recordset salvato in memoria dalla destinazione recordset e impostare il relativo tipo su **Object**.  
  
3.  Creare variabili aggiuntive dei tipi appropriati per contenere i valori di ogni colonna del recordset che si desidera utilizzare.  
  
4.  Aggiungere e configurare la gestione connessione richiesta dall'origine dati che si intende utilizzare nel flusso di dati.  
  
5.  Aggiungere un'attività Flusso di dati al pacchetto, quindi nella scheda Flusso di dati di Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] configurare le origini e le trasformazioni per il caricamento e la trasformazione dei dati.  
  
6.  Aggiungere una destinazione recordset al flusso di dati e connetterla alle trasformazioni. Per la proprietà **VariableName** della destinazione recordset, immettere il nome della variabile creata per contenere il recordset.  
  
7.  Nella scheda Flusso di controllo di Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] aggiungere un contenitore Ciclo Foreach e connetterlo dopo l'attività Flusso di dati. Aprire quindi **Editor ciclo Foreach** per configurare il contenitore con le impostazioni seguenti:  
  
    1.  Nella pagina **Raccolta** selezionare l'enumeratore Foreach ADO. Quindi, per **Variabile di origine oggetto ADO**, selezionare la variabile che contiene il recordset.  
  
    2.  Nella pagina **Mapping variabili** eseguire il mapping dell'indice in base zero di ogni colonna che si desidera usare alla variabile appropriata.  
  
         A ogni iterazione del ciclo, l'enumeratore popola queste variabili con i valori delle colonne della riga corrente.  
  
8.  Nel contenitore Ciclo Foreach aggiungere e configurare attività per elaborare una riga del recordset alla volta leggendo i valori dalle variabili.  
  
## <a name="example-of-using-the-recordset-destination"></a>Esempio di utilizzo della destinazione recordset  
 Nell'esempio seguente l'attività Flusso di dati carica informazioni sui dipendenti di [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] dalla tabella Sales.SalesPerson in una destinazione recordset. Quindi, un contenitore Ciclo Foreach legge una riga di dati alla volta e chiama un'attività Invia messaggi. L'attività Invia messaggi utilizza espressioni per inviare un messaggio di posta elettronica personalizzato a ogni venditore sull'importo del premio ricevuto.  
  
#### <a name="to-create-the-project-and-configure-the-variables"></a>Per creare il progetto e configurare le variabili  
  
1.  In [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]creare un nuovo progetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
2.  Scegliere **Variabili** dal menu **SSIS**.  
  
3.  Nella finestra **Variabili** creare le variabili che conterranno il recordset e i valori delle colonne della riga corrente:  
  
    1.  Creare una variabile denominata **BonusRecordset**e impostare il relativo tipo su **Object**.  
  
         La variabile **BonusRecordset** contiene il recordset.  
  
    2.  Creare una variabile denominata **EmailAddress**e impostare il relativo tipo su **String**.  
  
         La variabile **EmailAddress** contiene l'indirizzo di posta elettronica del venditore.  
  
    3.  Creare una variabile denominata **FirstName**e impostare il relativo tipo su **String**.  
  
         La variabile **FirstName** contiene il nome del venditore.  
  
    4.  Creare una variabile denominata **Bonus**e impostare il relativo tipo su **Double**.  
  
         La variabile **Bonus** contiene l'importo del premio del venditore.  
  
#### <a name="to-configure-the-connection-managers"></a>Per configurare le gestioni connessioni  
  
1.  Nell'area Gestioni connessioni di Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] aggiungere e configurare una nuova gestione connessione OLE DB che si connette al database di esempio [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] .  
  
     L'origine OLE DB nell'attività Flusso di dati utilizzerà questa gestione connessione per recuperare dati.  
  
2.  Nell'area Gestioni connessioni aggiungere e configurare una nuova gestione connessione SMTP che si connette a un server SMTP disponibile.  
  
     L'attività Invia messaggi nel contenitore Ciclo Foreach utilizzerà questa gestione connessione per inviare posta elettronica.  
  
#### <a name="to-configure-the-data-flow-and-the-recordset-destination"></a>Per configurare il flusso di dati e la destinazione recordset  
  
1.  Nella scheda **Flusso di controllo** di Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] aggiungere un'attività Flusso di dati nell'area di progettazione.  
  
2.  Nella scheda **Flusso di dati** aggiungere un'origine OLE DB all'attività Flusso di dati e quindi aprire **Editor origine OLE DB.**  
  
3.  Nella pagina **Gestione connessione** dell'editor configurare l'origine con le impostazioni seguenti:  
  
    1.  Per **Gestione connessione OLE DB**selezionare la gestione connessione OLE DB creata in precedenza.  
  
    2.  Per **Modalità di accesso ai dati**selezionare **Comando SQL**.  
  
    3.  Per **Testo comando SQL**immettere la query seguente:  
  
        ```sql 
        SELECT     Person.Contact.EmailAddress, Person.Contact.FirstName, CONVERT(float, Sales.SalesPerson.Bonus) AS Bonus  
        FROM         Sales.SalesPerson INNER JOIN  
                              Person.Contact ON Sales.SalesPerson.SalesPersonID = Person.Contact.ContactID  
        ```  
  
        > [!NOTE]  
        >  È necessario convertire il valore **currency** nella colonna Bonus in **float** prima che sia possibile caricare tale valore in una variabile del pacchetto il cui tipo è **Double**.  
  
4.  Nella scheda **Flusso di dati** aggiungere una destinazione recordset e connetterla dopo l'origine OLE DB.  
  
5.  Aprire l' **editor destinazione recordset**e configurare la destinazione con le impostazioni seguenti:  
  
    1.  Nella scheda **Proprietà componente** selezionare **User::BonusRecordset** per la proprietà **VariableName**.  
  
    2.  Nella scheda **Colonne di input** selezionare tutte e tre le colonne disponibili.  
  
#### <a name="to-configure-the-foreach-loop-container-and-run-the-package"></a>Per configurare il contenitore Ciclo Foreach ed eseguire il pacchetto  
  
1.  Nella scheda **Flusso di controllo** di Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] aggiungere un contenitore Ciclo Foreach e connetterlo dopo l'attività Flusso di dati.  
  
2.  Aprire **Editor ciclo Foreach**e configurare il contenitore con le impostazioni seguenti:  
  
    1.  Nella pagina **Raccolta** selezionare **Enumeratore Foreach ADO**per **Enumeratore**e **User::BonusRecordset**per **Variabile di origine oggetto ADO**.  
  
    2.  Nella pagina **Mapping variabili** eseguire il mapping di **User::EmailAddress** all'indice 0, di **User::FirstName** all'indice 1 e di **User::Bonus** all'indice 2.  
  
3.  Nella scheda **Flusso di controllo** aggiungere un'attività Invia messaggi nel contenitore Ciclo Foreach.  
  
4.  Aprire **Editor attività Invia messaggi**e quindi nella pagina **Messaggio** configurare l'attività con le impostazioni seguenti:  
  
    1.  Per **SmtpConnection**selezionare la gestione connessione SMTP configurata in precedenza.  
  
    2.  Per **Da**immettere un indirizzo di posta elettronica appropriato.  
  
         Se si utilizza il proprio indirizzo di posta elettronica, sarà possibile verificare la corretta esecuzione del pacchetto. Si riceveranno notifiche di messaggi non recapitati per i messaggi inviati dall'attività Invia messaggi ai venditori fittizi di [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
    3.  Per **A**immettere un indirizzo di posta elettronica predefinito.  
  
         Questo valore non verrà utilizzato ma in fase di esecuzione verrà sostituito con l'indirizzo di posta elettronica di ogni venditore.  
  
    4.  Per **Oggetto**immettere "Your annual bonus".  
  
    5.  Per **MessageSourceType**selezionare **Input diretto**.  
  
5.  Nella pagina **Espressioni** di **Editor attività Invia messaggi**fare clic sul pulsante con i puntini di sospensione ( **...** ) per aprire **Editor espressioni di proprietà**.  
  
6.  In **Editor espressioni di proprietà**immettere le informazioni seguenti:  
  
    1.  Per **ToLine**aggiungere l'espressione seguente:  
  
        ```  
        @[User::EmailAddress]  
        ```  
  
    2.  Per la proprietà **MessageSource** aggiungere l'espressione seguente:  
  
        ```  
        "Dear " +  @[User::FirstName] + ": The amount of your bonus for this year is $" +  (DT_WSTR, 12) @[User::Bonus] + ". Thank you!"  
        ```  
  
7.  Eseguire il pacchetto.  
  
     Se è stato specificato un server SMTP valido ed è stato fornito il proprio indirizzo di posta elettronica, si riceveranno notifiche di messaggi non recapitati per i messaggi inviati dall'attività Invia messaggi ai venditori fittizi di [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
  
