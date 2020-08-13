---
title: 'Lesson 3: Defining a Data-Driven Subscription (Lezione 3: Definizione di una sottoscrizione guidata dai dati) | Microsoft Docs'
description: È possibile usare le pagine di sottoscrizione guidate dai dati del portale Web di Reporting Services per connettersi a un'origine dei dati di sottoscrizione e compilare una query che consenta di recuperare i dati di sottoscrizione.
ms.date: 06/06/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: 89197b9b-7502-4fe2-bea3-ed7943eebf3b
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 332a1cbcda7bee87c16167179ef488fe02334474
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/28/2020
ms.locfileid: "87247180"
---
# <a name="lesson-3-defining-a-data-driven-subscription"></a>Lezione 3: Definizione di una sottoscrizione guidata dai dati
In questa lezione dell'esercitazione [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] verranno usate le pagine di sottoscrizione guidata dai dati del portale Web di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] per connettersi a un'origine dati di sottoscrizione, verrà compilata una query che recupera i dati di sottoscrizione e verrà eseguito il mapping tra il set di risultati e le opzioni di recapito e del report.  
  
> [!NOTE]  
> Prima di iniziare, verificare che il servizio **[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent** sia in esecuzione. Se non è in esecuzione, non è possibile salvare la sottoscrizione.  Un metodo per verificarlo consiste nell'aprire [Gestione configurazione SQL Server](../relational-databases/sql-server-configuration-manager.md).
In questa lezione si presuppone che le lezioni 1 e 2 siano state completate e che l'origine dati del report utilizzi credenziali archiviate.  Per altre informazioni, vedere [Lezione 2: Modifica delle proprietà dell'origine dati del report](../reporting-services/lesson-2-modifying-the-report-data-source-properties.md)  
  
## <a name="start-the-data-driven-subscription-wizard"></a><a name="bkmk_startwizard"></a>Avvio di Creazione guidata sottoscrizione guidata dai dati  
  
1.  Nel portale Web di [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] fare clic su **Home**e passare alla cartella contenente il report **Ordini vendita** .  
  
2.  Nel menu di scelta rapida ![ssrs_tutorial_datadriven_reportmenu](../reporting-services/media/ssrs-tutorial-datadriven-reportmenu.png) del report fare clic su **Gestisci**, quindi fare clic su **Sottoscrizioni** nel riquadro a sinistra.  
  
3. Fare clic su **+ Nuova sottoscrizione**. Se il pulsante non è visualizzato, non si dispone delle autorizzazioni di Gestione contenuto.
  
## <a name="define-a-description"></a>Definire una descrizione  
1.  Digitare **Recapito ordine di vendita** nella descrizione.

## <a name="type"></a>Type
1.  Fare clic su **Sottoscrizione guidata dai dati**.  

## <a name="schedule"></a>Pianificazione
1. Nella sezione Pianificazione fare clic su **Pianificazione in base al report**.
2. Fare clic su **Modifica pianificazione**.
3. In **Dettagli pianificazione**fare clic su **Singola occorrenza**.  
4. Specificare un'ora di inizio posticipata di alcuni minuti rispetto all'ora corrente.  
5. Specificare le **date di inizio e di fine**.
6. Selezionare **Applica**.

## <a name="destination"></a>Destination  
1.  Nella sezione Destinazione selezionare **Condivisione file di Windows** per il metodo di recapito.  

## <a name="dataset"></a>Set di dati
1. Fare clic su **Modifica set di dati**.
2. Fare clic su **Origine dei dati personalizzata**.
3. Selezionare **Microsoft SQL Server** come tipo di **connessione** dell'origine dati.
4. In Stringa di connessione digitare la stringa di connessione seguente. *Subscribers* è il database creato nella lezione 1. 
  
    ```  
    data source=localhost; initial catalog=Subscribers
    ```
    
