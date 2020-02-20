---
title: Creare, eliminare o modificare una cartella - Reporting Services | Microsoft Docs
ms.date: 06/26/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
ms.assetid: 70a38879-856c-414b-8479-5f9dead38f15
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 874fb7ba143c8f08a0f25501e1852b4d2b280cb2
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "67492859"
---
# <a name="create-delete-or-modify-a-folder---reporting-services"></a>Creare, eliminare o modificare una cartella - Reporting Services
  È possibile creare cartelle per organizzare e gestire gli elementi pubblicati in un server di report. La creazione di cartelle consente agli utenti di individuare in modo semplice i report desiderati. Per gli utenti con ruolo di gestione del contenuto, le cartelle costituiscono una struttura per l'applicazione di autorizzazioni. È possibile creare assegnazioni di ruolo su cartelle specifiche per limitare l'accesso a report in fase di sviluppo o che non devono essere distribuiti su larga scala.  

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"

## <a name="to-create-a-folder"></a>Per creare una cartella  
  
1.  Avviare [Gestione report &#40;modalità nativa SSRS&#41;](https://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896).  
  
2.  In Gestione report selezionare la cartella Home e fare clic su **Nuova cartella**. In alternativa, per creare una cartella all'interno di una cartella esistente, passare alla cartella nella pagina **Contenuto** e fare clic sulla cartella per aprirla. Fare clic su **Nuova cartella**.  
  
     Verrà visualizzata la pagina **Nuova cartella** .  
  
3.  Digitare il nome della cartella. I nomi di cartella possono includere spazi, ma non caratteri riservati usati per la codifica degli URL: \; \? \: \@ \& \= \+ \, \$ \/ \* \< \> \|. Non è possibile digitare una serie di nomi di cartella per creare più cartelle contemporaneamente.  
  
4.  Se lo si desidera, digitare una descrizione.  
  
5.  Selezionare **Nascondi in visualizzazione Elenco** se non si vuole visualizzare la cartella nella visualizzazione predefinita della pagina **Contenuto** . La cartella sarà visibile agli utenti solo dopo aver fatto clic su **Mostra dettagli** nella pagina **Contenuto** .  
  
6.  Fare clic su **OK**.  
  
## <a name="to-delete-a-folder"></a>Per eliminare una cartella  
  
1.  In Gestione report passare alla pagina **Contenuto** e individuare l'elemento che si vuole modificare.  
  
2.  Posizionare il puntatore del mouse sull'elemento, quindi fare clic sulla freccia a discesa.  
  
3.  Scegliere **Elimina**dal menu a discesa.  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="to-modify-or-delete-a-folder"></a>Per modificare o eliminare una cartella  
  
1.  In Gestione report passare alla pagina **Contenuto** e individuare l'elemento che si vuole modificare.  
  
2.  Posizionare il puntatore del mouse sull'elemento, quindi fare clic sulla freccia a discesa.  
  
3.  Scegliere **Gestisci**dal menu a discesa. Verrà visualizzata la pagina Proprietà generali.  
  
4.  Per modificare il percorso della cartella, fare clic su **Sposta**. Digitare il percorso della cartella di destinazione oppure scegliere la cartella di destinazione nell'albero e quindi fare clic su **OK**.  
  
5.  In alternativa, modificare le proprietà della cartella nei modi seguenti:  
  
    -   Per modificare il testo da visualizzare per la cartella, digitare un nome o una descrizione.  
  
    -   Per visualizzare la cartella nella visualizzazione predefinita nella pagina **Contenuto** , deselezionare **Nascondi in visualizzazione Elenco**.  
  
6.  In alternativa, per rimuovere la cartella e il suo contenuto, fare clic su **Elimina**.  
  
7.  Fare clic su **Applica** per salvare le modifiche.  

::: moniker-end

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
 
## <a name="to-create-a-folder"></a>Per creare una cartella  
  
1. Aprire [il portale Web di un server di report (modalità nativa SSRS)](../../reporting-services/web-portal-ssrs-native-mode.md).  
  
2. Passare alla cartella o alla sottocartella in cui si vuole individuare la nuova cartella. Selezionare la cartella **Home** facendo clic sul pulsante **Sfoglia** sulla barra degli strumenti in alto a sinistra nella pagina per crearla in cima alla gerarchia di cartelle.  
  
3. Fare clic sul pulsante **Nuovo** in alto a destra nella barra degli strumenti del server di report, quindi selezionare **Cartella** dal menu a discesa.  
  
4. Nella finestra di dialogo **Creare una nuova cartella in (nome cartella corrente)** immettere il nome della nuova cartella da creare. I nomi di cartella possono includere spazi, ma non caratteri riservati usati per la codifica degli URL: \; \? \: \@ \& \= \+ \, \$ \/ \* \< \> \|. Non è neppure possibile digitare una serie di nomi di cartella per creare più cartelle contemporaneamente.  
  
5. Selezionare **Crea** per completare l'azione.  
  
## <a name="to-delete-a-folder"></a>Per eliminare una cartella  
  
1. Nel portale Web esplorare la gerarchia di cartelle e individuare la cartella che si vuole eliminare.  
  
2. Fare clic con il pulsante destro del mouse sulla cartella e scegliere **Elimina** dal menu a discesa.  
  
3. Selezionare il pulsante **Elimina** nella finestra di dialogo **Elimina <foldername>** per confermare l'eliminazione.  
  
## <a name="to-modify-a-folders-properties"></a>Per modificare le proprietà di una cartella  
  
1. Nel portale Web esplorare la gerarchia di cartelle e individuare la cartella che si vuole eliminare.  
  
2. Fare clic con il pulsante destro del mouse sulla cartella e scegliere **Elimina** dal menu a discesa.  
  
3. Fare clic sulla scheda **Proprietà**. Viene visualizzata la pagina **Proprietà** per impostazione predefinita.  
  
4. È possibile modificare il nome della cartella nella casella di testo *Nome**.  
  
5. È possibile aggiungere o modificare la descrizione della cartella nella casella di testo *Descrizione**.  
  
6. È possibile nascondere o visualizzare la cartella selezionando o deselezionando la casella di controllo **Nascondi questo elemento**.  
  
7. Selezionare **Applica** per salvare le modifiche alle proprietà.  
  
8. Facoltativamente, è possibile spostare o eliminare la cartella selezionando i pulsanti **Sposta** o **Elimina** nella parte superiore della pagina **Proprietà**. Per altre informazioni, vedere l'articolo [Spostare o eliminare un elemento (portale Web)](../../reporting-services/report-server/move-or-delete-an-item-report-manager.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Creare, eliminare o modificare una cartella (portale Web)](../../reporting-services/report-server/create-delete-or-modify-a-folder-web-portal.md)   
 [Gestione del contenuto del server di report (modalità nativa SSRS)](../../reporting-services/report-server/report-server-content-management-ssrs-native-mode.md)   
 [Ricerca, visualizzazione e gestione dei report &#40;Generatore report e SSRS&#41;](../../reporting-services/report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)    
  
::: moniker-end