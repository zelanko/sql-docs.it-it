---
title: 'Lezione 5: aggiunta di configurazioni del pacchetto per il modello di distribuzione del pacchetto | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 1c10dd54-67cb-4b63-9e4d-aa6ff0452ecb
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 25922725e202bc7b38e2c6141a097df1af119ed2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62767420"
---
# <a name="lesson-5-adding-package-configurations-for-the-package-deployment-model"></a>Lezione 5: Aggiunta di configurazioni del pacchetto per il modello di distribuzione del pacchetto
  Le configurazioni di pacchetto consentono di impostare variabili e proprietà di runtime all'esterno dell'ambiente di sviluppo. Le configurazioni consentono inoltre di sviluppare pacchetti flessibili e semplici da implementare e distribuire. [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] in sono disponibili i tipi di configurazione seguenti:  
  
-   File di configurazione XML  
  
-   Variabile di ambiente  
  
-   Voce del Registro di sistema  
  
-   Variabile pacchetto padre  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]tavolo  
  
 In questa lezione verrà modificato il pacchetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] semplice creato nella [Lesson 4: Adding Error Flow Redirection](lesson-4-add-error-flow-redirection-with-ssis.md) per usare il modello di distribuzione del pacchetto e le configurazioni del pacchetto. È inoltre possibile copiare il pacchetto della lezione 4 completato incluso nell'esercitazione. Configurazione guidata pacchetto consente di creare una configurazione XML che aggiorna la proprietà `Directory` del contenitore Ciclo Foreach tramite una variabile a livello di pacchetto associata alla proprietà Directory. Dopo aver creato il file di configurazione è possibile modificare il valore della variabile all'esterno dell'ambiente di sviluppo e puntare la proprietà modificata a una nuova cartella di dati di esempio. Quando si esegue di nuovo il pacchetto, il file di configurazione popola il valore della variabile e la variabile a sua volta aggiorna la `Directory` proprietà. Di conseguenza, il pacchetto esegue un'iterazione della nuova cartella dei dati anziché della cartella originale specificata a livello di codice nel pacchetto.  
  
> [!IMPORTANT]  
>  Per eseguire questa esercitazione, è necessario il database di esempio **AdventureWorksDW2012** . Per altre informazioni sull'installazione e sulla distribuzione di **AdventureWorksDW2012**, vedere la pagina relativa agli [esempi del prodotto Reporting Services su CodePlex](https://go.microsoft.com/fwlink/?LinkID=526910).  
  
## <a name="lesson-tasks"></a>Argomenti della lezione  
 In questa lezione sono incluse le attività seguenti:  
  
-   [Passaggio 1: Copia del pacchetto della lezione 4](lesson-5-1-copying-the-lesson-4-package.md)  
  
-   [Passaggio 2: Abilitazione e impostazione delle configurazioni dei pacchetti](lesson-5-2-enabling-and-configuring-package-configurations.md)  
  
-   [Passaggio 3: Modifica del valore di configurazione della proprietà Directory](lesson-5-3-modifying-the-directory-property-configuration-value.md)  
  
-   [Passaggio 4: Test del pacchetto creato nell'esercitazione della lezione 5](lesson-5-4-testing-the-lesson-5-tutorial-package.md)  
  
## <a name="start-the-lesson"></a>Inizio della lezione  
  
-   [Passaggio 1: Copia del pacchetto della lezione 4](lesson-5-1-copying-the-lesson-4-package.md)  
  
  
