---
title: Uso di indicatori KPI in Reporting Services | Microsoft Docs
description: Informazioni su come è possibile misurare facilmente lo stato e le prestazioni usando gli indicatori KPI in SQL Server Reporting Services.
author: maggiesMSFT
ms.author: maggies
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.date: 07/02/2017
ms.openlocfilehash: e661fee4e9b5afe5f78cae444ff8d6574a536bb9
ms.sourcegitcommit: 80701484b8f404316d934ad2a85fd773e26ca30c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/03/2020
ms.locfileid: "93243780"
---
# <a name="working-with-kpis-in-reporting-services"></a>Usare gli indicatori KPI in Reporting Services

[!INCLUDE[ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../includes/ssrs-appliesto-pbirs.md)]

Un *indicatore di prestazioni chiave (KPI)* è un'indicazione visiva che comunica il progresso compiuto verso un obiettivo.  Gli indicatori KPI consentono a team, manager e aziende di valutare con rapidità l'avanzamento compiuto verso risultati misurabili.
  
Grazie agli indicatori KPI, SQL Server Reporting Services consente di rispondere con facilità alle domande seguenti:  
  
- A che punto sono rispetto al raggiungimento dell'obiettivo?  
  
- Quanto sono avanti o indietro rispetto al raggiungimento dell'obiettivo?  
  
- Quali sono le quantità minime completate?  

> [!NOTE]
> Gli indicatori KPI sono accessibili solo nelle edizioni Enterprise (Developer) del portale di SSRS.

## <a name="creating-a-dataset"></a>Creazione di un set di dati

Un indicatore KPI usa solo la prima riga di dati di un set di dati condiviso. Verificare che i dati da usare si trovino nella prima riga. Per creare un set di dati condiviso, è possibile usare Generatore report o SQL Server Data Tools.  
  
> **Nota** : non è necessario che il set di dati si trovi nella stessa cartella dell'indicatore KPI.  
  
## <a name="placement-of-kpis"></a>Posizionamento di indicatori KPI  
  
È possibile creare gli indicatori KPI in qualsiasi cartella nel server di report.  Prima di creare un indicatore KPI, è bene considerare quale sia il percorso corretto in cui inserirlo. È possibile collocarlo in una cartella visibile agli utenti e al contempo pertinente anche per altri report e indicatori KPI.  
## <a name="adding-a-kpi"></a>Aggiunta di un indicatore KPI
  
Dopo aver stabilito la posizione dell'indicatore KPI, passare alla cartella e nel menu principale selezionare **Nuovo** > **KPI** .  
  
![Screenshot che mostra l'elenco a discesa Nuovo con l'opzione KPI evidenziata.](../reporting-services/media/rscreatekpi1.png)  
  
Verrà visualizzata la schermata **Nuovo indicatore KPI** .  
  
![Screenshot che mostra la schermata Nuovo indicatore KPI.](../reporting-services/media/rscreatekpi2.png)  
  
È possibile assegnare valori statici o usare i dati di un set di dati condiviso. L'indicatore KPI appena creato verrà popolato con un set casuale di dati da aggiornare manualmente.  
  
| Campo | Descrizione |
|-----------------|--------------------------------------------------------------------------------------------------------------------------------------------------|
| Formato del valore | Consente di modificare il formato del valore visualizzato. |
| valore | Il valore da visualizzare per l'indicatore KPI. |
| Obiettivo | Usato come confronto con un valore numerico e visualizzato come differenza della percentuale. |
| Stato | Valore numerico usato per determinare il colore del riquadro dell'indicatore KPI. Sono valori validi 1 (verde), 0 (ambra) e -1 (rosso). |
| Set di tendenze | Valori numerici delimitati da virgole usati per le visualizzazioni dei grafici. Può essere impostato su una colonna di un set di dati con valori che rappresentano la tendenza. |
| Contenuti correlati | Possibilità di impostare un collegamento drill-through. Questo collegamento può essere un report per dispositivi mobili pubblicato nel portale o un URL personalizzato. |
  
> **Avviso** : sebbene in fase di progettazione sia possibile usare il valore in lettere per il campo **Stato** , per l'aggiornamento del set di dati è necessario usare il valore numerico. Aggiornando il set di dati con il valore letterale invece che numerico, l'indicatore KPI nel server potrebbe essere danneggiato.  
>
> **Nota** : per i campi **Valore** , **Obiettivo** e **Stato** è possono scegliere solo un valore nella prima riga del risultato di un set di dati. Per il campo **Set di tendenze** è invece possibile scegliere la colonna che riflette la tendenza.  
  
