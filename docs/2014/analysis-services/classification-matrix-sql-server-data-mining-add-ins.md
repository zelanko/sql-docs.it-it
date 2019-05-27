---
title: Matrice di classificazione (componenti aggiuntivi Data Mining SQL Server dati) | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining models, validating
- classification matrix
- confusion table
- mining models, testing
ms.assetid: d6f620f4-39af-4714-9628-28ce3c361fca
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 78f8581839b6b4bdd761c25a1a207e942ae37f62
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66087965"
---
# <a name="classification-matrix-sql-server-data-mining-add-ins"></a>Matrice di classificazione (componenti aggiuntivi Data mining di SQL Server)
  ![Pulsante matrice di classificazione, barra multifunzione Data Mining](media/dmc-cmatrix.gif "pulsante matrice di classificazione, barra multifunzione Data Mining")  
  
 È possibile utilizzare la matrice di classificazione per valutare l'accuratezza di un modello per la stima. Per generare una matrice di classificazione, è necessario eseguire un set di dati di testing tramite il modello; inoltre mediante lo strumento della matrice di classificazione vengono confrontati i valori effettivi del set di testing con le stime eseguite dal modello. Osservando la matrice, è possibile determinare immediatamente la frequenza con cui il modello è corretto e quella con cui vengono eseguite stime in modo errato.  
  
 In questi componenti aggiuntivi, usare il **matrice di classificazione** guidato per selezionare un modello, specificare i dati di test e quindi generare una matrice di risultati.  
  
## <a name="how-to-read-a-classification-matrix"></a>Modalità di lettura di una matrice di classificazione  
 Si supponga che l'obiettivo consiste nel progettare un programma di fedeltà dei clienti e quindi assegnare i clienti a categorie appropriate, in modo da fornire loro il livello adeguato di incentivi. L'implementazione di tre livelli per il programma di ricompensa: bronzo, argento e oro - e assegnati ai clienti in una fase di valutazione. È stato inoltre progettato un modello tramite cui vengono analizzati i clienti e stimate le categorie corrette. A questo punto si utilizzerà la matrice di classificazione nei dati di prova per determinare l'efficacia del modello relativamente alla stima dell'offerta corretta per tutti i clienti.  
  
 Tramite la tabella della matrice di classificazione viene indicato il numero di clienti che verranno assegnati a ogni categoria in base al modello e il risultato ottenuto verrà confrontato con il numero di clienti effettivamente iscritti a ogni livello di ricompensa.  
  
||Bronzo (valore effettivo)|Oro (valore effettivo)|Argento (valore effettivo)|  
|-|-----------------------|---------------------|-----------------------|  
|Bronzo|**94.45%**|15.18%|1.70%|  
|Oro|2.72%|**84.82%**|0,00%|  
|Argento|1.84%|0,00%|**93.80%**|  
|*Corretti*|*95.45%*|*84.82%*|*98.30%*|  
|*Classificato in modo errato*|*4.55%*|*15.18%*|*1.70%*|  
  
-   In ogni colonna vengono visualizzati i valori effettivi del set di dati di testing.  
  
-   In ogni riga vengono visualizzati i valori stimati.  
  
-   I valori in grassetto, rappresentati in diagonale dall'angolo superiore sinistro all'angolo inferiore destro della matrice, forniscono il quadro di ciò che è appropriato nel modello.  
  
-   Tutti gli altri valori all'esterno della diagonale rappresentano errori. Alcuni sono falsi positivi, vale a dire che con la stima eseguita dal modello il cliente è stato associato al programma oro ma non era corretto.  A seconda del dominio, i falsi positivi possono essere molto costosi.  
  
     Altri sono falsi negativi, vale a dire che con la stima eseguita dal modello il cliente non era interessato anche se è stato associato al programma. Anche in questo caso, a seconda del dominio del problema, il costo dell'opportunità persa potrebbe essere significativo.  
  
## <a name="using-the-classification-matrix-wizard"></a>Utilizzo della procedura guidata Matrice di classificazione  
  
1.  Selezionare il modello di data mining sul quale si desidera basare le stime.  
  
2.  Selezionare un'origine dei nuovi dati di test oppure utilizzare i dati di testing salvati con la struttura.  
  
3.  Selezionare la colonna di cui si desidera valutare l'accuratezza. È possibile selezionare solo una colonna quando si crea una matrice, ma la colonna può disporre di più valori.  
  
     Suggerimento: Può essere difficile interpretare una matrice di classificazione se nella colonna stimabile contiene molte colonne da confrontare.  
  
     Nel **Seleziona colonne da stimare** pagina, è possibile inoltre specificare se si desidera visualizzare il numero di valori errati e corretti o visualizzare una percentuale.  
  
4.  Nella pagina Selezione dati di origine indicare se si utilizzano i dati di test esterni o i dati di test salvati con il modello.  
  
5.  Se si usano dati di test esterni, è necessario eseguire il mapping alle colonne di input il modello i **specificare la relazione** pagina della procedura guidata.  
  
     Se si utilizza il set di dati di test predefinito, il mapping viene eseguito automaticamente.  
  
6.  Fare clic su **fine** per eseguire stime sul modello e generare la matrice di classificazione.  
  
     La procedura guidata crea un report che contiene la matrice di classificazione e altri dettagli sull'analisi. Il report viene salvato come tabella in Excel, con un riepilogo nella parte superiore in cui vengono indicati il numero di case stimati correttamente e il numero di stime errate.  
  
### <a name="requirements"></a>Requisiti  
  
-   Per creare una matrice di classificazione, è necessario avere accesso a un modello di data mining esistente che supporta la misura dell'accuratezza. I modelli di previsione e quelli di associazione non possono essere misurati con questo strumento.  
  
-   Per il modello di misura è necessario stimare un valore che sia discreto o che sia già stato discretizzato.  
  
-   Se si non utilizza l'opzione per salvare un set di testing insieme alla struttura o modello, è necessario ottenere un set di dati di input che è essenzialmente lo stesso numero di colonne, con i corrispondenti tipi di dati, come quelli usati nel modello.  
  
-   Sia il modello di data mining che i nuovi dati utilizzati per il testing devono contenere almeno una colonna stimabile e le colonne devono includere lo stesso tipo di dati.  
  
### <a name="known-issues"></a>Problemi noti  
 In SQL Server 2012 e SQL Server 2014, la possibilità di eseguire il mapping di set di dati di test interno al modello non funziona **matrice di classificazione** dello strumento. Tuttavia, è possibile specificare un set di dati esterno e selezionare il set di training come input per determinare l'errore nel set di dati originale.  
  
## <a name="see-also"></a>Vedere anche  
 [Convalida dei modelli e utilizzo dei modelli per la stima &#40;dati di componenti aggiuntivi Data Mining per Excel&#41;](validating-models-and-using-models-for-prediction-data-mining-add-ins-for-excel.md)   
 [Esplorare i dati &#40;componenti aggiuntivi Data Mining di dati SQL Server&#41;](explore-data-sql-server-data-mining-add-ins.md)   
 [Rileva categorie &#40;strumenti di analisi tabelle per Excel&#41;](detect-categories-table-analysis-tools-for-excel.md)  
  
  
