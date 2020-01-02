---
title: Importare domini da un file di Excel in individuazione informazioni
description: Informazioni su come importare domini da un file di Excel durante l'individuazione delle informazioni per SQL Server Data Quality Services (DQS)
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 4d3a3940-6c2a-4dc4-90eb-86f26012c165
author: swinarko
ms.author: sawinark
ms.openlocfilehash: 35f5c02e7206c6a9117b31c9ca9b503fb7b6875f
ms.sourcegitcommit: 035ad9197cb9799852ed705432740ad52e0a256d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/31/2019
ms.locfileid: "75557957"
---
# <a name="import-domains-from-an-excel-file-in-knowledge-discovery---data-quality-services-dqs"></a>Importare domini da un file di Excel in individuazione informazioni-Data Quality Services (DQS)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  In questo argomento viene descritto come importare uno o più domini da un file di Excel nell'attività di individuazione delle informazioni di [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS). Il processo di importazione semplifica il processo di generazione delle informazioni, risparmiando tempo e fatica. In questo modo è possibile creare una Knowledge Base con i dati presenti in un file di Excel o in un file di testo. Per ulteriori informazioni sull'importazione di valori in un dominio di una Knowledge Base esistente, vedere [importare i valori da un file di Excel in un dominio](../data-quality-services/import-values-from-an-excel-file-into-a-domain.md) . L'esportazione in un file di Excel non è supportata.  
  
##  <a name="BeforeYouBegin"></a>Prima di iniziare  
  
