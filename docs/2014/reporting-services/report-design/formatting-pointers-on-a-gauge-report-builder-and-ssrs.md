---
title: Formattazione degli indicatori di misura su un misuratore (Generatore report e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 2fdf670a-5237-48fe-813d-97657c5c77d2
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 3254f7bbe4cfdd826b24c003b5b472535534dd54
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62654468"
---
# <a name="formatting-pointers-on-a-gauge-report-builder-and-ssrs"></a>Formattazione degli indicatori di misura su un misuratore (Generatore report e SSRS)
  Un indicatore di misura del misuratore indica il valore corrente del misuratore. Per impostazione predefinita, quando si aggiunge un campo, i valori in esso contenuti vengono aggregati in un unico valore indicato dall'indicatore di misura sul misuratore. È possibile aggiungere più indicatori di misura al misuratore in modo da indicare più valori sulla stessa scala o aggiungere più scale e un indicatore di misura per ogni scala aggiunta. Dopo aver aggiunto un campo a un misuratore, è necessario impostare i valori massimo e minimo sulla scala corrispondente in modo da fornire un contesto per il valore dell'indicatore di misura. È inoltre possibile impostare i valori minimo e massimo su un intervallo per mostrare un'area critica sulla scala.  
  
 Per impostare le proprietà relative all'aspetto dell'indicatore di misura, fare clic con il pulsante destro del mouse sull'indicatore di misura e scegliere **Proprietà indicatore di misura radiale** o **Proprietà indicatore di misura lineare**. Ogni indicatore di misura del misuratore contiene lo stesso set di proprietà. Sono disponibili anche proprietà relative all'aspetto corrispondenti, specifiche per ogni tipo di misuratore:  
  
-   Su un misuratore radiale è possibile specificare un indicatore di misura di tipo lancetta e un'estremità della lancetta.  
  
-   Su un misuratore lineare è possibile specificare un indicatore di misura di tipo termometro, ovvero una variazione dell'indicatore di misura a barre. L'indicatore di misura di tipo termometro consente di specificare la forma del bulbo.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="HowPointer"></a> Connessione dell'indicatore di misura ai dati  
 Per impostazione predefinita, quando si aggiunge un misuratore, in quest'ultimo è contenuto un indicatore di misura senza alcun campo associato, noto anche come indicatore di misura vuoto. Questo consente di visualizzare il valore zero finché non si aggiunge un campo al riquadro dei dati. Quando si esegue questa operazione, l'indicatore di misura viene connesso al campo aggiunto. Se si elimina un campo dal riquadro dei dati, viene eliminato anche l'indicatore di misura a esso associato.  
  
 Dopo aver aggiunto i dati, quando si fa clic con il pulsante destro del mouse sull'indicatore di misura, vengono visualizzate le opzioni **Cancella valore indicatore di misura** ed **Elimina indicatore di misura** . L'opzione **Cancella valore indicatore di misura** consente di rimuovere il campo associato al misuratore lasciando comunque visualizzato l'indicatore di misura. L'opzione **Elimina indicatore di misura** consente di rimuovere il campo dal misuratore eliminando anche l'indicatore di misura. Se si riaggiunge un campo al misuratore, verrà nuovamente visualizzato l'indicatore di misura predefinito. Quando si imposta il puntatore **Hidden** proprietà `True`, il puntatore non viene nascosto nell'area di progettazione, ma è nascosta in fase di esecuzione.  
  
  
##  <a name="DisplayingMultiple"></a> Visualizzazione di più indicatori di misura sul misuratore  
 È possibile aggiungere più indicatori di misura al misuratore in modo da indicare più valori sulla stessa scala. Questa operazione può risultare utile se si desidera visualizzare contemporaneamente un valore alto e uno basso. Per specificare più indicatori di misura sul misuratore per la stessa scala, fare clic con il pulsante destro del mouse in un punto qualsiasi all'interno del misuratore e scegliere **Aggiungi indicatore di misura** dal menu di scelta rapida. In alternativa, è possibile aggiungere una scala facendo clic con il pulsante destro del mouse in un punto qualsiasi del misuratore e scegliendo **Aggiungi scala**. È quindi possibile aggiungere un nuovo indicatore di misura che verrà associato automaticamente all'ultima scala.  
  
 Quando gli indicatori di misura si sovrappongono, l'ordine in base al quale vengono disegnati viene determinato dall'ordine in cui vengono aggiunti al misuratore. Non è possibile ridefinire l'ordine di disegno degli indicatori di misura modificando l'ordine dei campi nel riquadro dei dati. Per modificare l'ordine di disegno di più indicatori di misura, aprire il riquadro Proprietà e fare clic su **Indicatori di misura (...)**. Modificare quindi l'ordine degli indicatori di misura nella raccolta Indicatore di misura.  
  
  
##  <a name="SettingGradients"></a> Impostazione delle sfumature sull'estremità di una lancetta  
 È possibile specificare un'estremità della lancetta che può essere disegnato al di sopra o al di sotto dell'indicatore di misura solo su un misuratore radiale. Tutti gli stili dell'estremità della lancetta vengono disegnati con sfumature predefinite che non possono essere modificate. L'unica eccezione è lo stile `RoundedDark` per il quale è possibile specificare un colore e uno stile di sfumatura.  
  
  
##  <a name="SettingSnappingInterval"></a> Impostazione di un intervallo di blocco  
 Un intervallo di blocco definisce il multiplo in base al quale arrotondare i valori. Per impostazione predefinita, il misuratore punterà al valore esatto del campo specificato nel riquadro dei dati. È tuttavia possibile arrotondare il valore esatto per eccesso o per difetto, in modo da bloccare l'indicatore di misura su un intervallo predefinito. Se, ad esempio, il valore sul misuratore è 34,2 e si specifica un intervallo di blocco pari a 5, l'indicatore di misura del misuratore punterà al valore 35. Se invece il valore sul misuratore è 31,2 e si specifica un intervallo di blocco pari a 5, l'indicatore di misura del misuratore punterà al valore 30. Per altre informazioni, vedere [impostare un intervallo di blocco su un misuratore &#40;Generatore Report e SSRS&#41;](../set-a-snapping-interval-on-a-gauge-report-builder-and-ssrs.md).  
  
  
##  <a name="SpecifyingImage"></a> Specifica di un'immagine come indicatore di misura su un misuratore radiale  
 Oltre all'elenco predefinito di stili dell'indicatore di misura, è possibile specificare un'immagine come indicatore di misura. Questa operazione è consigliata quando si utilizza un'immagine per sostituire uno stile dell'indicatore di misura di tipo lancetta esistente. L'immagine viene sovrapposta all'indicatore di misura, ma tutte le funzionalità dell'indicatore di misura risultano ancora disponibili. Le opzioni relative al colore e alla sfumatura non sono applicabili quando si utilizza un'immagine per l'indicatore di misura.  
  
 Se l'immagine dell'indicatore di misura è una forma irregolare, è necessario definire un colore trasparente per nascondere le aree dell'immagine che non devono essere visualizzate sul misuratore. Quando si definisce un colore trasparente, il misuratore traspone l'immagine al di sopra dell'indicatore di misura esistente e la taglia in modo da visualizzare solo la forma dell'indicatore di misura. Ridefinisce inoltre la scala dell'immagine per adattarla alle dimensioni dell'indicatore di misura. Quando si specifica un'immagine per un indicatore di misura, qualsiasi indicatore di misura successivo aggiunto al di sopra del misuratore verrà disegnato sotto l'immagine. Per questo motivo, è consigliabile non specificare un'immagine per l'indicatore di misura se nel misuratore sono presenti più indicatori di misura. Per altre informazioni, vedere [specificare un'immagine come indicatore di misura su un misuratore &#40;Generatore Report e SSRS&#41;](../specify-an-image-as-a-pointer-on-a-gauge-report-builder-and-ssrs.md).  
  
  
## <a name="see-also"></a>Vedere anche  
 [Formattazione di scale su un misuratore &#40;Generatore report e SSRS&#41;](formatting-scales-on-a-gauge-report-builder-and-ssrs.md)   
 [Formattazione di intervalli su un misuratore &#40;Generatore report e SSRS&#41;](formatting-ranges-on-a-gauge-report-builder-and-ssrs.md)   
 [Misuratori &#40;Generatore report e SSRS&#41;](gauges-report-builder-and-ssrs.md)  
  
  
