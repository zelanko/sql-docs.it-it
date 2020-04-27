---
title: Finestra di dialogo Proprietà viewport mappa, allineamento al centro e zoom | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.mapviewport.centerandzoom.f1
- "10506"
ms.assetid: 642a06f5-293f-48e0-97a6-1489dbefa719
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 4a5c71344fe45df4265db72e9fd6dc41ac13bd98
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66108285"
---
# <a name="map-viewport-properties-dialog-box-center-and-zoom"></a>Finestra di dialogo Proprietà viewport mappa, Allineamento al centro e zoom
  Selezionare **Centra e zoom** affinché tramite la finestra di dialogo **Proprietà viewport mappa** venga impostata la vista con allineamento al centro e il fattore di zoom per una mappa. Dopo aver specificato un'origine dati della mappa e i limiti della mappa che si desidera includere nel report, è possibile specificare l'allineamento al centro della vista e il fattore di zoom per controllare ulteriormente la visualizzazione della mappa. Le opzioni variano a seconda del metodo utilizzato per specificare i valori di allineamento al centro e zoom. Fare clic sul pulsante **Espressione** (*fx*) per modificare un'espressione che imposta il valore per l'opzione.  
  
## <a name="options"></a>Opzioni  
 **Imposta un livello di allineamento al centro e zoom della vista**  
 Scegliere questa opzione per specificare valori personalizzati per il livello di allineamento al centro e zoom della vista.  
  
 **Allinea al centro la mappa per mostrare un livello mappa**  
 Scegliere questa opzione per specificare un livello e allineare automaticamente al centro la vista sui dati della mappa. Ad esempio allineare al centro la vista su LineLayer1.  
  
 **Allinea al centro la mappa per mostrare un elemento della mappa incorporato**  
 Scegliere questa opzione per allineare al centro la vista su un elemento della mappa associato a dati specifico. I dati spaziali devono disporre di una relazione con i dati analitici per specificare questa opzione.  
  
 Ad esempio allineare al centro la vista sull'elemento della mappa in cui il nome del campo delle corrispondenze è [Città] e il valore della corrispondenza è "Seattle".  
  
 **Allinea al centro la mappa per mostrare tutti gli elementi associati a dati**  
 Scegliere questa opzione per allineare al centro la vista su tutti gli elementi della mappa del livello. I dati spaziali devono disporre di una relazione con i dati analitici per specificare questa opzione.  
  
 Ad esempio allineare al centro la vista sul livello bolle poligono che visualizza le città. Le dimensioni delle bolle sono correlate alla popolazione. Vengono incluse solo le città con un valore della popolazione corrispondente quando si calcola il centro per il viewport.  
  
 **Opzioni di allineamento al centro e zoom**  
 Selezionare un'opzione per specificare il livello di allineamento al centro e zoom della vista.  
  
 **Centro visualizzazione X (percentuale)**  
 Coordinata orizzontale. Il valore predefinito 50% consente di allineare al centro la vista sul punto medio tra i valori orizzontali minimo e massimo.  
  
 **Centro visualizzazione Y (percentuale)**  
 Coordinata verticale. Il valore predefinito, 50%, allinea al centro la vista sul punto medio tra i valori verticali minimo e massimo.  
  
 **Livello zoom (%)**  
 Fattore di zoom. Il valore predefinito, 100%, indica nessun ingrandimento.  
  
 **Allinea al centro la visualizzazione su questo livello**  
 Specificare il nome del livello.  
  
 **Allinea al centro la visualizzazione sull'elemento della mappa che soddisfa questa condizione**  
 Il campo di sola lettura visualizzato viene utilizzato per far corrispondere i dati della mappa e quelli analitici. Specificare il valore con cui eseguire la corrispondenza. La vista viene allineata automaticamente al centro su questo elemento della mappa. Ad esempio NAME = TEXAS. Per impostazione predefinita, il tipo di dati per la condizione è String e la corrispondenza supporta la distinzione tra lettere maiuscole e minuscole.  
  
 Per eseguire la corrispondenza con un campo che dispone di un tipo di dati diverso, è necessario scrivere un'espressione che restituisce tale tipo di dati. Ad esempio se il campo delle corrispondenze è un codice postale di 5 cifre archiviato come un numero intero, per specificare il codice postale 98053 è necessario utilizzare l'espressione = 98053.  
  
## <a name="see-also"></a>Vedi anche  
 [Mappe &#40;Generatore report e SSRS&#41;](report-design/maps-report-builder-and-ssrs.md)  
  
  
