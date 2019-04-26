---
title: Personalizzare il comportamento dei word breaker con un dizionario personalizzato | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: search, sql-database
ms.technology: search
ms.topic: conceptual
ms.assetid: a8e278d1-aeaa-48f1-a0c6-5de232c983e4
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: ff74b4583c8f730fbee1dacb35b895049084db19
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62631808"
---
# <a name="customize-the-behavior-of-word-breakers-with-a-custom-dictionary"></a>Personalizzare Comportamento di word breaker con un dizionario personalizzato
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  È possibile personalizzare il comportamento del word breaker per una particolare lingua creando un file del dizionario personalizzato specifico della lingua. Ad esempio, è possibile impedire l'attività del word breaker per determinati termini o modelli.  
  
 Per ulteriori informazioni, vedere il seguente articolo SharePoint:  
  
 [Creare un dizionario personalizzato (SharePoint Server 2010)](https://go.microsoft.com/fwlink/?LinkId=215011)  
  
 Per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], posizionare file del dizionario personalizzato nella seguente cartella:  
  
 `C:\Program Files\Microsoft SQL Server\<instance name>\MSSQL\Binn`  
  
 Dopo aver creato o modificato i file del dizionario personalizzato, riavviare l'Utilità di avvio del Daemon Full-text SQL attraverso il seguente comando:  
  
 `exec sp_fulltext_service 'restart_all_fdhosts'`  
  
  