###  <a name="Prerequisites"></a>Prerequisiti  
 Per importare i domini da un file di Excel, è necessario che Excel sia installato nel computer in cui è installato il [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] . È necessario avere creato un file di Excel con i valori di dominio (vedere [How the import works](#How)). Infine, è necessario avere creato e aperto una Knowledge Base in cui importarvi il dominio.  
  
###  <a name="Security"></a>Sicurezza  
  
####  <a name="Permissions"></a>Autorizzazioni  
 Per importare i domini da un file di Excel, è necessario disporre del ruolo dqs_kb_editor o dqs_administrator nel database DQS_MAIN.  
  
##  <a name="Import"></a>Importare i domini da un file di Excel in una Knowledge base  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][Eseguire l'applicazione Data Quality Client](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Nella schermata iniziale del [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] effettuare una delle operazioni seguenti:  
  
    -   Creare una nuova Knowledge Base in cui eseguire l'importazione facendo clic su **Nuova Knowledge Base**, immettendo un nome per la Knowledge Base, selezionando **Nessuno** per **Crea Knowledge Base da**, selezionando l'attività **Individuazione informazioni** , quindi facendo clic su **Crea**.  
  
    -   Aprire una Knowledge Base esistente in cui eseguire l'importazione facendo clic su **Apri Knowledge Base**, selezionando la Knowledge Base, selezionando **Individuazione informazioni**, quindi facendo clic su **Avanti**.  
  
3.  Nella pagina **Mappa** selezionare **File di Excel** per **Origine dati**.  
  
4.  Fare clic su **Sfoglia** nella riga **File di Excel** .  
  
5.  Nella finestra di dialogo **Seleziona un file di Excel** spostarsi nella cartella che contiene il file di Excel da cui si desidera eseguire l'importazione, selezionare il file di Excel, quindi fare clic su **Apri**.  
  
6.  Nell'elenco a discesa **Foglio di lavoro** selezionare il foglio di lavoro nel file di Excel da cui si desidera eseguire l'importazione.  
  
7.  Selezionare **Utilizza la prima riga come intestazione** se si desidera che la prima riga venga considerata come intestazione di dati e se si desidera che i valori nella prima riga vengano utilizzati come nomi di colonna. Deselezionare **Utilizza la prima riga come intestazione** se si desidera che la prima riga venga considerata come valore di dati. In questo caso verranno utilizzati i nomi di intestazione di Excel (caratteri alfabetici) per la colonna.  
  
8.  Selezionare una colonna, quindi eseguire il mapping di un dominio esistente alla colonna o creare un nuovo dominio facendo clic sull'icona **Crea un dominio** , creando un dominio nella finestra di dialogo **Crea un dominio** e quindi eseguendo il mapping del dominio alla colonna. Il tipo di dati del dominio deve corrispondere al tipo di dati della colonna. Ripetere l'operazione per tutte le colonne del foglio di calcolo.  
  
9. Fare clic su **Avanti**.  
  
10. Nella pagina **Individua** fare clic su **Avvia** per analizzare i dati nel foglio di calcolo di Excel.  
  
    > [!NOTE]  
    >  Se si esce dalla pagina prima della fine del caricamento dei dati, il processo di caricamento del file verrà terminato.  
  
11. Verificare che l'analisi venga completata correttamente, quindi fare clic su **Avanti**.  
  
12. Nella pagina **Gestisci valori di dominio** verificare che i domini corretti siano elencati nell'elenco **Domini** e che i valori siano immessi nella tabella del dominio.  
  
13. Fare clic su **Fine**, quindi su **Pubblica** per pubblicare la Knowledge Base o su **No** per non pubblicarla.  
  
14. Verificare che la Knowledge Base sia stata pubblicata, quindi fare clic su **OK**.  
  
##  <a name="FollowUp"></a>Completamento: fasi successive all'importazione di domini da un file di Excel  
 Dopo avere importato i domini da un file di Excel, è possibile aggiungere informazioni ai domini o utilizzare i domini per un progetto di pulizia o un progetto corrispondente, a seconda del contenuto dei domini. Per altre informazioni, vedere [Eseguire l'individuazione di informazioni](../data-quality-services/perform-knowledge-discovery.md), [Gestione di un dominio](../data-quality-services/managing-a-domain.md), [Gestione di un dominio composito](../data-quality-services/managing-a-composite-domain.md), [Creare criteri di corrispondenza](../data-quality-services/create-a-matching-policy.md), [Pulizia dei dati](../data-quality-services/data-cleansing.md), o [Corrispondenza di dati](../data-quality-services/data-matching.md).  
  
##  <a name="How"></a>Funzionamento dell'importazione  
 Nell'operazione di importazione di DQS un file di Excel viene interpretato come segue:  
  
-   Una colonna rappresenta un dominio.  
  
-   Una riga rappresenta un record di dati.  
  
-   La prima riga rappresenta nomi di dominio o è il primo record o valore di dati, a seconda dell'impostazione della casella di controllo **Utilizza la prima riga come intestazione** .  
  
 All'operazione di importazione vengono applicate le regole seguenti:  
  
-   Con questa operazione vengono importati i valori di dominio in una Knowledge Base. Non vengono importati regole di dominio o criteri di corrispondenza.  
  
-   L'estensione del file di Excel può essere XLSX, XLS o CSV. È necessario che Microsoft Excel sia installato nel computer del [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] per poter importare i valori di dominio o un dominio completo. Sono supportate le versioni di Excel dalla 2003 in poi. Se viene utilizzata la versione a 64 bit di Excel, sono supportati solo i file di Excel 2003, mentre non sono supportati i file di Excel 2007 o 2010.  
  
-   I file di Excel di tipo XLSX non sono supportati per un'installazione di Excel a 64 bit. Se si utilizza Excel a 64 bit, salvare il file del foglio di calcolo come file XLS.  
  
-   Nei file XLSX e XLS il tipo di dati della colonna viene determinato dal tipo di dati più prevalente nelle prime otto righe. Se una cella non è conforme a tale tipo di dati, verrà fornito un valore Null.  
  
-   Nei file CSV il tipo di dati viene determinato dal tipo di dati più prevalente nelle prime otto righe.  
  
-   Un valore in un foglio di calcolo di Excel che non soddisfa una regola di dominio verrà importato come valore non valido.  
  
-   Se il formato del file di Excel non è corretto o è danneggiato, l'operazione di importazione genererà un errore.  
  
  
