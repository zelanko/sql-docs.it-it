---
title: Query di data mining | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.dataminingquery.f1
ms.assetid: 948e358a-6245-429f-82c7-4cedc5e048fd
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 6ab9374312051ab22aa90c48bfed40713fe4e318
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/26/2019
ms.locfileid: "71298313"
---
# <a name="data-mining-query"></a>Query di data mining

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Il riquadro di progettazione contiene il generatore delle query di stima di data mining che consente di compilare le query delle stime di data mining. È possibile progettare query di stima in base a tabelle di input o query di stima singleton. Passare alla visualizzazione dei risultati per eseguire la query e visualizzare i risultati. Nella visualizzazione Query viene visualizzata la query DMX (Data Mining Extensions) creata dal generatore delle query di stima.  
  
## <a name="options"></a>Opzioni  
 Pulsante Cambia visualizzazione  
 Fare clic su un'icona per alternare il riquadro di progettazione al riquadro Query. Per impostazione predefinita è aperto il riquadro di progettazione.  
  
 Per passare al riquadro di progettazione, fare clic sull'icona ![Icona Progettazione](../../integration-services/control-flow/media/ssis-designicon.gif "Icona Progettazione").  
  
 Per passare al riquadro Query, fare clic sull'icona ![Icona SQL](../../integration-services/control-flow/media/ssis-queryicon.gif "Icona SQL").  
  
 **Modello di data mining**  
 Consente di visualizzare il modello di data mining selezionato sul quale si desidera basare le stime.  
  
 **Seleziona modello**  
 Consente di aprire la finestra di dialogo **Seleziona modello di data mining** .  
  
 **Colonne di input**  
 Consente di visualizzare le colonne di input selezionate per la generazione delle stime.  
  
 **Origine**  
 Consente di selezionare l'origine contenente il campo che verrà utilizzato per la colonna nell'elenco a discesa. È possibile usare il modello di data mining selezionato nella tabella **Modello di data mining** , la tabella o le tabelle di input selezionate nella tabella **Seleziona tabella/e di input** , una funzione di stima o un'espressione personalizzata.  
  
 È possibile trascinare le colonne dalle tabelle contenenti il modello di data mining e dalle tabelle di input sulla cella.  
  
 **Campo**  
 Consente di selezionare una colonna nell'elenco di colonne derivato dalla tabella di origine. Se è stata selezionata l'opzione **Funzione di stima** in **Origine**, la cella conterrà un elenco a discesa delle funzioni di stima disponibili per il modello di data mining selezionato.  
  
 **Alias**  
 Il nome della colonna restituito dal server.  
  
 **Visualizza**  
 Selezionare questa opzione per restituire la colonna o per utilizzarla solo nella clausola WHERE.  
  
 **Gruppo**  
 Usare questa opzione con la colonna **And/Or** per raggruppare le espressioni. Ad esempio, (espr1 OR espr2) AND espr3.  
  
 **And/Or**  
 Utilizzare questa opzione per creare una query logica. Ad esempio, (espr1 OR espr2) AND espr3.  
  
 **Criteri/Argomento**  
 Consente di specificare una condizione o un'espressione utente da applicare a una colonna. È possibile trascinare le colonne dalle tabelle contenenti il modello di data mining e dalle tabelle di input sulla cella.  
  
## <a name="see-also"></a>Vedere anche  
 [Strumenti query di data mining](https://docs.microsoft.com/analysis-services/data-mining/data-mining-query-tools)   
 [Guida di riferimento a DMX &#40;Data Mining Extensions&#41;](../../dmx/data-mining-extensions-dmx-statements.md)  
  
  
