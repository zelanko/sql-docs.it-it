---
title: Trasformazione Controllo | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.audittrans.f1
- sql13.dts.designer.audittransformation.f1
helpviewer_keywords:
- environment data in packages [Integration Services]
- Audit transformation
ms.assetid: 8c143682-9c81-4150-83d6-1d9678151d37
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 76ce8959e9b9cedb9a1e8a096913a3d6257cfd2d
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "71298021"
---
# <a name="audit-transformation"></a>Controllo - trasformazione

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  La trasformazione Controllo consente di includere nel flusso di dati di un pacchetto informazioni sull'ambiente in cui viene eseguito il pacchetto. Ad esempio, il nome del pacchetto, del computer e dell'operatore può essere aggiunto al flusso di dati. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] include variabili di sistema che forniscono queste informazioni.  
  
## <a name="system-variables"></a>Variabili di sistema  
 Nella tabella seguente sono descritte le variabili di sistema che possono essere utilizzate dalla trasformazione Controllo.  
  
|Variabile di sistema|Indice|Descrizione|  
|---------------------|-----------|-----------------|  
|**ExecutionInstanceGUID**|0|GUID che identifica l'istanza di esecuzione del pacchetto.|  
|**PackageID**|1|Identificatore univoco del pacchetto.|  
|**PackageName**|2|Nome del pacchetto.|  
|**VersionID**|3|Versione del pacchetto.|  
|**ExecutionStartTime**|4|Ora di inizio dell'esecuzione del pacchetto.|  
|**MachineName**|5|Nome del computer.|  
|**UserName**|6|Nome dell'account di accesso dell'utente che ha avviato il pacchetto.|  
|**TaskName**|7|Nome dell'attività Flusso di dati a cui è associata la trasformazione Controllo.|  
|**TaskId**|8|Identificatore univoco dell'attività Flusso di dati.|  
  
## <a name="configuration-of-the-audit-transformation"></a>Configurazione della trasformazione Controllo  
 Per configurare la trasformazione Controllo è necessario specificare il nome di una nuova colonna di output da aggiungere all'output della trasformazione ed eseguire il mapping della variabile di sistema a tale colonna di output. È possibile eseguire il mapping di una stessa variabile di sistema a più colonne di output.  
  
 Questa trasformazione include un input e un output. Non supporta un output degli errori.  
  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../../includes/ssis-md.md)] o a livello di codice.  
  
 Nella finestra di dialogo **Editor avanzato** sono disponibili le proprietà che è possibile impostare a livello di codice. Per ulteriori informazioni sulle proprietà che è possibile impostare nella finestra di dialogo **Editor avanzato** o a livello di codice, fare clic su uno degli argomenti seguenti:  
  
-   [Proprietà comuni](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Proprietà personalizzate delle trasformazioni](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 Per altre informazioni su come impostare le proprietà, vedere [Impostazione delle proprietà di un componente del flusso di dati](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## <a name="audit-transformation-editor"></a>Editor trasformazione Controllo
  La trasformazione Controllo consente di includere nel flusso di dati di un pacchetto informazioni sull'ambiente in cui viene eseguito il pacchetto. Ad esempio, il nome del pacchetto, del computer e dell'operatore può essere aggiunto al flusso di dati. [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] include variabili di sistema che forniscono queste informazioni.  
  
### <a name="options"></a>Opzioni  
 **Nome colonna di output**  
 Consente di specificare il nome di una nuova colonna di output che conterrà le informazioni di controllo.  
  
 **Tipo di controllo**  
 Consente di selezionare una variabile di sistema disponibile per visualizzare le informazioni di controllo.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|**GUID istanza esecuzione**|Consente di specificare il GUID che identifica in modo univoco l'istanza di esecuzione del pacchetto.|  
|**ID pacchetto**|Consente di specificare il GUID che identifica in modo univoco il pacchetto.|  
|**Nome pacchetto**|Consente di specificare il nome del pacchetto.|  
|**ID versione**|Consente di specificare il GUID che identifica in modo univoco la versione del pacchetto.|  
|**Ora di inizio esecuzione**|Consente di specificare l'ora di inizio dell'esecuzione del pacchetto.|  
|**Nome computer**|Consente di specificare il nome del computer sul quale è stato avviato il pacchetto.|  
|**Nome utente**|Consente di specificare il nome dell'account di accesso dell'utente che ha avviato il pacchetto.|  
|**Nome attività**|Consente di specificare il nome dell'attività Flusso di dati a cui è associata la trasformazione Controllo.|  
|**ID attività**|Consente di specificare il GUID che identifica in modo univoco l'attività Flusso di dati a cui è associata la trasformazione Controllo.|  
  
  
