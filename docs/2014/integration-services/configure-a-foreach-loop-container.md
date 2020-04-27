---
title: Configurare un contenitore ciclo foreach | Microsoft Docs
ms.custom: ''
ms.date: 08/22/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Foreach Loop containers
- containers [Integration Services], Foreach Loop
ms.assetid: 519c6f96-5e1f-47d2-b96a-d49946948c25
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 461a652999e97907962486cfc05e5b6668f5590d
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66060880"
---
# <a name="configure-a-foreach-loop-container"></a>Configurare un contenitore Ciclo Foreach
  Questa procedura descrive la configurazione di un contenitore Ciclo Foreach, incluse le espressioni di proprietà a livello di enumeratore e contenitore.  
  
### <a name="to-configure-the-foreach-loop-container"></a>Per configurare il contenitore Ciclo Foreach  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]aprire il progetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] che contiene il pacchetto desiderato.  
  
2.  Fare clic sulla scheda **Flusso di controllo** e quindi fare doppio clic su Ciclo Foreach.  
  
3.  Nella finestra di dialogo **Editor ciclo Foreach** fare clic su **Generale** e, facoltativamente, modificare il nome e la descrizione del ciclo Foreach.  
  
4.  Fare clic su **Raccolta** e selezionare un tipo di enumeratore nell'elenco **Enumeratore** .  
  
5.  Specificare un enumeratore e impostarne le opzioni nel modo seguente:  
  
    -   Per usare l'enumeratore Foreach File, specificare la cartella che contiene i file da enumerare, specificare un filtro per il nome e il tipo di file e quindi specificare se deve essere restituito il nome completo del file. Indicare inoltre se ricercare ulteriori file nelle sottocartelle.  
  
    -   Per usare l'enumeratore Foreach Item, fare clic su **Colonne**e, nella finestra di dialogo **Colonne For Each Item** , fare clic su **Aggiungi** per aggiungere le colonne. Selezionare un tipo di dati nell'elenco **Tipo di dati** per ogni colonna e quindi fare clic su **OK**.  
  
         Digitare i valori nelle colonne oppure selezionarli dagli elenchi.  
  
        > [!NOTE]  
        >  Per aggiungere una nuova riga, fare clic in un punto qualsiasi al di fuori della cella in cui si è digitato.  
  
        > [!NOTE]  
        >  Se un valore non è compatibile con il tipo di dati della colonna, il testo viene evidenziato.  
  
    -   Per usare l'enumeratore Foreach ADO, selezionare una variabile esistente oppure fare clic su **Nuova variabile** nell'elenco **Variabile di origine oggetto ADO** per specificare la variabile in cui è contenuto il nome dell'oggetto ADO da enumerare e selezionare l'opzione corrispondente alla modalità di enumerazione.  
  
         Se si crea una nuova variabile, impostarne le proprietà nella finestra di dialogo **Aggiungi variabile** .  
  
    -   Per usare l'enumeratore Foreach ADO.NET set di righe dello schema, selezionare un connettore ADO.NET esistente oppure fare clic su **Nuova connessione** nell'elenco **Connessione** e quindi selezionare uno schema.  
  
         Facoltativamente, fare clic su **Imposta restrizioni** e selezionare le restrizioni dello schema, selezionare la variabile che contiene il valore della restrizione oppure digitare il valore della restrizione e fare clic su **OK**.  
  
    -   Per usare l'enumeratore Foreach da variabile, selezionare una variabile nell'elenco **Variabile** .  
  
    -   Per usare l'enumeratore Foreach NodeList, fare clic su DocumentSourceType e selezionare il tipo di origine nell'elenco, quindi fare clic su DocumentSource. A seconda del valore selezionato per DocumentSourceType, selezionare una variabile o una connessione file nell'elenco, creare una nuova variabile o connessione file oppure specificare l'origine XML in **Editor origine documento**.  
  
         Fare quindi clic su EnumerationType e selezionare un tipo di enumeratore nell'elenco. Se è EnumerationType è **Navigator, Node o NodeText**, fare clic su OuterXPathStringSourceType e selezionare il tipo di origine, quindi fare clic su OuterXPathString. A seconda del valore impostato per OuterXPathStringSourceType, selezionare una variabile o una connessione file nell'elenco, creare una nuova variabile o connessione file oppure digitare la stringa per l'espressione XPath (XML Path Language) esterna.  
  
         Se EnumerationType è **ElementCollection**, impostare OuterXPathStringSourceType e OuterXPathString come descritto in precedenza. Fare quindi clic su InnerElementType, selezionare un tipo di enumerazione per gli elementi interni e quindi fare clic su InnerXPathStringSourceType. A seconda del valore impostato per InnerXPathStringSourceType, selezionare una variabile o una connessione file, creare una nuova variabile o connessione file oppure digitare la stringa per l'espressione XPath interna.  
  
    -   Per usare l'enumeratore Foreach SMO, selezionare una connessione ADO.NET esistente oppure fare clic su **Nuova connessione** nell'elenco **Connessione** e quindi digitare la stringa da usare oppure fare clic su **Sfoglia**. Se si fa clic su **Sfoglia**, nella finestra di dialogo **Seleziona enumerazione SMO** selezionare il tipo di oggetto da enumerare e il tipo di enumerazione e quindi fare clic su **OK**.  
  
6.  Facoltativamente, fare clic sul pulsante Sfoglia **(...)** nella casella di testo **espressioni** della pagina **raccolta** per creare le espressioni che aggiornano i valori delle proprietà. Per altre informazioni, vedere [Aggiunta o modifica di un'espressione di proprietà](expressions/add-or-change-a-property-expression.md).  
  
    > [!NOTE]  
    >  Le proprietà incluse nell'elenco **Proprietà** variano a seconda dell'enumeratore.  
  
7.  Facoltativamente, fare clic su **Mapping variabili** per eseguire il mapping delle proprietà degli oggetti ai valori della raccolta e quindi eseguire le operazioni seguenti:  
  
    1.  Nell'elenco **variabili** selezionare una variabile oppure fare clic su ** \<nuova variabile>** per creare una nuova variabile.  
  
    2.  Se si aggiunge una nuova variabile, impostarne le proprietà nella finestra di dialogo **Aggiungi variabile** e fare clic su **OK**.  
  
    3.  Se si usa l'enumeratore For Each Item, è possibile aggiornare il valore dell'indice nell'elenco **Indice** .  
  
        > [!NOTE]  
        >  Il valore dell'indice indica la colonna dell'elemento su cui eseguire il mapping alla variabile. Solo l'enumeratore For Each Item può utilizzare un valore di indice diverso da 0.  
  
8.  Facoltativamente, fare clic su **Espressioni** e, nella pagina **Espressioni** , creare espressioni di proprietà per le proprietà del contenitore Ciclo Foreach. Per altre informazioni, vedere [Aggiunta o modifica di un'espressione di proprietà](expressions/add-or-change-a-property-expression.md).  
  
9. Fare clic su **OK**.  
  
## <a name="see-also"></a>Vedi anche  
 [Contenitore Ciclo Foreach](control-flow/foreach-loop-container.md)  
  
  
