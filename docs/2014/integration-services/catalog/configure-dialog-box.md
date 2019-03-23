---
title: Finestra di dialogo Configura | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL12.SSIS.SSMS.ISPROJECTPROP.PARAMETERS.F1
- SQL12.SSIS.SSMS.ISPROJECTPROP.REFERENCES.F1
- sql12.dts.designer.configure.f1
ms.assetid: 10183c8d-b1be-420f-972a-96ea97d4f4d8
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 9361e08722ae832c9e671cd8b83caa51bddaf4f4
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2019
ms.locfileid: "58374968"
---
# <a name="configure-dialog-box"></a>Finestra di dialogo Configura
  Utilizzare la finestra di dialogo **Configura** per configurare i parametri, le gestioni connessioni e i riferimenti agli ambienti per pacchetti e progetti.  
  
 **Per saperne di più**  
  
-   [Aprire la finestra di dialogo Configura](#open_dialog)  
  
-   [Impostare le opzioni nella pagina Parametri](#parameter)  
  
-   [Impostare le opzioni nella pagina Riferimenti](#references)  
  
##  <a name="open_dialog"></a> Aprire la finestra di dialogo Configura  
  
1.  In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]connettersi al server [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
     Verrà eseguita la connessione all'istanza del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] in cui è ospitato il database SSISDB.  
  
2.  In Esplora oggetti espandere l'albero per visualizzare il nodo dei **cataloghi di Integration Services** .  
  
3.  Espandere il nodo **SSISDB** .  
  
4.  Espandere la cartella contenente il pacchetto o il progetto che si desidera configurare.  
  
5.  Fare clic con il pulsante destro del mouse sul pacchetto o sul progetto, quindi scegliere **Configura**.  
  
##  <a name="parameter"></a> Impostare le opzioni nella pagina Parametri  
 Utilizzare la pagina **Parametri** per visualizzare i nomi dei parametri e i valori e per modificare i valori.  
  
 Selezionare l'ambito dei parametri visualizzato nelle schede **Parametri** e **Gestioni connessioni** nell'elenco a discesa **Ambito** .  
  
 Di seguito sono riportate le opzioni della scheda **Parametri** .  
  
 **Contenitore**  
 Viene elencato l'oggetto contenente il parametro.  
  
 **Name**  
 Viene elencato il nome del parametro.  
  
 **Valore**  
 Viene elencato il valore del parametro. Fare clic sul pulsante con i puntini di sospensione per modificare il valore nella finestra di dialogo **Imposta valore parametro** .  
  
 Di seguito sono riportate le opzioni della scheda **Gestioni connessioni** . Utilizzare questa scheda per modificare i valori per le proprietà di gestione connessione. I parametri vengono automaticamente generati nel server SSIS per le proprietà.  
  
 **Contenitore**  
 Viene elencato l'oggetto contenente la gestione connessione.  
  
 **Name**  
 Viene elencato il nome della gestione connessione.  
  
 **Nome proprietà**  
 Viene elencato il nome della proprietà della gestione connessione.  
  
 **Valore**  
 Viene elencato il valore assegnato alla proprietà della gestione connessione. Fare clic sul pulsante con i puntini di sospensione per modificare il valore nella finestra di dialogo **Imposta valore parametro** . È possibile immettere un valore letterale, eseguire il mapping di una variabile di ambiente contenente il valore da utilizzare oppure utilizzare il valore predefinito dal pacchetto.  
  
##  <a name="references"></a> Impostare le opzioni nella pagina Riferimenti  
 Utilizzare la pagina **Riferimenti** per aggiungere e rimuovere i riferimenti agli ambienti e accedere alle proprietà dell'ambiente.  
  
 Un ambiente specifica i valori di runtime per i pacchetti contenuti nei progetti distribuiti nel server [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 **Ambiente**  
 Elenca l'ambiente  
  
 **Cartella ambiente**  
 Elenca la cartella in cui è contenuto l'ambiente.  
  
 **Aprire**  
 Fare clic per aprire la finestra di dialogo **Proprietà ambiente** .  
  
 **Aggiungi**  
 Fare clic per aggiungere un riferimento a un ambiente. Nella finestra di dialogo **Sfoglia ambienti** fare clic su un ambiente, quindi fare clic su **OK**.  
  
 È possibile selezionare un ambiente contenuto in qualsiasi cartella del progetto nel nodo **SSISDB** .  
  
 **Rimuovi**  
 Fare clic su un ambiente elencato nell'area **Riferimenti** e quindi fare clic su **Rimuovi**.  
  
  
