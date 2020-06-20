---
title: Destinazione ADO NET | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.adonetdest.f1
helpviewer_keywords:
- destinations [Integration Services], ADO.NET
- ADO.NET destination
ms.assetid: cb883990-d875-4d8b-b868-45f9f15ebeae
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 56f2a4d85579634c6e5d303c5cde8d766d162d42
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84916891"
---
# <a name="ado-net-destination"></a>Destinazione ADO NET
  La destinazione ADO NET consente di caricare i dati in un'ampia gamma di database compatibili con [!INCLUDE[vstecado](../../includes/vstecado-md.md)]che utilizzano una tabella o una vista di database. È disponibile l'opzione per caricare i dati in una tabella o in una vista esistenti o è possibile creare una nuova tabella e caricare i dati in essa.  
  
 È possibile usare la destinazione ADO NET per connettersi a [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]. La connessione a [!INCLUDE[ssSDS](../../includes/sssds-md.md)] tramite OLE DB non è supportata. Per altre informazioni su [!INCLUDE[ssSDS](../../includes/sssds-md.md)], vedere la pagina relativa alle [linee guida e limitazioni generali (database SQL di Azure)](https://go.microsoft.com/fwlink/?LinkId=248228).  
  
## <a name="troubleshooting-the-ado-net-destination"></a>Risoluzione dei problemi relativi alla destinazione ADO NET  
 È possibile registrare le chiamate eseguite dalla destinazione ADO NET a provider di dati esterni. Questa nuova funzionalità di registrazione può essere utilizzata per risolvere i problemi relativi al salvataggio di dati in origini di dati esterne da parte della destinazione ADO NET. Per registrare le chiamate eseguite dalla destinazione ADO NET a provider di dati esterni, abilitare la registrazione dei pacchetti e selezionare l'evento **Diagnostica** a livello di pacchetto. Per altre informazioni, vedere [Risoluzione dei problemi relativi agli strumenti per l'esecuzione del pacchetto](../troubleshooting/troubleshooting-tools-for-package-execution.md).  
  
## <a name="configuring-the-ado-net-destination"></a>Configurazione della destinazione ADO NET  
 Per connettersi a un'origine dati, questa destinazione utilizza una gestione connessione [!INCLUDE[vstecado](../../includes/vstecado-md.md)] che specifica il provider [!INCLUDE[vstecado](../../includes/vstecado-md.md)] da utilizzare. Per altre informazioni, vedere [Gestione connessione ADO.NET](../connection-manager/ado-net-connection-manager.md).  
  
 Una destinazione ADO NET include i mapping tra le colonne di input e quelle nell'origine dei dati della destinazione. Non è necessario eseguire il mapping delle colonne di input su tutte le colonne di destinazione. Tuttavia, le proprietà di alcune colonne di destinazione possono richiedere il mapping delle colonne di input. In caso contrario, potrebbero verificarsi degli errori. Se ad esempio una colonna di destinazione non consente valori Null, sarà necessario eseguire il mapping di una colonna di input sulla colonna di destinazione. È inoltre necessario che i tipi di dati delle colonne di cui è stato eseguito il mapping siano compatibili. Ad esempio, non è possibile eseguire il mapping di una colonna di input con un tipo di dati stringa su una colonna di destinazione con un tipo di dati numerici se il provider [!INCLUDE[vstecado](../../includes/vstecado-md.md)] non supporta questo mapping.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non supporta l'inserimento di testo nelle colonne il cui tipo di dati è impostato su immagine. Per altre informazioni sui tipi di dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , vedere [Tipi di dati &#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql).  
  
> [!NOTE]  
>  La destinazione ADO NET non supporta l'esecuzione del mapping di una colonna di input il cui tipo è impostato su DT_DBTIME su una colonna del database il cui tipo è impostato su datetime. Per altre informazioni su tutti i tipi di dati [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , vedere [Tipi di dati di Integration Services](integration-services-data-types.md).  
  
 La destinazione ADO NET include un input regolare e un output degli errori.  
  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] o a livello di codice.  
  
 Per altre informazioni sulle proprietà che è possibile impostare nella finestra di dialogo **Editor destinazione ADO NET** , fare clic su uno degli argomenti seguenti:  
  
-   [Editor destinazione ADO NET &#40;pagina Gestione connessione&#41;](../ado-net-destination-editor-connection-manager-page.md)  
  
-   [Editor destinazione ADO NET &#40;pagina Mapping&#41;](../ado-net-destination-editor-mappings-page.md)  
  
-   [Editor destinazione ADO NET &#40;pagina Output degli errori&#41;](../ado-net-destination-editor-error-output-page.md)  
  
 Nella finestra di dialogo **Editor avanzato** sono disponibili le proprietà che è possibile impostare a livello di codice. Per ulteriori informazioni sulle proprietà che è possibile impostare nella finestra di dialogo **Editor avanzato** o a livello di codice, fare clic su uno degli argomenti seguenti:  
  
-   [Proprietà comuni](../common-properties.md)  
  
-   [Proprietà personalizzate ADO NET](ado-net-custom-properties.md)  
  
 Per altre informazioni su come impostare le proprietà, vedere [Impostazione delle proprietà di un componente del flusso di dati](set-the-properties-of-a-data-flow-component.md).  
  
  
