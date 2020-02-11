---
title: 'Attività 4: mana e visualizzazione dei risultati | Microsoft Docs'
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: ecc3ba7e-fecf-478f-8825-6e4764b00e99
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 8b97b0129a7cc4ffa21b4a82ad0208a2c1890b27
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "72313651"
---
# <a name="task-4-manaing-and-viewing-results"></a>Attività 4: Gestione e visualizzazione dei risultati
  In questa attività si controllano i risultati della pulizia computerizzata; inoltre, si effettua la pulizia interattiva dei dati del fornitore. Per ulteriori informazioni, vedere [fase di pulizia interattiva](https://msdn.microsoft.com/library/hh213061.aspx#Interactive) .  
  
1.  Selezionare **Contact email** Domain dall'elenco di domini.  
  
2.  Passare alla scheda **non valida** nel riquadro di destra. Si noti che alla fine sono presenti due indirizzi di posta elettronica mancanti. Questi due messaggi di posta elettronica che non sono stati trovati come validi dalla regola di dominio che richiede che tutti gli indirizzi di posta elettronica terminino con ** \@Adventure-Works.com** (con ' s'). In DQS viene applicata la regola di dominio durante la pulizia per stabilire la validità di un indirizzo di posta elettronica. In questa scheda vengono visualizzati i valori del dominio contrassegnati come non validi nella Knowledge Base o che non hanno superato una regola di dominio. In questo caso, i valori in questione non hanno superato la regola di dominio (Email Validation).  
  
3.  Nella colonna **Correggi** in digitare l'indirizzo di posta elettronica corretto che termina con ** \@Adventure-Works.com** (con ' s').  
  
     ![Correzioni della regola di convalida posta elettronica](../../2014/tutorials/media/et-managingandviewingresults-01.jpg "Correzioni della regola di convalida posta elettronica")  
  
4.  Fare clic su **approva** per entrambi i record per approvare entrambe le modifiche. Quando si approva, i record vengono spostati nella scheda con **correzione** . Anziché approvare separatamente ogni elemento, è possibile approvare tutte le modifiche contemporaneamente usando il pulsante della barra degli strumenti **approva tutti i termini** .  
  
5.  Passare alla scheda **nuovo** nel riquadro destro. I valori in questa scheda sono quelli per i quali DQS non dispone ancora di informazioni sufficienti nella Knowledge Base per stabilire se sono corretti. Pertanto, non è possibile apportare o suggerire modifiche ai valori di dominio.  
  
6.  Esaminare i valori per confermare che tutti i messaggi di posta elettronica terminano con ** \@Adventure-Works.com** e fare clic su **approva tutti i termini** sulla barra degli strumenti. I valori approvati da questa scheda passano alla scheda **corretta** .  
  
7.  Selezionare il dominio **Country** dall'elenco dei domini.  
  
8.  Passare alla scheda con **correzione** nel riquadro destro e notare che il valore **United State** viene corretto automaticamente in **Stati Uniti** con ' s'alla fine. Questa regola non è una regola definita per il dominio **Country** , ma DQS è il **83%** sicuro che il valore corretto sia **Stati Uniti**. Il pulsante **approva** viene selezionato automaticamente per tutti gli elementi **corretti** . È possibile eseguire l'override di questo comportamento e rifiutare una modifica.  
  
9. Si noti che **USA** viene corretto **Stati Uniti** perché si tratta di sinonimi e **Stati Uniti** è il valore principale (preferito).  
  
     ![Correzioni basate su sinonimi](../../2014/tutorials/media/et-managingandviewingresults-02.jpg "Correzioni basate su sinonimi")  
  
10. Si noti che il pulsante **approva** è già selezionato per questi valori corretti. Si tratta del comportamento predefinito per i valori con correzione. È possibile rifiutare una modifica e, quando si esegue questa operazione, il valore viene spostato nella scheda **non valido** .  
  
11. Selezionare **Supplier Name** nell'elenco di domini.  
  
12. Passare alla scheda con **correzione** nel riquadro destro.  
  
     ![Nomi fornitori con correzione](../../2014/tutorials/media/et-managingandviewingresults-03.jpg "Nomi fornitori con correzione")  
  
    1.  Si noti che a **. Datum Corp.** è stato corretto in a **. Datum Corporation** e il **motivo** è impostato **sulla relazione basata su termini. A. Datum Corporation** è un valore di dominio noto di DQS perché è stato individuato durante il processo di individuazione delle informazioni. Pertanto, DQS è **sicuro del 100%** sulla correzione.  
  
    2.  Si noti **che Lazy Country Storex è stato** corretto in **Lazy Country Store**, il **livello di confidenza** è impostato su **100%** e il **motivo** è impostato sul **valore di dominio**. Durante il processo di individuazione delle informazioni, impostare **Lazy Country Storex** come errore con **Lazy Country Store** come **correzione**, in modo che DQS sia il **100% di sicurezza** per l'esecuzione di questa correzione.  
  
    3.  DQS non ha familiarità con gli altri valori nell'elenco, ma ha trovato le correzioni per questi valori usando il **controllo ortografico** e propone le correzioni appropriate. DQS non è sicuro del **100%** su queste correzioni, ma il livello di confidenza è superiore al 80%, che rappresenta il livello di soglia per l'esecuzione di correzioni, quindi DQS propone le correzioni.  
  
13. Si noti che l' **approvazione** viene abilitata automaticamente per tutti i valori. È possibile sostituire il valore con correzione o rifiutare la modifica in base alle esigenze. Per impostazione predefinita, il pulsante **approva** è selezionato per tutti i valori nella scheda con **correzione** .  
  
14. Passare alla **nuova** scheda.  
  
15. Si noti che **Corp.** è stato corretto in **Corporation**, **Co.** è stato corretto in **società**e **Inc.** è stato corretto in **incorporato**. Ad esempio, **consolidate Inc.** viene corretta per il consolidamento di consolidate **Incorporated** e **Consolidated Co.** viene corretto in **società consolidata**e **Frabrikam Corp.** viene corretto in **Fabrikam Corporation**.  È possibile osservare che la **relazione basata su termini** è indicata come motivo. Queste modifiche vengono proposte tramite le relazioni basate su termini definite durante l'attività di gestione del dominio. È possibile modificare manualmente i valori **corretti in** qui.  
  
16. Scorrere l'elenco per visualizzare **Hunxgry Coyote Store** con una linea rossa ondulata. Fare clic con il pulsante destro del mouse su di esso e scegliere **archivio Coyote** bloccati (senza ' x '). La colonna **Correggi in** deve essere popolata automaticamente con l' **archivio Coyote affamato**. Inoltre, è possibile digitare manualmente un valore nella colonna Correggi in.  
  
17. Fare clic su **approva tutti i termini** dalla barra degli strumenti. I valori di dominio con il valore **corretto a** specificato passano alla scheda con **correzione** e i nuovi valori senza i valori **corretti** associati passano alla scheda **corretta** .  
  
18. Selezionare il dominio composito **Address Validation** dall'elenco di domini.  
  
19. Nel riquadro destro passare alla scheda **corretta** . Verranno visualizzati gli indirizzi che risultano corretti dal servizio **Melissa Data-Address Check** DQS in **Azure Marketplace**.  
  
20. Passare alla scheda con **correzione** .  
  
21. Si noti che lo **stato** del record con **City** As **Los Angeles** è impostato su **CA** Now. Si noti che il campo **reason** è **corretto dalla regola ' City-State Rule '**.  
  
     ![Correzione regola Città-Provincia](../../2014/tutorials/media/et-managingandviewingresults-04.jpg "Correzione regola Città-Provincia")  
  
22. Si noti che il pulsante di opzione **approva** è già selezionato per questo elemento nell'elenco. Questo è il comportamento predefinito per gli elementi nella scheda con **correzione** .  
  
23. Passare alla scheda **suggerita** . rivedere le modifiche suggerite dal servizio **Melissa Data-Address Check** .  
  
24. **Fare clic su approva tutti i termini** sul pulsante della barra degli strumenti e fare clic su **OK** nella finestra di messaggio di **conferma** .  
  
     ![Pulsante della barra degli strumenti Approva tutti i termini](../../2014/tutorials/media/et-managingandviewingresults-05.jpg "Pulsante della barra degli strumenti Approva tutti i termini")  
  
25. Fare clic su **Avanti** per passare alla pagina **Esporta** .  
  
## <a name="next-step"></a>passaggio successivo  
 [Attività 5: Esportazione dei risultati della pulizia in un file di Excel](../../2014/tutorials/task-5-exporting-cleansing-results-to-an-excel-file.md)  
  
  
