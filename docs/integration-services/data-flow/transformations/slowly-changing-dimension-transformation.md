---
title: Trasformazione Dimensione a modifica lenta | Microsoft Docs
ms.custom: ''
ms.date: 08/31/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.slowlychangingdimtrans.f1
helpviewer_keywords:
- Slowly Changing Dimension transformation
- slowly changing dimensions
- SCD transformation
- updating slowly changing dimensions
ms.assetid: f8849151-c171-4725-bd25-f2c33a40f4fe
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 1fd5584a5c43762c4d732c677de225436e191a7e
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "71297806"
---
# <a name="slowly-changing-dimension-transformation"></a>Dimensione a modifica lenta - trasformazione

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  La trasformazione Dimensione a modifica lenta consente di coordinare l'aggiornamento e l'inserimento dei record nelle tabelle delle dimensioni dei data warehouse. È ad esempio possibile usare questa trasformazione per configurare gli output che inseriscono e aggiornano i record nella tabella DimProduct del database [!INCLUDE[ssSampleDBDWobject](../../../includes/sssampledbdwobject-md.md)] con i dati della tabella Production.Products del database OLTP AdventureWorks.  
  
> [!IMPORTANT]  
>  La Configurazione guidata dimensioni a modifica lenta supporta solo le connessioni a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 La trasformazione Dimensione a modifica lenta fornisce le funzionalità seguenti per la gestione delle dimensioni a modifica lenta:  
  
-   Confronto tra le righe in ingresso e le righe presenti nella tabella di ricerca per distinguere tra righe nuove e righe esistenti.  
  
-   Identificazione delle righe in ingresso contenenti modifiche quando le modifiche non sono consentite.  
  
-   Identificazione dei record dei membri derivati che richiedono un aggiornamento.  
  
-   Identificazione delle righe in ingresso contenenti modifiche cronologiche che richiedono l'inserimento di nuovi record e l'aggiornamento dei record scaduti.  
  
-   Rilevamento delle righe in ingresso contenenti modifiche che richiedono l'aggiornamento dei record esistenti, compresi quelli scaduti.  
  
 La trasformazione Dimensione a modifica lenta supporta quattro tipi di modifiche: Attributo modificabile, Attributo cronologico, Attributo fisso e Membro derivato.  
  
-   Le modifiche di tipo Attributo modificabile sovrascrivono i record esistenti. Questo tipo di modifica è equivalente a una modifica di tipo 1. La trasformazione Dimensione a modifica lenta invia queste righe a un output denominato **Output aggiornamenti attributi modificabili**.  
  
-   Le modifiche di tipo Attributo cronologico creano nuovi record anziché aggiornare quelli esistenti. L'unica modifica consentita in un record esistente è l'aggiornamento di una colonna che indica se il record è aggiornato o scaduto. Questo tipo di modifica è equivalente a una modifica di tipo 2. La trasformazione Dimensione a modifica lenta invia queste righe a due output: **Output inserimenti attributo cronologico** e **Nuovo output**.  
  
-   Le modifiche di tipo Attributo fisso indicano che il valore della colonna non deve essere modificato. La trasformazione Dimensione a modifica lenta rileva le modifiche e può inviare le righe modificate a un output denominato **Output attributo fisso**.  
  
-   Membro derivato indica che la riga è un record membro derivato nella tabella delle dimensioni. Un membro derivato esiste quando una tabella dei fatti fa riferimento a un membro della dimensione non ancora caricato. In attesa di dati di dimensione rilevanti, che verranno forniti in un caricamento successivo, viene creato un record membro derivato minimo. La trasformazione Dimensione a modifica lenta invia queste righe a un output denominato **Output aggiornamenti membro derivato**. Dopo il caricamento dei dati relativi al membro derivato, sarà possibile aggiornare il record esistente anziché crearne uno nuovo.  
  
