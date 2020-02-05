---
title: Destinazione SQL Server Compact Edition | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.sqlservercompactdest.f1
helpviewer_keywords:
- destinations [Integration Services], SQL Server Compact
- SQL Server Compact, destination
- inserting data
ms.assetid: 697742ba-cc14-414d-8187-1845ad0dd99b
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 1a9192e96bb99082b63e4feac451a378eabd8093
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "71298061"
---
# <a name="sql-server-compact-edition-destination"></a>Destinazione SQL Server Compact Edition

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  La destinazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact consente di scrivere dati in database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact.  
  
> [!NOTE]  
>  In un computer a 64 bit è necessario eseguire pacchetti che si connettono a origini dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact in modalità a 32 bit. Il provider [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact usato in [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] per la connessione a origini dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact è disponibile solo nella versione a 32 bit.  
  
 Per configurare la destinazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact, è necessario specificare il nome della tabella in cui la destinazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact inserisce i dati. Il TableName è contenuto nella proprietà personalizzata [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] della destinazione Compact.  
  
 Per connettersi a un'origine dati, questa destinazione usa una gestione connessione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact che specifica il provider OLE DB da usare. Per altre informazioni, vedere [Configurazione della gestione connessione SQL Server Compact Edition](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager.md).  
  
 La destinazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact include la proprietà personalizzata TableName, che può essere aggiornata da un'espressione di proprietà al caricamento del pacchetto. Per altre informazioni, vedere [Espressioni di Integration Services &#40;SSIS&#41;](../../integration-services/expressions/integration-services-ssis-expressions.md), [Utilizzo delle espressioni di proprietà nei pacchetti](../../integration-services/expressions/use-property-expressions-in-packages.md) e [Proprietà personalizzate della destinazione SQL Server Compact Edition](../../integration-services/data-flow/sql-server-compact-edition-destination-custom-properties.md).  
  
 La destinazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact prevede un solo input e non supporta un output degli errori.  
  
## <a name="configuration-of-the-sql-server-compact-edition-destination"></a>Configurazione della destinazione SQL Server Compact Edition  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] o a livello di codice.  
  
 Nella finestra di dialogo **Editor avanzato** sono disponibili le proprietà che è possibile impostare a livello di codice. Per ulteriori informazioni sulle proprietà che è possibile impostare nella finestra di dialogo **Editor avanzato** o a livello di codice, fare clic su uno degli argomenti seguenti:  
  
-   [Proprietà comuni](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Proprietà personalizzate della destinazione SQL Server](../../integration-services/data-flow/sql-server-destination-custom-properties.md)  
  
## <a name="related-tasks"></a>Attività correlate  
 Per altre informazioni su come impostare le proprietà del componente, vedere [Impostazione delle proprietà di un componente del flusso di dati](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Flusso di dati](../../integration-services/data-flow/data-flow.md)  
  
  
