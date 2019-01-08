---
title: 'Attività 4: Impostazione delle regole di dominio | Microsoft Docs'
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.topic: conceptual
ms.assetid: 3a7162ba-cf2f-481f-830d-bb6a02823827
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 6c3b51408258b93f6585b46171793eb885a6d0d3
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2018
ms.locfileid: "53349573"
---
# <a name="task-4-setting-domain-rules"></a>Attività 4: Impostazione delle regole di dominio
  In questa attività viene creata una regola per il **Contact Email** dominio per verificare se l'indirizzo di posta elettronica termina con **@adventure-works.com**. Visualizzare [creazione di una regola di dominio](https://msdn.microsoft.com/library/hh510397.aspx) per altre informazioni sulla pagina.  
  
1.  Fare clic su **Contact Email** nel **elenco di domini**.  
  
2.  Passare al **regole di dominio** scheda nel riquadro di destra.  
  
     ![Aggiungere un nuovo pulsante della barra degli strumenti di regola di dominio](../../2014/tutorials/media/et-settingdomainrules-01.jpg "aggiungere un nuovo pulsante della barra degli strumenti di regola di dominio")  
  
3.  Nel riquadro di destra, fare clic su **aggiungere una nuova regola di dominio** pulsante sulla barra degli strumenti (vedere l'immagine) per aggiungere una regola.  
  
4.  Tipo di **convalida di posta elettronica** per il **il nome della regola** , quindi premere **invio**. Il **Active** casella di controllo deve essere selezionata per impostazione predefinita. Questo controllo consente di disattivare temporaneamente una regola.  
  
5.  Nel **compila una regola** riquadro, fare clic su **freccia giù**e selezionare **valore termina con**.  
  
6.  Tipo di **@adventure-works.com** nella casella di testo e premere **scheda**. È possibile aggiungere più condizioni facendo **aggiungere una nuova condizione alla clausola selezionata** pulsante della barra degli strumenti nel **compila una regola** riquadro.  
  
     ![Regola di convalida di posta elettronica](../../2014/tutorials/media/et-settingdomainrules-02.jpg "regola di convalida di posta elettronica")  
  
7.  Fare clic su **eseguire la regola di dominio selezionato sui dati di test** pulsante sulla barra degli strumenti nel riquadro destro per testare la regola rispetto ai dati di esempio.  
  
     ![Esegui la regola di dominio sul pulsante della barra degli strumenti dati di Test](../../2014/tutorials/media/et-settingdomainrules-03.jpg "Esegui la regola di dominio sul pulsante della barra degli strumenti dati di Test")  
  
8.  Nel **Test regola dominio** finestra di dialogo, fare clic su **aggiunge un nuovo termine di test per la regola di dominio** pulsante sulla barra degli strumenti.  
  
     ![Finestra di dialogo regola di dominio di test](../../2014/tutorials/media/et-settingdomainrules-04.jpg "verifica finestra di dialogo regola di dominio")  
  
9. Tipo di **frank7@adventure-works.com** (un valore valido) nella **Contact Email** colonna.  
  
10. Ripetere i due passaggi precedenti per aggiungere **joe2@adventure-work.com** (un valore non valido senza alcun del ').  
  
11. Fare clic sul pulsante ultima (**testa la regola di dominio su tutti i termini**) sulla barra degli strumenti per testare i dati di input rispetto alla regola.  
  
     ![Testa la regola di dominio su tutti i pulsante sulla barra degli strumenti di termini](../../2014/tutorials/media/et-settingdomainrules-05.jpg "testa la regola di dominio su tutti i termini della barra degli strumenti pulsante")  
  
12. Si noti che la prima voce viene visualizzata come un elemento valido e la seconda come un elemento non valido.  
  
     ![Testare i risultati della regola di dominio](../../2014/tutorials/media/et-settingdomainrules-06.jpg "testare i risultati della regola di dominio")  
  
13. Fare clic su **chiudere** per chiudere la **Test regola dominio** nella finestra di dialogo.  
  
## <a name="next-step"></a>Passaggio successivo  
 [Attività 5: Impostazione basate su termini relazioni](../../2014/tutorials/task-5-setting-term-based-relationships.md)  
  
  
