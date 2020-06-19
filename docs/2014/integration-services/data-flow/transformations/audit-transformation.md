---
title: Trasformazione Controllo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.audittrans.f1
helpviewer_keywords:
- environment data in packages [Integration Services]
- Audit transformation
ms.assetid: 8c143682-9c81-4150-83d6-1d9678151d37
author: janinezhang
ms.author: janinez
ms.openlocfilehash: daca48b79b4bb0dd4655bb306c881c199ecfb0a7
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84913851"
---
# <a name="audit-transformation"></a>Controllo - trasformazione
  La trasformazione Controllo consente di includere nel flusso di dati di un pacchetto informazioni sull'ambiente in cui viene eseguito il pacchetto. Ad esempio, il nome del pacchetto, del computer e dell'operatore può essere aggiunto al flusso di dati. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] include variabili di sistema che forniscono queste informazioni.  
  
## <a name="system-variables"></a>Variabili di sistema  
 Nella tabella seguente sono descritte le variabili di sistema che possono essere utilizzate dalla trasformazione Controllo.  
  
|Variabile di sistema|Indice|Descrizione|  
|---------------------|-----------|-----------------|  
|`ExecutionInstanceGUID`|0|GUID che identifica l'istanza di esecuzione del pacchetto.|  
|`PackageID`|1|Identificatore univoco del pacchetto.|  
|`PackageName`|2|Nome del pacchetto.|  
|`VersionID`|3|Versione del pacchetto.|  
|`ExecutionStartTime`|4|Ora di inizio dell'esecuzione del pacchetto.|  
|`MachineName`|5|Nome del computer.|  
|`UserName`|6|Nome dell'account di accesso dell'utente che ha avviato il pacchetto.|  
|`TaskName`|7|Nome dell'attività Flusso di dati a cui è associata la trasformazione Controllo.|  
|**TaskId**|8|Identificatore univoco dell'attività Flusso di dati.|  
  
## <a name="configuration-of-the-audit-transformation"></a>Configurazione della trasformazione Controllo  
 Per configurare la trasformazione Controllo è necessario specificare il nome di una nuova colonna di output da aggiungere all'output della trasformazione ed eseguire il mapping della variabile di sistema a tale colonna di output. È possibile eseguire il mapping di una stessa variabile di sistema a più colonne di output.  
  
 Questa trasformazione include un input e un output. Non supporta un output degli errori.  
  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../../includes/ssis-md.md)] o a livello di codice.  
  
 Per ulteriori informazioni sulle proprietà che è possibile impostare nella finestra di dialogo **Editor trasformazione Controllo** , vedere [Audit Transformation Editor](../../audit-transformation-editor.md).  
  
 Nella finestra di dialogo **Editor avanzato** sono disponibili le proprietà che è possibile impostare a livello di codice. Per ulteriori informazioni sulle proprietà che è possibile impostare nella finestra di dialogo **Editor avanzato** o a livello di codice, fare clic su uno degli argomenti seguenti:  
  
-   [Proprietà comuni](../../common-properties.md)  
  
-   [proprietà personalizzate della trasformazione](transformation-custom-properties.md)  
  
 Per altre informazioni su come impostare le proprietà, vedere [Impostazione delle proprietà di un componente del flusso di dati](../set-the-properties-of-a-data-flow-component.md).  
  
  
