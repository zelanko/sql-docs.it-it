---
title: Creare un avviso dati nella finestra di progettazione Avviso dati | Microsoft Docs
description: Informazioni su come creare definizioni di avviso dati nella finestra di progettazione Avviso dati, nonché su come modificare gli avvisi e salvare le modifiche al termine dell'operazione.
ms.date: 08/17/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: 8464ab9d-afe1-4490-955f-9f3319bcbf8d
author: maggiesMSFT
ms.author: maggies
monikerRange: '>=sql-server-2016 <=sql-server-2016'
ms.openlocfilehash: 28b62c4f3bc15e00337099fd3f954406e3f04122
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97425496"
---
# <a name="create-a-data-alert-in-data-alert-designer"></a>Creare un avviso dati nella finestra di progettazione Avviso dati

[!INCLUDE[ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../includes/ssrs-appliesto-not-pbirs.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../includes/ssrs-appliesto-sharepoint-2013-2016.md)]

Le definizioni di avviso dati vengono create nella finestra di progettazione Avviso dati. Dopo aver salvato le definizioni di avviso, è possibile riaprirle, modificarle, quindi salvare di nuovo nella finestra di progettazione Avviso dati. Per informazioni sulla modifica delle definizioni di avviso, vedere [Gestire gli avvisi dati in Gestione avvisi dati](../reporting-services/manage-my-data-alerts-in-data-alert-manager.md) e [Modificare un avviso dati nella finestra di progettazione di avvisi](../reporting-services/edit-a-data-alert-in-alert-designer.md).

> [!NOTE]
> L'integrazione di Reporting Services con SharePoint non è più disponibile nelle versioni successive a SQL Server 2016.

## <a name="create-a-data-alert-definition"></a>Creare una definizione di avviso dati
 
1.  Individuare la raccolta di SharePoint in cui è contenuto il report per il quale si desidera creare una definizione di avviso dati.  
  
2.  Fare clic sul report.  
  
     Il report verrà eseguito. Se il report è con parametri, verificare che in esso vengano visualizzati i dati per i quali si desidera ricevere messaggi di avviso. Se non vengono visualizzati i valori o le colonne di interesse per l'utente, potrebbe essere necessario eseguire nuovamente il report, utilizzando valori dei parametri diversi.  
  
    > [!NOTE]  
    >  I valori dei parametri scelti per l'esecuzione del report vengono salvati nella definizione di avviso e verranno utilizzati quando il report viene eseguito di nuovo come passaggio nell'elaborazione della definizione di avviso. Per utilizzare valori dei parametri diversi, è necessario creare una nuova definizione di avviso.  
  
3.  Scegliere **Nuovo avviso dati** dal menu **Azioni**.  
  
     L'immagine seguente illustra il menu **Azioni** .  
  
     ![Aprire Alert Designer dalla raccolta di SharePoint](../reporting-services/media/rs-openalertdesigneriw.gif "Aprire Alert Designer dalla raccolta di SharePoint")  
  
     La finestra di progettazione Avviso dati viene visualizzata, con le prime 100 righe del primo feed di dati generato dal report in una tabella.  
  
    > [!NOTE]  
    >  Se l'opzione **Nuovo avviso dati** non viene visualizzata, il servizio avvisi non è configurato nel sito di SharePoint oppure l'edizione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] non include gli avvisi dati. Per altre informazioni, vedere [Servizio SharePoint di Reporting Services e applicazioni di servizio](../reporting-services/report-server-sharepoint/reporting-services-sharepoint-service-and-service-applications.md).  
    >   
    >  Se l'opzione **Nuovo avviso dati** è visualizzata in grigio, l'origine dati del report è configurata per l'utilizzo di credenziali di sicurezza integrata o per la richiesta di credenziali. Per rendere disponibile l'opzione **Nuovo avviso dati** , è necessario aggiornare l'origine dati per usare credenziali archiviate o nessuna credenziale.  
  
     Il nome del feed di dati viene visualizzato nell'elenco a discesa **Nome dati report** .  
  