> [!NOTE]  
>  La trasformazione Dimensione a modifica lenta non supporta modifiche di tipo 3, che richiedono la modifica della tabella delle dimensioni. Identificando le colonne con il tipo di aggiornamento Attributo fisso, è possibile acquisire i valori dei dati che possono subire modifiche di tipo 3.  
  
 In fase di esecuzione la trasformazione Dimensione a modifica lenta cerca innanzitutto una corrispondenza tra la riga in ingresso e un record nella tabella di ricerca. Se non viene trovata alcuna corrispondenza, significa che la riga in ingresso è un nuovo record. In questo caso la trasformazione Dimensione a modifica lenta non esegue altre operazioni e invia la riga a **Nuovo output**.  
  
 Quando viene trovata una corrispondenza, la trasformazione Dimensione a modifica lenta verifica invece se sono presenti eventuali modifiche. Se la riga contiene modifiche, verrà identificato il tipo di aggiornamento eseguito sulle varie colonne e la riga verrà inviata a **Output aggiornamenti attributi modificabili**, **Output attributo fisso**, **Output inserimenti attributo cronologico**o **Output aggiornamenti membro derivato**. Se la riga non contiene modifiche, verrà inviata a **Output non modificato**.  
  
## <a name="slowly-changing-dimension-transformation-outputs"></a>Output della trasformazione Dimensione a modifica lenta  
 La trasformazione Dimensione a modifica lenta utilizza un solo input e un massimo di sei output. Un output indirizza una riga al subset del flusso di dati che corrisponde ai requisiti di aggiornamento e inserimento della riga. Questa trasformazione non supporta un output degli errori.  
  
 Nella tabella seguente vengono descritti gli output della trasformazione e i requisiti dei flussi di dati successivi. I requisiti descrivono il flusso di dati creato dalla Configurazione guidata dimensioni a modifica lenta.  
  
|Output|Descrizione|Requisiti del flusso di dati|  
|------------|-----------------|----------------------------|  
|**Output aggiornamenti attributi modificabili**|Il record nella tabella di ricerca è stato aggiornato. Questo output viene utilizzato per le righe con attributi modificabili.|Una trasformazione Comando OLE DB aggiorna il record utilizzando un'istruzione UPDATE.|  
|**Output attributo fisso**|Per i valori nelle righe che non devono essere modificate non esiste alcuna corrispondenza con i valori nella tabella di ricerca. Questo output viene utilizzato per le righe con attributi fissi.|Non viene creato alcun flusso di dati predefinito. Se la trasformazione è configurata in modo da continuare anche in caso di rilevamento di modifiche alle colonne con attributi fissi, sarà necessario creare un flusso di dati che acquisisca tali righe.|  
|**Output inserimenti attributo cronologico**|La tabella di ricerca contiene almeno una riga corrispondente. La riga contrassegna come "corrente" viene ora contrassegnata come "scaduta". Questo output viene utilizzato per le righe con attributi cronologici.|Le trasformazioni Colonna derivata creano colonne per gli indicatori di riga scaduta e di riga corrente. Una trasformazione del comando OLE DB aggiorna il record che ora deve essere contrassegnato come "scaduto". La riga con i valori della colonna nuovi è indirizzata a Nuovo Output, dove viene inserita e contrassegna come "corrente".|  
|**Output aggiornamenti membro derivato**|Vengono inserite righe per membri di dimensione derivati. Questo output viene utilizzato per le righe dei membri derivati.|Una trasformazione Comando OLE DB aggiorna il record utilizzando un'istruzione SQL UPDATE.|  
|**Nuovo output**|La tabella di ricerca non contiene righe corrispondenti. La riga viene aggiunta alla tabella delle dimensioni. Questo output viene utilizzato per le nuove righe e per le modifiche alle righe con attributi cronologici.|Una trasformazione Colonna derivata imposta l'indicatore di riga corrente e una destinazione OLE DB inserisce la riga.|  
|**Output non modificato**|I valori nella tabella di ricerca corrispondono a quelli della riga. Questo output viene utilizzato per le righe non modificate.|Non viene creato alcun flusso di dati perché la trasformazione Dimensione a modifica lenta non esegue alcuna operazione. Se si desidera acquisire queste righe, sarà necessario creare un flusso di dati per questo output.|  
  
## <a name="business-keys"></a>Chiavi business  
 La trasformazione Dimensione a modifica lenta richiede almeno una colonna chiave business.  
  
 La trasformazione Dimensione a modifica lenta non supporta chiavi business Null. Se i dati includono righe in cui la colonna chiave business è Null, tali righe dovranno essere rimosse dal flusso di dati. Per filtrare le righe con colonne chiave business contenenti valori Null, è possibile utilizzare la trasformazione Suddivisione condizionale. Per altre informazioni, vedere [Trasformazione Suddivisione condizionale](../../../integration-services/data-flow/transformations/conditional-split-transformation.md).  
  
