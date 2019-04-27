---
title: Outlier (componenti aggiuntivi Data Mining SQL Server dati) | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- exceptions [data mining]
- data preparation
- outliers [data mining]
- data cleaning
ms.assetid: e6fa7c62-4005-4792-9211-3b699377a517
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0771c953875e9871c53892bc14a3e2a537060833
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62743623"
---
# <a name="outliers-sql-server-data-mining-add-ins"></a>Outlier (componenti aggiuntivi Data mining di SQL Server)
  ![Procedura guidata rimozione outlier sulla barra multifunzione Data Mining](media/dmc-outliers.gif "procedura guidata rimozione Outlier sulla barra multifunzione Data Mining")  
  
 Un' *outlier* significa che un valore di data che risulta problematico per uno dei motivi seguenti:  
  
-   Il valore non rientra nell'intervallo previsto.  
  
-   I dati potrebbero essere stati immessi in modo non corretto.  
  
-   Il valore non è presente.  
  
-   I dati sono costituiti da uno spazio o da un'altra stringa Null.  
  
-   Il valore è accurato, ma è talmente al di fuori della distribuzione che può influire in modo significativo sul modello.  
  
 Il client di data mining per Excel consente di rilevare questi dati, quindi di aggiornare i valori o di eliminarli. È possibile, ad esempio, sostituire gli outlier con una media aritmetica o eliminare le righe che contengono valori potenzialmente errati.  
  
## <a name="handling-outliers"></a>Gestione degli outlier  
 Il **rimozione Outlier** guidata offre diversi strumenti per gestire in modo appropriato gli outlier:  
  
-   È innanzitutto possibile esplorare i dati per comprendere meglio la distribuzione dei valori e la relazione degli outlier con gli altri dati.  
  
     Ad esempio, è possibile usare la **Esplora dati** attività per esaminare e correggere i valori. Il **rimozione Outlier** guidata visualizza inoltre un grafico, una linea o un grafico a barre, che consentono di comprendere la distribuzione di tutti i valori.  
  
-   Successivamente, è possibile usare la **Outlier** procedura guidata per rimuovere o modificare gli outlier. Il metodo utilizzato varia a seconda che i valori siano discreti o continui.  
  
     I valori discreti vengono visualizzati dalla procedura guidata su un grafico a barre, dove ogni barra rappresenta un valore specifico e l'altezza della barra indica il numero di case per ogni valore. Trascinando il controllo del valore di soglia sul grafico, è possibile escludere le barre che rappresentano gruppi di valori estremi o potenzialmente errati.  
  
-   I valori continui vengono visualizzati dalla procedura guidata su un grafico a barre o a linee. Sul grafico a linee, il valore è rappresentato sull'asse X e il numero dei valori sull'asse Y.  
  
     È possibile specificare se rimuovere o mantenere i valori alle estremità superiore e inferiore del grafico modificando la **minimo** e **massimo** valori o le barre di scorrimento. Quando si modificano le impostazioni dei valori minimo e massimo, i dati che verranno eliminati vengono illustrati sul grafico con un'ombreggiatura.  
  
 Dopo aver selezionato gli outlier da utilizzare, è possibile indicare come questi devono essere gestiti dalla procedura guidata. È possibile eliminare le righe contenenti i valori outlier oppure specificare un valore di sostituzione, ad esempio una media, un valore Null o un altro valore desiderato.  
  
 Nella procedura guidata sono infine disponibili alcune opzioni per la visualizzazione dei nuovi dati. È possibile sostituire i dati originali con i nuovi valori, aggiungere una nuova colonna alla tabella contenente i nuovi valori o creare un nuovo foglio di lavoro contenente i dati aggiornati.  
  
### <a name="using-the-outlier-wizard"></a>Utilizzo della procedura guidata relativa agli outlier  
  
1.  Nel **Data Mining** sulla barra multifunzione, fare clic su **pulire i dati**e selezionare **Outlier**.  
  
2.  Nel **selezione dati di origine** della finestra di dialogo selezionare una tabella di dati di Excel o un intervallo di celle e fare clic su **successivo**.  
  
    > [!WARNING]  
    >  Non è possibile usare la **Outlier** guidata su dati esterni, a meno che non si copiati in Excel prima di tutto.  
  
3.  Nel **Seleziona colonna** finestra di dialogo, selezionare una **singolo** colonna.  
  
     Scegliere **Avanti**.  
  
4.  Nel **specificare le soglie** dialogo casella, esaminare la distribuzione dei dati.  
  
    -   Se la colonna contiene valori discreti, verrà visualizzato un istogramma contenente il conteggio per ogni valore discreto.  
  
         Supponendo che gli outlier siano valori rari, è possibile filtrarli modificando la **minimo** valore.  
  
    -   Se la colonna contiene dati numerici, è possibile scegliere il **Visualizza come valori discreti** pulsante o il **Visualizza come valori numerici** per alternare la visualizzazione dei valori in un grafico a barre o un grafico a linee.  
  
5.  Nel **specificare le soglie** finestra di dialogo, scegliere l'intervallo di dati da conservare digitando un valore minimo e massimo o trascinando le barre di scorrimento. Scegliere **Avanti**.  
  
6.  Nel **gestione Outlier** finestra di dialogo specificare se si vuole che i valori vengano eliminati o sostituiti e fare clic su **successivo**.  
  
7.  Nel **selezionare la destinazione** finestra di dialogo, specificare in cui si desidera che i nuovi dati da salvare.  
  
### <a name="related-options"></a>Opzioni correlate  
 La procedura guidata fornisce le seguenti opzioni:  
  
|**Opzioni**|**Commento**|  
|-----------------|-----------------|  
|**Seleziona colonna**|È possibile utilizzare una sola colonna alla volta.|  
|**Specificare le soglie di gestione**|Impostare una soglia **minimo** per escludere i valori che si trovano in un minor numero di righe rispetto al valore di soglia.<br /><br /> Inizialmente il valore in **minimo** è uguale al valore con i numero minore di righe e non può essere inferiore a tale valore minimo.|  
|**Gestione outlier**|Se si decide di eliminare gli outlier, è possibile modificare i dati nel foglio di lavoro corrente oppure creare una copia dei dati in un nuovo foglio di lavoro.|  
  
## <a name="see-also"></a>Vedere anche  
 [Esplorare i dati &#40;componenti aggiuntivi Data Mining di dati SQL Server&#41;](explore-data-sql-server-data-mining-add-ins.md)  
  
  
