---
description: Origine BLOB di Azure
title: Origine BLOB di Azure | Microsoft Docs
ms.custom: ''
ms.date: 08/20/2018
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.afpblobsrc.f1
- sql14.dts.designer.afpblobsrc.f1
ms.assetid: 80645c5c-88c8-4fb0-8607-de1bb7bffcbb
author: chugugrace
ms.author: chugu
ms.openlocfilehash: ce39fed32923ae46bd499c32d5b58660db5dcd8b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88457483"
---
# <a name="azure-blob-source"></a>Origine BLOB di Azure

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Il componente **Origine Blob di Azure** consente a un pacchetto SSIS di leggere dati da un BLOB di Azure. I formati di file supportati sono CSV e AVRO.
  
  Per visualizzare l'editor per l'origine BLOB di Azure, trascinare la selezione **Origine BLOB di Azure** nell'area di progettazione del flusso di dati e fare doppio clic per aprire l'editor.  
  
 **Origine BLOB di Azure** è un componente del [Feature Pack di SQL Server Integration Services (SSIS) per Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).  
  
1.  Nel campo **Gestione connessione di archiviazione di Azure** specificare un'istanza esistente di Gestione connessioni dell'archiviazione di Azure o creare una nuova istanza che fa riferimento a un account di archiviazione di Azure.  
  
2.  Nel campo **Nome contenitore BLOB** specificare il nome del contenitore BLOB che contiene i file di origine.  
  
3.  Nel campo **Nome BLOB** specificare il percorso per il BLOB.  
  
4.  Nel campo **Formato del file BLOB** selezionare il formato BLOB che si vuole usare **Testo** o **Avro**.  
  
5.  Se il formato del file è **Testo**, è necessario impostare il valore **Carattere delimitatore di colonna**. I delimitatori a più caratteri non sono supportati.

    Selezionare anche **Nomi di colonne nella prima riga di dati** se la prima riga nel file contiene i nomi di colonna.

6.  Se il file è compresso, selezionare **Decomprimi file**.

7.  Se il file è compresso, selezionare il **Tipo di compressione**: **GZIP**, **DEFLATE** oppure **BZIP2**. Si noti che il formato di file ZIP non è supportato.
  
8.  Dopo aver specificato le informazioni di connessione, passare alla pagina **Colonne** per eseguire il mapping delle colonne di origine alle colonne di destinazione per il flusso di dati SSIS.  
  
  
