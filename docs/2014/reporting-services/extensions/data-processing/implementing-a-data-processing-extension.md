---
title: Implementazione di un'estensione per l'elaborazione dati | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- custom data processing extensions [Reporting Services]
- data sources [Reporting Services], data processing extensions
- data processing extensions [Reporting Services]
- extensions [Reporting Services], data processing
ms.assetid: 8dc2b44e-5ad9-411d-a29f-7213e29321a9
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 2efc74fa2ba84335fcb5e03b42125fb9c6782f43
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "63164115"
---
# <a name="implementing-a-data-processing-extension"></a>Implementazione di un'estensione per l'elaborazione dati
  Le estensioni per l'elaborazione dati in [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] consentono di eseguire la connessione a un'origine dati e di recuperare i dati. Fungono inoltre da ponte tra un'origine dati e un set di dati. [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]le [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] estensioni per l'elaborazione dati vengono modellate dopo un subset delle interfacce del provider di dati.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
 [Cenni preliminari sulle estensioni per l'elaborazione dati](data-processing-extensions-overview.md)  
 Vengono fornite informazioni introduttive per la scrittura di un'estensione per l'elaborazione dati per [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)].  
  
 [Preparazione all'implementazione di un'estensione per l'elaborazione dati](preparing-to-implement-a-data-processing-extension.md)  
 Vengono descritte le interfacce disponibili quando si implementa un'estensione per l'elaborazione dati di [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] e vengono indicati i casi in cui è necessario implementare un'interfaccia specifica.  
  
 [Creazione di una libreria di estensioni per l'elaborazione dati](creating-a-data-processing-extension-library.md)  
 Vengono descritte le operazioni di assegnazione di uno spazio dei nomi per l'estensione per l'elaborazione dati di [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] e di compilazione dell'estensione per l'elaborazione dati nella DLL di una libreria.  
  
 [Implementazione di una classe Connection per un'estensione per l'elaborazione dati](implementing-a-connection-class-for-a-data-processing-extension.md)  
 Vengono descritti gli attributi di una connessione e come implementare una classe **Connection** personalizzata per l'estensione per l'elaborazione dati.  
  
 [Implementazione di una classe Command per un'estensione per l'elaborazione dati](implementing-a-command-class-for-a-data-processing-extension.md)  
 Vengono descritti gli attributi di un comando e come implementare una classe **Command** personalizzata per l'estensione per l'elaborazione dati.  
  
 [Implementazione di una classe DataReader per un'estensione per l'elaborazione dati](implementing-a-datareader-class-for-a-data-processing-extension.md)  
 Vengono descritti gli attributi di un lettore di dati e come implementare una classe **DataReader** personalizzata per l'estensione per l'elaborazione dati.  
  
 [Utilizzo di un set di dati esterno con Reporting Services](using-an-external-dataset-with-reporting-services.md)  
 Viene descritto come esporre gli oggetti **DataSet** personalizzati nel server di report per l'uso.  
  
 [Distribuzione di un'estensione per l'elaborazione dati](deploying-a-data-processing-extension.md)  
 Viene descritto come distribuire un'estensione per l'elaborazione dati.  
  
 [Debug del codice di un'estensione per l'elaborazione dati](debugging-data-processing-extension-code.md)  
 Viene descritto come eseguire il debug del codice nelle estensioni per l'elaborazione dati.  
  
 [Rimozione di un'estensione per l'elaborazione dati](removing-a-data-processing-extension.md)  
 Viene descritto come rimuovere un'estensione per l'elaborazione dati da un server di report o da Progettazione report.  
  
 Per un esempio di estensione per l'elaborazione dati completamente implementata, vedere la pagina degli [esempi del prodotto SQL Server Reporting Services](https://go.microsoft.com/fwlink/?LinkId=177889).  
  
## <a name="see-also"></a>Vedere anche  
 [Estensioni di Reporting Services](../reporting-services-extensions.md)   
 [Libreria di estensioni di Reporting Services](../reporting-services-extension-library.md)  
  
  