## <a name="credentials"></a>Credenziali
1. Selezionare **Usa le credenziali seguenti**.
2. Selezionare **Nome utente di Windows e password**.
3.  In **Nome utente** e **Password**digitare nome utente e password per il dominio. In **Nome utente**specificare sia il dominio che l'account utente.

> [!NOTE]  
> Le credenziali utilizzate per connettersi a un'origine dati del Sottoscrittore non vengono restituite a [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]. Se in seguito si modifica la sottoscrizione, sarà necessario immettere nuovamente la password utilizzata per la connessione all'origine dei dati.

## <a name="query"></a>Query      
1.  Nella casella della query digitare la query seguente:  
  
    ```
    Select * from OrderInfo  
    ```  
  
2.  Specificare un timeout di 30 secondi.  
  
3.  Fare clic su **Convalida query**e quindi su **Applica**.

## <a name="delivery-options"></a>Opzioni di recapito
Compilare i valori seguenti:

Parametro  |Origine del valore  | Valore/campo  
---------|---------|---------
**Nome file**     |Ottieni il valore dal set di dati | JSON     
**Percorso**     | Immettere il valore  | Per Valore digitare il nome di una condivisione file pubblica per cui si hanno autorizzazioni di scrittura, ad esempio `\\mycomputer\public\myreports`. 
**Formato di rendering** | Ottieni il valore dal set di dati | Format
**Modalità scrittura**| Immettere il valore| Incremento automatico    
**Estensione file** |Immettere il valore |True
**Nome utente** | Immettere il valore | Digitare l'account utente di dominio. Immetterlo nel formato \<domain>\\\<account>. L'account utente deve avere le autorizzazioni richieste per il percorso configurato. 
**Password** | Immettere il valore | Digitare la password
**Usa l'account di condivisione file** | Immettere il valore | False

## <a name="report-parameters"></a>Parametri di report
 1. Nel campo **Numero ordine** selezionare **Ottieni il valore dal set di dati**. In Valore selezionare **Ordine**. 
 2. Selezionare **Crea sottoscrizione**.
   
## <a name="next-steps"></a>Passaggi successivi  
Quando la sottoscrizione viene eseguita, nella condivisione file specificata vengono recapitati quattro file di report, uno per ogni ordine nell'origine dati *Sottoscrittori* . Ogni recapito deve essere univoco in termini di dati (che devono essere specifici dell'ordine), di formato di visualizzazione e di formato di file. È possibile aprire tutti i report dalla cartella condivisa per verificare che ogni versione sia personalizzata in base alle opzioni di sottoscrizione definite.  
  
![Elenco di file creati dalla sottoscrizione](../reporting-services/media/ssrs-tutorial-datadriven-subscription-filelist.gif "Elenco di file creati dalla sottoscrizione")  
  
La pagina di sottoscrizione nel portale Web conterrà la data dell'**Ultima esecuzione** e lo **Stato** della sottoscrizione. 
> [!NOTE]
> Aggiornare la pagina dopo l'esecuzione della sottoscrizione per visualizzare le informazioni aggiornate.  
    
![Risultati della sottoscrizione nel portale Web](../reporting-services/media/ssrs-tutorial-datadriven-subscription-status-reportmanager.png "Risultati della sottoscrizione nel portale Web")  
  
Questo passaggio conclude l'esercitazione relativa alla definizione di una sottoscrizione guidata dai dati.   
  
## <a name="see-also"></a>Vedere anche  
[Sottoscrizioni e recapito &#40;Reporting Services&#41;](../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md)  
[Sottoscrizioni guidate dai dati](../reporting-services/subscriptions/data-driven-subscriptions.md)  
[Creare, modificare ed eliminare le sottoscrizioni guidate dai dati](../reporting-services/subscriptions/create-modify-and-delete-data-driven-subscriptions.md)  
[Utilizzare un'origine dei dati esterna per i dati del Sottoscrittore &#40;sottoscrizione guidata dai dati&#41;](../reporting-services/subscriptions/use-an-external-data-source-for-subscriber-data-data-driven-subscription.md)  
  
