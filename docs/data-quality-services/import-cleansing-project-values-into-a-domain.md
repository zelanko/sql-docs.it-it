---
title: Importare i valori di un progetto di pulizia in un dominio | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql13.dqs.kb.importprojectvalues.f1
ms.assetid: f23e38e2-39e0-42d7-abd5-34d8fcca5d2a
author: lrtoyou1223
ms.author: lle
manager: jroth
ms.openlocfilehash: 080353df8c140349e60247c3e18b0430601a2972
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66776516"
---
# <a name="import-cleansing-project-values-into-a-domain"></a>Importazione dei valori di un progetto di pulizia in un dominio

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  In [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS), è possibile importare informazioni sulla qualità dei dati raccolta durante il processo di pulizia in un processo di pulizia Data Quality o in un pacchetto di Integration Services contenente il componente di pulizia di DQS in un dominio. Ciò garantisce che le informazioni attendibili non vadano perse e che la Knowledge Base venga continuamente migliorata.  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Prerequisites"></a> Prerequisiti  
  
-   Per importare valori di un progetto di pulizia in un dominio, il dominio deve essere stato utilizzato nel progetto di pulizia in Client Data Quality o nel pacchetto di Integration Services contenente un componente di pulizia di DQS.  
  
-   Il progetto di pulizia in Client Data Quality o nel pacchetto di Integration Services contenente il componente di pulizia di DQS deve essere stato completato correttamente.  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Autorizzazioni  
 Per importare in un dominio informazioni sulla qualità dei dati raccolta durante il processo di pulizia, è necessario disporre del ruolo dqs_kb_editor o dqs_administrator nel database DQS_MAIN.  
  
##  <a name="Import"></a> Importazione dei valori di un progetto di pulizia  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Eseguire l'applicazione Data Quality Client](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Nella schermata iniziale del [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] aprire una Knowledge Base nell'attività Gestione dominio.  
  
3.  In caso di aggiunta di valori a un dominio esistente, selezionare il dominio nell'elenco di domini.  
  
4.  Fare clic sulla scheda **Valori di dominio** , fare clic sull'icona **Importa valori** nella barra delle icone, quindi fare clic su **Importa valori progetto**. Viene visualizzata la finestra di dialogo **Importa valori progetto** con un elenco di progetti Data Quality e pacchetti di Integration Services che sono stati puliti utilizzando il dominio.  
  
    > [!NOTE]  
    >  Se non è stato creato alcun progetto utilizzando il dominio o uno dei domini collegati, oppure se il progetto non è stato completato, l'opzione **Importa valori progetto** non sarà disponibile.  
  
5.  Nella finestra di dialogo **Importa valori progetto** :  
  
    -   Selezionare **Tutto** nell'elenco a discesa **Importato** per visualizzare tutti i progetti o **No** per mostrare solo progetti i cui valori non sono stati importati.  
  
    -   Selezionare il progetto da cui si desidera importare i valori.  
  
    -   Selezionare **Aggiungere i valori dalla scheda Nuova** per importare valori nella nuova scheda, oltre a valori nelle schede **Corretti** e **Con correzione** .  
  
    -   Fare clic su **OK**.  
  
6.  Si torna nella scheda **Valori di dominio** e viene visualizzato un messaggio sulla corretta importazione dei valori. I valori importati, e quindi nuovi per il dominio, verranno visualizzati nella tabella **Valori** .  
  
7.  Deselezionare **Mostra solo nuovi** per visualizzare tutti i valori presenti nel dominio.  
  
8.  Selezionare **Corretti**, **Errori**o **Non validi** per visualizzare solo i valori del tipo selezionato.  
  
9. Per cercare una stringa specifica, immettere la stringa nella casella di testo **Trova** . Fare clic sulla freccia Su o Giù per spostarsi tra i valori che soddisfano il criterio di ricerca. Questi verranno evidenziati in giallo.  
  
10. Scegliere **Fine**.  
  
    > [!NOTE]  
    >  Per ulteriori informazioni sull'utilizzo di valori nella scheda **Valori di dominio** , vedere [Change Domain Values](../data-quality-services/change-domain-values.md).  
  
##  <a name="FollowUp"></a> Completamento: dopo l'importazione dei valori di progetto in un dominio  
 Dopo avere importato le informazioni sulla qualità dei dati raccolta durante il processo di pulizia in un dominio, è possibile eseguire attività di gestione relative ai domini sul dominio e sui relativi valori. Per altre informazioni, vedere [Gestione di un dominio](../data-quality-services/managing-a-domain.md).  
  
##  <a name="Values"></a> Valori che verranno importati  
 I valori seguenti verranno importati da un progetto in un dominio:  
  
-   Solo i valori stringa vengono importati nel dominio.  
  
-   Verranno importato solo i valori delle schede **Corretti**, **Con correzione**e **Nuovi** nella pagina **Gestisci e visualizza risultati** dell'attività **Pulizia** . I valori della scheda **Nuovi** verranno importati solo se è stata selezionata la casella di controllo **Aggiungere i valori dalla scheda Nuova** nella finestra di dialogo **Importa valori progetto** .  
  
-   I valori verranno importati come corretti o come errore con relativa correzione. Verranno importati solo valori di errore con relativo valore di correzione.  
  
-   Il valore della correzione sarà un nuovo valore che non esiste nella Knowledge Base o un valore corretto esistente.  
  
-   Solo correzioni eseguite a livello di valore, e non a livello di record, verranno importate nella Knowledge Base.  
  
-   Se il valore importato è in contrasto con una regola di dominio, verranno creati valori non validi.  
  
-   Se si importano valori da diversi progetti in una sola operazione, i valori vengono importati secondo un ordine sequenziale.  
  
-   Una correzione effettuata come risultato di una relazione basata su termine in un dominio, viene importata come valore corretto (non come errore).  
  
##  <a name="ValuesNot"></a> Valori che non verranno importati  
 I valori seguenti non verranno importati da un progetto in un dominio:  
  
-   I valori dalle schede **Suggeriti** e **Non validi** nella pagina **Gestisci e visualizza risultati** dell'attività **Pulizia** non vengono importati.  
  
-   Se un valore trovato nel progetto di pulizia è in contrasto con un valore esistente nel dominio, il valore trovato nel progetto verrà ignorato. Questo include conflitti tra valori di pulizia e valori della Knowledge Base.  
  
-   Le correzioni eseguite a livello di record non verranno importate nella Knowledge Base.  
  
-   Non verrà importato alcun valore in un dominio se il valore che sostituirebbe è corretto o è stato approvato come corretto da un servizio dati di riferimento.  
  
-   Se un valore di correzione compare nella Knowledge Base come valore erroneo o non valido, non verranno importati né l'errore né il valore di correzione.  
  
-   Se il dominio fa parte di un dominio composito, e la pulizia è stata eseguita sul dominio composito, non verrà importato alcun valore.  
  
-   È possibile importare valori da un progetto solo quando la Knowledge Base presenta uno stato operativo ed è bloccata dall'utente che sta effettuando l'importazione.  
  
## <a name="see-also"></a>Vedere anche  
 [Pulizia dei dati](../data-quality-services/data-cleansing.md)   
 [Trasformazione DQS Cleansing](../integration-services/data-flow/transformations/dqs-cleansing-transformation.md)  
  
  
