---
title: 'Lezione 8: creare indicatori di prestazioni chiave | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: a6c8ac2b-64ba-456f-b418-7bf0afe145d1
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1d9d3145583670fb849321bac5b57928caacfbc2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66078365"
---
# <a name="lesson-8-create-key-performance-indicators"></a>Lezione 8: Creare indicatori di prestazioni chiave
  In questa lezione verranno creati indicatori di prestazioni chiave (KPI). Gli indicatori KPI vengono usati per misurare le prestazioni di un valore, definito da una misura di *base* , rispetto a un valore di *destinazione* , definito anch ' esso da una misura o da un valore assoluto. Nelle applicazioni client per la creazione di report, gli indicatori KPI possono fornire ai professionisti aziendali un modo rapido e semplice per comprendere i risultati aziendali positivi nel loro complesso o per identificare tendenze significative. Per altre informazioni, vedere [KPI &#40;SSAS tabulare&#41;](tabular-models/kpis-ssas-tabular.md).  
  
 Tempo previsto per il completamento della lezione: **15 minuti**  
  
## <a name="prerequisites"></a>Prerequisites  
 Questo argomento fa parte di un'esercitazione sulla creazione di modelli tabulari, con lezioni che è consigliabile completare nell'ordine indicato. Prima di eseguire le attività in questa lezione è necessario aver completato la lezione precedente: [Lezione 7: Creare misure](lesson-6-create-measures.md).  
  
## <a name="create-key-performance-indicators"></a>Creare indicatori di prestazioni chiave  
  
#### <a name="to-create-an-internet-current-quarter-sales-performance-kpi"></a>Per creare un indicatore KPI relativo alle prestazioni delle vendite Internet trimestrali correnti  
  
1.  In Progettazione modelli fare clic sulla tabella (scheda) **Internet Sales** .  
  
2.  Nella griglia delle misure fare clic su una cella vuota.  
  
3.  Nella barra della formula sopra la tabella digitare la formula seguente:  
  
     `Internet Current Quarter Sales Performance :=IFERROR([Internet Current Quarter Sales]/[Internet Previous Quarter Sales Proportion to QTD],BLANK())`  
  
     Dopo avere completato la compilazione della formula, premere INVIO.  
  
     Questa misura verrà usata come misura di base per l'indicatore KPI.  
  
4.  Nella griglia delle misure fare clic con il pulsante destro del mouse sulla misura **Internet Current Quarter Sales Performance** , quindi scegliere **Crea KPI**.  
  
     Verrà visualizzata la finestra di dialogo **Indicatore di prestazioni chiave** .  
  
5.  Nella finestra di dialogo **Indicatore di prestazioni chiave** selezionare l'opzione **Valore assoluto**in **Definisci valore di destinazione** .  
  
6.  Nel campo **valore assoluto** Digitare `1.1`, quindi premere INVIO.  
  
7.  In **Definisci soglie stato**, nel campo del dispositivo di scorrimento a sinistra ( `1`in basso), digitare e quindi nel campo del dispositivo di scorrimento `1.07`a destra (alto), digitare.  
  
8.  In **Seleziona stile icona** selezionare l'icona a forma di rombo (rossa), di triangolo (gialla) o di cerchio (verde).  
  
    > [!TIP]  
    >  Si noti il campo espandibile **Descrizioni** sotto gli stili di icona disponibili. È possibile digitare le descrizioni per i diversi elementi KPI per semplificarne l'identificazione nelle applicazioni client.  
  
9. Fare clic su **OK** per completare l'indicatore KPI.  
  
     Nella griglia delle misure osservare l'icona accanto alla misura **Internet Current Quarter Sales Performance** . Questa icona indica che la misura funge da valore di base per un indicatore KPI.  
  
#### <a name="to-create-an-internet-current-quarter-margin-performance-kpi"></a>Per creare un indicatore KPI relativo alle prestazioni dei margini Internet trimestrali correnti  
  
1.  Nella griglia delle misure per la tabella **Internet Sales** fare clic su una cella vuota.  
  
2.  Nella barra della formula sopra la tabella digitare la formula seguente:  
  
     `Internet Current Quarter Margin Performance :=IF([Internet Previous Quarter Margin Proportion to QTD]<>0,([Internet Current Quarter Margin]-[Internet Previous Quarter Margin Proportion to QTD])/[Internet Previous Quarter Margin Proportion to QTD],BLANK())`  
  
     Dopo avere completato la compilazione della formula, premere INVIO.  
  
3.  Nella griglia delle misure fare clic con il pulsante destro del mouse sulla misura **Internet Current Quarter Margin Performance** , quindi scegliere **Crea KPI**.  
  
4.  Nella finestra di dialogo **Indicatore di prestazioni chiave** selezionare l'opzione **Valore assoluto**in **Definisci valore di destinazione** .  
  
5.  Nel campo **valore assoluto** Digitare `1.25`.  
  
6.  In **Definisci soglie stato**far scorrere il dispositivo di scorrimento sinistro (in basso) fino a quando non viene visualizzato **0.8**, quindi far scorrere il dispositivo di scorrimento destro (in alto) fino a quando non viene visualizzato **1.03**.  
  
7.  In **Seleziona stile icona** selezionare l'icona a forma di rombo (rossa), di triangolo (gialla) o di cerchio (verde) e quindi fare clic su **OK**.  
  
## <a name="next-step"></a>passaggio successivo  
 Per continuare questa esercitazione, passare alla lezione successiva: [Lezione 9: Creare prospettive](lesson-8-create-perspectives.md).  
  
  
