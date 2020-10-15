---
title: Aggiungere un report nuovo o esistente a un progetto report | Microsoft Docs
description: Informazioni su come aggiungere un report nuovo o esistente a un progetto report usando la Creazione guidata report in SQL Server Reporting Services.
ms.date: 03/17/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: tools
ms.topic: conceptual
helpviewer_keywords:
- reports [Reporting Services], creating
ms.assetid: 8bc0bb53-ad8a-464d-bb6a-7fea5fa62c5c
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 07d1f6d9f31fa300b2e9e43e80eda9c03111cc6c
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/13/2020
ms.locfileid: "91986507"
---
# <a name="add-a-new-or-existing-report-to-a-report-project-ssrs"></a>Aggiungere un report nuovo o esistente a un progetto report (SSRS)
  Per aggiungere un nuovo report impaginato di [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]in [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] , è possibile usare la Creazione guidata report o aggiungere un nuovo report vuoto al progetto. È anche possibile aggiungere un report esistente. Dopo l'aggiunta di un report, il relativo nome verrà visualizzato nella cartella **Report** nel progetto.  
  
> [!NOTE]  
>  Per visualizzare in anteprima un report con le origini dati esistenti, è necessario disporre delle autorizzazioni per l'origine dati dal client di creazione report. Per altre informazioni, vedere l'articolo relativo a [connessioni dati, origini dati e stringhe di connessione](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md).  
  
 Dopo l'aggiunta di un report, è possibile definire origini dati e set di dati, nonché progettarne il layout. Per iniziare, vedere [Creare un report tabella semplice &#40;esercitazione su SSRS&#41;](../../reporting-services/create-a-basic-table-report-ssrs-tutorial.md) o [Tabelle &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/tables-report-builder-and-ssrs.md).  
  
## <a name="to-add-a-new-report-using-the-report-wizard"></a>Per aggiungere un nuovo report tramite la Creazione guidata report  
  
1.  In Esplora soluzioni fare clic con il pulsante destro del mouse sulla cartella Report, quindi scegliere **Aggiungi nuovo report**. Verrà visualizzata la finestra di dialogo **Creazione guidata report** .  
  
     I passaggi della procedura guidata consentono di creare un'origine dati, creare un set di dati con una query, definire gruppi, specificare un layout e creare il report. I passaggi includono:  
  
    -   **Selezione un'origine dati.** Il primo passaggio della creazione di un report consiste nel definire un'origine dati. Nella Creazione guidata report viene visualizzato un elenco di tutte le origini dei dati condivise disponibili nel progetto report, nonché un'opzione per la creazione di una nuova origine dei dati.  
  
    -   **Progettazione query.** Nel secondo passaggio si progetta la query. È possibile digitare la stringa della query, compilarla tramite Progettazione query o importare una query da un altro report. Per altre informazioni sugli strumenti di progettazione query, vedere [Strumenti di progettazione query in Reporting Services](/previous-versions/sql/).  
  
    -   **Selezione tipo di report.** Nel terzo passaggio si seleziona il tipo di report desiderato. È possibile selezionare un report tabulare o matrice. Un report tabella include un numero fisso di colonne. Un report matrice, o a campi incrociati, include un numero variabile di colonne in base ai risultati della query. In un report mappa i dati analitici vengono visualizzati su uno sfondo geografico.  
  
    -   **Assegnazione di un nome al report.**  Nell'ultimo passaggio della procedura guidata si assegna un nome al report e si verificano i campi che verranno inclusi nel report. Dopo il completamento di tutti i passaggi il report viene creato automaticamente e aggiunto al progetto server di report.  
  
## <a name="to-add-a-new-blank-report"></a>Per aggiungere un report vuoto  
  
1.  Scegliere **Aggiungi nuovo elemento** dal menu **Progetto**.  
  
2.  In **Modelli**fare clic su **Report**.  
  
3.  Scegliere **Aggiungi**.  
  
     Un nuovo report vuoto verrà aggiunto al progetto e visualizzato nell'area di progettazione.  
  
## <a name="to-add-an-existing-report"></a>Per aggiungere un report esistente  
  
1.  Scegliere **Aggiungi** dal menu **Progetto**, quindi  **Elemento esistente**.  
  
2.  Passare al percorso del file con estensione rdl, selezionarlo, quindi fare clic su **Aggiungi**.  
  
     l report verrà aggiunto al progetto nella cartella **Report** . Quando il progetto verrà chiuso e riaperto, i report verranno disposti in ordine alfabetico.  
  
## <a name="see-also"></a>Vedere anche  
 [Esercitazioni su Reporting Services &#40;SSRS&#41;](../../reporting-services/reporting-services-tutorials-ssrs.md)  
 Altre domande? [Visitare il forum su Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)
  