4.  Facoltativamente, selezionare un feed di dati diverso nell'elenco a discesa **Nome dati report** .  
  
     Se non viene generato alcun feed di dati dal report, non è possibile creare una definizione di avviso per tale report. Il layout del report determina il contenuto di ogni feed di dati. Per altre informazioni, vedere [Generazione di feed di dati dai report &#40;Generatore report e SSRS&#41;](../reporting-services/report-builder/generating-data-feeds-from-reports-report-builder-and-ssrs.md).  
  
5.  Facoltativamente, nella casella di testo **Nome avviso** aggiornare il nome predefinito per renderlo più significativo.  
  
     Il nome predefinito della definizione di avviso corrisponde al nome del report. Non è necessario che i nomi delle definizioni di avviso siano univoci, ma l'utilizzo di nomi uguali ne renderebbe difficile la distinzione quando si visualizza l'elenco di avvisi in Gestione avvisi dati. È consigliabile utilizzare nomi significativi e univoci per le definizioni di avviso.  
  
6.  Facoltativamente, cambiare l'opzione dei dati predefiniti da **any data in the data feed has** (alcuni dati nel feed di dati hanno) in **no data in the data feed has** (nessun dato del feed di dati ha).  
  
7.  Fare clic su **Aggiungi regola**.  
  
     Verrà visualizzato un elenco delle colonne nel feed di dati.  
  
8.  Nell'elenco selezionare la colonna che si desidera utilizzare nella regola, quindi selezionare un operatore di confronto e immettere il valore soglia.  
  
     A seconda del tipo di dati della colonna selezionata, vengono elencati operatori di confronto differenti. Se la colonna dispone di un tipo di dati relativo alla data, verrà visualizzata un'icona di calendario accanto al valore soglia per la regola. È possibile immettere dati facendo clic su una data nel calendario o digitando la data.  
  
     La finestra di progettazione Avviso Dati fornisce due modalità di confronto: **Modalità immissione valori** e **Modalità selezione campo**. La modalità predefinita è **Modalità immissione valori**. È possibile aggiungere clausole OR solo quando è attiva la **Modalità immissione valori** e si sta usando il confronto di tipo **is** .  
  
9. Per aggiungere una clausola OR, fare clic sulla freccia rivolta verso il basso, quindi su **Modalità immissione valori**.  
  
10. Digitare il valore di confronto.  
  
11. Facoltativamente, fare di nuovo clic sui puntini di sospensione **(...)** .  
  
     I puntini di sospensione **(...)** vengono visualizzati nella riga contenente la prima clausola.  
  
     Una clausola OR viene aggiunta nella parte inferiore e all'interno della regola AND.  
  
12. Facoltativamente, fare clic sulla freccia rivolta verso il basso, selezionare **Modalità selezione campo**, quindi selezionare una colonna nell'elenco.  
  
     Si noterà che i puntini di sospensione **(...)** su cui si fa clic per aggiungere clausole OR non sono più disponibili.  
  
13. Facoltativamente, fare di nuovo clic su **Aggiungi regola** per aggiungere altre regole.  
  
     Le regole vengono combinate tramite l'operatore logico AND.  
  
14. Selezionare un'opzione nell'elenco relativo alla ricorrenza. In base al tipo di ricorrenza, immettere un intervallo.  
  
15. Facoltativamente, fare clic su **Avanzate**.  
  
16. Facoltativamente, modificare la data di inizio del messaggio di avviso digitando una data diversa o aprendo il calendario, quindi facendo clic su una data nel calendario.  
  
     La data di inizio predefinita è la data corrente.  
  
17. Facoltativamente, selezionare la casella di controllo accanto a **Arresta avviso il**, quindi scegliere una data di fine per il messaggio di avviso.  
  
     Per impostazione predefinita, un messaggio di avviso non dispone di alcuna data di fine.  
  
    > [!NOTE]  
    >  L'arresto di un messaggio di avviso non comporta l'eliminazione della definizione di avviso. Dopo avere arrestato un messaggio di avviso, è possibile riavviarlo aggiornando le date di inizio e di fine. Per informazioni sull'eliminazione delle definizioni di avviso, vedere [Gestire gli avvisi dati in Gestione avvisi dati](../reporting-services/manage-my-data-alerts-in-data-alert-manager.md).  
  
18. Facoltativamente, deselezionare la casella di controllo **Invia un messaggio solo se cambiano i risultati degli avvisi** .  
  
     Se si inviano messaggi di avviso frequentemente e non si desidera ricevere informazioni ridondanti, non deselezionare questa casella di controllo.  
  
19. Immettere gli indirizzi di posta elettronica dei destinatari dei messaggi di avviso. Separare gli indirizzi con punti e virgola.  
  
     Se disponibile, l'indirizzo di posta elettronica dell'utente che ha creato la definizione di avviso viene aggiunto alla casella dei **destinatari** .  
  
20. Facoltativamente, nella casella di testo **Oggetto** aggiornare la riga dell'oggetto del messaggio di avviso.  
  
     L'oggetto predefinito è **Avviso dati per \<data alert name>** .  
  
21. Facoltativamente, digitare una descrizione per il messaggio di avviso nella casella di testo **Descrizione** .  
  
22. Fare clic su **Salva**.  

## <a name="see-also"></a>Vedere anche

[Finestra di progettazione Avviso dati](../reporting-services/data-alert-designer.md)   
[Gestione avvisi dati per gli amministratori di avvisi](../reporting-services/data-alert-manager-for-alerting-administrators.md)   
[Avvisi dati di Reporting Services](../reporting-services/reporting-services-data-alerts.md)  

Altre domande? [Visitare il forum su Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)
