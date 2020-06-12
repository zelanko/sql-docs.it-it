---
title: Outlier (SQL Server componenti aggiuntivi Data mining) | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- exceptions [data mining]
- data preparation
- outliers [data mining]
- data cleaning
ms.assetid: e6fa7c62-4005-4792-9211-3b699377a517
author: minewiskan
ms.author: owend
ms.openlocfilehash: ecc7cba81a394664b2bdb6a60b6c5f8110760f44
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/09/2020
ms.locfileid: "84547278"
---
# <a name="outliers-sql-server-data-mining-add-ins"></a>Outlier (componenti aggiuntivi Data mining di SQL Server)
  ![Procedura guidata Rimozione outlier sulla barra multifunzione Data mining](media/dmc-outliers.gif "Procedura guidata Rimozione outlier sulla barra multifunzione Data mining")  
  
 Un *outlier* indica un valore di dati problematico per uno dei motivi seguenti:  
  
-   Il valore non rientra nell'intervallo previsto.  
  
-   I dati potrebbero essere stati immessi in modo non corretto.  
  
-   Il valore non è presente.  
  
-   I dati sono costituiti da uno spazio o da un'altra stringa Null.  
  
-   Il valore è accurato, ma è talmente al di fuori della distribuzione che può influire in modo significativo sul modello.  
  
 Il client di data mining per Excel consente di rilevare questi dati, quindi di aggiornare i valori o di eliminarli. È possibile, ad esempio, sostituire gli outlier con una media aritmetica o eliminare le righe che contengono valori potenzialmente errati.  
  
## <a name="handling-outliers"></a>Gestione degli outlier  
 La procedura guidata **Rimuovi outlier** offre diversi strumenti per gestire in modo appropriato gli outlier:  
  
-   È innanzitutto possibile esplorare i dati per comprendere meglio la distribuzione dei valori e la relazione degli outlier con gli altri dati.  
  
     È ad esempio possibile utilizzare l'attività **Esplora dati** per rivedere e correggere i valori. Nella procedura guidata **Rimuovi outlier** viene inoltre visualizzato un grafico, una linea o un grafico a barre, per facilitare la comprensione della distribuzione di tutti i valori.  
  
-   Successivamente, è possibile utilizzare la procedura guidata **outlier** per rimuovere o modificare gli outlier. Il metodo utilizzato varia a seconda che i valori siano discreti o continui.  
  
     I valori discreti vengono visualizzati dalla procedura guidata su un grafico a barre, dove ogni barra rappresenta un valore specifico e l'altezza della barra indica il numero di case per ogni valore. Trascinando il controllo del valore di soglia sul grafico, è possibile escludere le barre che rappresentano gruppi di valori estremi o potenzialmente errati.  
  
-   I valori continui vengono visualizzati dalla procedura guidata su un grafico a barre o a linee. Sul grafico a linee, il valore è rappresentato sull'asse X e il numero dei valori sull'asse Y.  
  
     È possibile controllare se rimuovere o impostare i valori alle estremità inferiore e superiore del grafico modificando i valori **minimo** e **massimo** oppure facendo scorrere le barre. Quando si modificano le impostazioni dei valori minimo e massimo, i dati che verranno eliminati vengono illustrati sul grafico con un'ombreggiatura.  
  
 Dopo aver selezionato gli outlier da utilizzare, è possibile indicare come questi devono essere gestiti dalla procedura guidata. È possibile eliminare le righe contenenti i valori outlier oppure specificare un valore di sostituzione, ad esempio una media, un valore Null o un altro valore desiderato.  
  
 Nella procedura guidata sono infine disponibili alcune opzioni per la visualizzazione dei nuovi dati. È possibile sostituire i dati originali con i nuovi valori, aggiungere una nuova colonna alla tabella contenente i nuovi valori o creare un nuovo foglio di lavoro contenente i dati aggiornati.  
  
### <a name="using-the-outlier-wizard"></a>Utilizzo della procedura guidata relativa agli outlier  
  
1.  Sulla barra multifunzione **data mining** fare clic su **Pulisci dati**e selezionare **outlier**.  
  
2.  Nella finestra di dialogo **selezione dati di origine** selezionare una tabella dati di Excel o un intervallo di celle, quindi fare clic su **Avanti**.  
  
    > [!WARNING]  
    >  Non è possibile utilizzare la procedura guidata **outlier** per i dati esterni, a meno che non venga prima copiata in Excel.  
  
3.  Nella finestra di dialogo **Seleziona colonna** selezionare una **singola** colonna.  
  
     Fare clic su **Avanti**.  
  
4.  Nella finestra di dialogo **Imposta valori di soglia** esaminare la distribuzione dei dati.  
  
    -   Se la colonna contiene valori discreti, verrà visualizzato un istogramma contenente il conteggio per ogni valore discreto.  
  
         Supponendo che gli outlier siano valori rari, è possibile filtrarli modificando il valore **minimo** .  
  
    -   Se la colonna contiene dati numerici, è possibile fare clic sul pulsante **Visualizza come discreto** o sul pulsante **Visualizza come numerico** per passare dalla visualizzazione dei valori in un grafico a barre o da un grafico a linee.  
  
5.  Nella finestra di dialogo **Imposta soglie** scegliere l'intervallo di dati che si desidera memorizzare digitando un valore minimo e massimo oppure trascinando le barre del dispositivo di scorrimento. Fare clic su **Avanti**.  
  
6.  Nella finestra di dialogo **gestione outlier** specificare se si desidera che i valori vengano eliminati o sostituiti e fare clic su **Avanti**.  
  
7.  Nella finestra di dialogo **Seleziona destinazione** specificare il percorso in cui si desidera salvare i nuovi dati.  
  
### <a name="related-options"></a>Opzioni correlate  
 La procedura guidata fornisce le seguenti opzioni:  
  
|**Opzioni**|**Commento**|  
|-----------------|-----------------|  
|**Seleziona colonna**|È possibile utilizzare una sola colonna alla volta.|  
|**Gestione di Impostazione valori di soglia**|Impostare una soglia usando il valore **minimo** per escludere i valori presenti in un minor numero di righe rispetto al valore soglia.<br /><br /> Inizialmente, il valore **minimo** è uguale al valore con il minor numero di righe e non è possibile rendere il valore minimo inferiore a tale valore.|  
|**Gestione outlier**|Se si decide di eliminare gli outlier, è possibile modificare i dati nel foglio di lavoro corrente oppure creare una copia dei dati in un nuovo foglio di lavoro.|  
  
## <a name="see-also"></a>Vedere anche  
 [Esplorare &#40;dati SQL Server componenti aggiuntivi Data mining&#41;](explore-data-sql-server-data-mining-add-ins.md)  
  
  
