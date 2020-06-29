---
title: Destinazione SQL Server Compact Edition | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.sqlservercompactdest.f1
helpviewer_keywords:
- destinations [Integration Services], SQL Server Compact
- SQL Server Compact, destination
- inserting data
ms.assetid: 697742ba-cc14-414d-8187-1845ad0dd99b
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 09b4e23d6d31ff580d7b8515c0604d06efb41c02
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/26/2020
ms.locfileid: "85437708"
---
# <a name="sql-server-compact-edition-destination"></a>Destinazione SQL Server Compact Edition
  La destinazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact consente di scrivere dati in database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact.  
  
> [!NOTE]  
>  In un computer a 64 bit è necessario eseguire pacchetti che si connettono a origini dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact in modalità a 32 bit. Il provider [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact usato in [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] per la connessione a origini dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact è disponibile solo nella versione a 32 bit.  
  
 Per configurare la destinazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact, è necessario specificare il nome della tabella in cui la destinazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact inserisce i dati. Il TableName è contenuto nella proprietà personalizzata [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] della destinazione Compact.  
  
 Per connettersi a un'origine dati, questa destinazione usa una gestione connessione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact che specifica il provider OLE DB da usare. Per altre informazioni, vedere [Configurazione della gestione connessione SQL Server Compact Edition](../connection-manager/sql-server-compact-edition-connection-manager.md).  
  
 La destinazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact include la proprietà personalizzata TableName, che può essere aggiornata da un'espressione di proprietà al caricamento del pacchetto. Per altre informazioni, vedere [Espressioni di Integration Services &#40;SSIS&#41;](../expressions/integration-services-ssis-expressions.md), [Utilizzo delle espressioni di proprietà nei pacchetti](../expressions/use-property-expressions-in-packages.md) e [Proprietà personalizzate della destinazione SQL Server Compact Edition](sql-server-compact-edition-destination-custom-properties.md).  
  
 La destinazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact prevede un solo input e non supporta un output degli errori.  
  
## <a name="configuration-of-the-sql-server-compact-edition-destination"></a>Configurazione della destinazione SQL Server Compact Edition  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] o a livello di codice.  
  
 Nella finestra di dialogo **Editor avanzato** sono disponibili le proprietà che è possibile impostare a livello di codice. Per ulteriori informazioni sulle proprietà che è possibile impostare nella finestra di dialogo **Editor avanzato** o a livello di codice, fare clic su uno degli argomenti seguenti:  
  
-   [Proprietà comuni](../common-properties.md)  
  
-   [Proprietà personalizzate della destinazione SQL Server](sql-server-destination-custom-properties.md)  
  
## <a name="related-tasks"></a>Attività correlate  
 Per altre informazioni su come impostare le proprietà del componente, vedere [Impostazione delle proprietà di un componente del flusso di dati](set-the-properties-of-a-data-flow-component.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Flusso di dati](data-flow.md)  
  
  