Per usare i dati di un nuovo set di dati condiviso, è possibile seguire questa procedura.
  
1. Modificare la casella di riepilogo a discesa da **Imposta manualmente** o **Non impostato** a **Campo del set di dati**.  
  
    ![Screenshot che mostra l'opzione Valore impostata su Campo del set di dati e l'opzione Scegliere un campo del set di dati impostata su Non impostato.](../reporting-services/media/rscreatekpi3.png)  
  
2. Selezionare i **puntini di sospensione (...)** nella casella dei dati. Verrà visualizzata la schermata **Scegliere un set di dati** .  
  
    ![Screenshot della sezione Scegliere un set di dati con l'opzione Finance_KPI selezionata.](../reporting-services/media/rscreatekpi4.png)  
  
3. Selezionare il set di dati contenente i dati da visualizzare.  
  
4. Scegliere il campo da usare. Selezionare **OK**.  
  
    ![Screenshot che mostra la sezione Selezionare un campo da Finance_KPI con l'opzione Sum_Amount selezionata.](../reporting-services/media/rscreatekpi5.png)  
  
5. Modificare il campo **Formato valore** affinché corrisponda al valore desiderato. In questo esempio, il valore è una valuta.  
  
    ![Screenshot dell'anteprima dell'indicatore KPI che mostra l'opzione Formato valore impostata su Valuta.](../reporting-services/media/rscreatekpi6.png)  
  
6. Selezionare **Applica**.  
  
    ![Screenshot degli indicatori KPI che mostrano che il set di dati include due elementi.](../reporting-services/media/rscreatekpi7.png)

## <a name="configuring-related-content"></a>Configurazione del contenuto correlato

Quando si sceglie **Report per dispositivi mobili** , è possibile scegliere la destinazione in una finestra di dialogo.

   ![Screenshot che mostra l'opzione Contenuto correlato impostata su Report per dispositivi mobili e l'opzione Scegliere un report per dispositivi mobili impostata su Non impostato.](media/rscreatekpi-related-content-mobile-report.png)

Quando si fa clic sull'indicatore KPI nel portale, un'anteprima del report per dispositivi mobili viene visualizzata nell'elenco a discesa del contenuto correlato. Facendo clic su questa anteprima è possibile passare direttamente al report.

È anche possibile specificare un URL personalizzato. L'attività può essere un sito Web, un sito di SharePoint, un URL di un report SSRS che consente di passare parametri hardcoded.

![Screenshot che mostra l'opzione Contenuto correlato impostata su URL personalizzato e l'opzione Immettere un URL impostata su http://.](media/rscreatekpi-related-content-custom-url.png)

Quando si fa clic sull'indicatore KPI, l'URL viene visualizzato nel contenuto correlato.

È possibile aggiungere solo un report per dispositivi mobili o un URL personalizzato.
  
## <a name="removing-a-kpi"></a>Rimozione di un indicatore KPI  
  
Per rimuovere un indicatore KPI, è possibile seguire questa procedura.
  
1. Selezionare i **puntini di sospensione (...)** dell'indicatore KPI da rimuovere. Selezionare **Gestisci**.  
  
    ![Screenshot che mostra l'opzione puntini di sospensione per un indicatore KPI selezionata e l'opzione GESTISCI evidenziata.](../reporting-services/media/rsremovekpi1.png)  
  
2. Selezionare **Elimina**. Selezionare di nuovo **Elimina** nella finestra di dialogo di conferma.  
  
    ![Screenshot dell'opzione Elimina.](../reporting-services/media/rsremovekpi2.png)  
  
## <a name="refreshing-a-kpi"></a>Aggiornamento di un indicatore KPI  
  
Per aggiornare l'indicatore KPI, è necessario configurare una memorizzazione nella cache per il set di dati condiviso. Per altre informazioni sui piani di aggiornamento della cache, vedere [Usare i set di dati condivisi (portale Web)](../reporting-services/work-with-shared-datasets-web-portal.md).  
  
## <a name="next-steps"></a>Passaggi successivi
  
[Portale Web](../reporting-services/web-portal-ssrs-native-mode.md)  
[Usare i set di dati condivisi (portale Web)](../reporting-services/work-with-shared-datasets-web-portal.md)

Altre domande? [Visitare il forum su Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)