## <a name="optimizing-the-performance-of-the-slowly-changing-dimension-transformation"></a>Ottimizzazione delle prestazioni della trasformazione di dimensioni a modifica lenta  
 Per suggerimenti sul miglioramento delle prestazioni della trasformazione Dimensione a modifica lenta, vedere [Funzionalità delle prestazioni del flusso di dati](../../../integration-services/data-flow/data-flow-performance-features.md).  
  
## <a name="troubleshooting-the-slowly-changing-dimension-transformation"></a>Risoluzione dei problemi relativi alla trasformazione Dimensione a modifica lenta  
 È possibile registrare le chiamate eseguite dalla trasformazione dimensioni a modifica lenta in provider di dati esterni. Questa nuova funzionalità di registrazione può essere utilizzata per risolvere i problemi relativi a connessioni, comandi e query a origini di dati esterne eseguiti dalla trasformazione dimensioni a modifica lenta. Per registrare le chiamate eseguite dalla trasformazione Dimensione a modifica lenta a provider di dati esterni, abilitare la registrazione dei pacchetti e selezionare l'evento **Diagnostic** a livello del pacchetto. Per altre informazioni, vedere [Risoluzione dei problemi relativi agli strumenti per l'esecuzione del pacchetto](../../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md).  
  
## <a name="configuring-the-slowly-changing-dimension-transformation"></a>Configurazione della trasformazione Dimensione a modifica lenta  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../../includes/ssis-md.md)] o a livello di codice.  
  
 Per ulteriori informazioni sulle proprietà che è possibile impostare nella finestra di dialogo **Editor avanzato** o a livello di codice, fare clic su uno degli argomenti seguenti:  
  
-   [Proprietà comuni](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Proprietà personalizzate delle trasformazioni](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 Per altre informazioni su come impostare le proprietà, vedere [Impostazione delle proprietà di un componente del flusso di dati](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## <a name="configuring-the-slowly-changing-dimension-transformation-outputs"></a>Configurazione degli output della trasformazione Dimensione a modifica lenta  
 Il coordinamento dell'aggiornamento e dell'inserimento dei record nelle tabelle delle dimensioni può risultare complesso, soprattutto se vengono utilizzate sia modifiche di tipo 1 che di tipo 2. [!INCLUDE[ssIS](../../../includes/ssis-md.md)] La finestra di progettazione offre due modi per configurare il supporto delle dimensioni a modifica lenta:  
  
-   Usare la finestra di dialogo **Editor avanzato** , in cui è necessario selezionare una connessione, impostare le proprietà di componenti comuni e personalizzati, scegliere le colonne di input e impostare le proprietà delle colonne dei sei output. Per completare la configurazione del supporto di una dimensione a modifica lenta, è necessario creare manualmente il flusso di dati per gli output utilizzati dalla trasformazione Dimensione a modifica lenta. Per altre informazioni, vedere [Flusso di dati](../../../integration-services/data-flow/data-flow.md).  
  
-   Utilizzare Caricamento guidato dimensione, che semplifica la configurazione della trasformazione Dimensione a modifica lenta e compila il flusso di dati per gli output della trasformazione. Per modificare la configurazione delle dimensioni a modifica lenta, eseguire nuovamente il Caricamento guidato dimensione. Per altre informazioni, vedere [Configurazione degli output tramite Configurazione guidata dimensioni a modifica lenta](../../../integration-services/data-flow/transformations/configure-outputs-using-the-slowly-changing-dimension-wizard.md).  
  
## <a name="related-tasks"></a>Attività correlate  
 [Impostazione delle proprietà di un componente del flusso di dati](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
## <a name="related-content"></a>Contenuto correlato  
  
-   [Gestione delle dimensioni a modifica lenta in SSIS](https://techcommunity.microsoft.com/t5/SQL-Server-Integration-Services/Handling-Slowly-Changing-Dimensions-in-SSIS/ba-p/387599)
-   [Ottimizzazione della Configurazione guidata dimensioni a modifica lenta](https://techcommunity.microsoft.com/t5/SQL-Server-Integration-Services/Optimizing-the-Slowly-Changing-Dimension-Wizard/ba-p/387702)
  
  
