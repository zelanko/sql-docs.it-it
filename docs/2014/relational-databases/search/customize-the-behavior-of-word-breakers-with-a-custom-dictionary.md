---
title: Personalizzare il comportamento dei word breaker con un dizionario personalizzato | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
ms.assetid: a8e278d1-aeaa-48f1-a0c6-5de232c983e4
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 9fb02a47da20134925d9b2486ea0c08091af4aa6
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85055511"
---
# <a name="customize-the-behavior-of-word-breakers-with-a-custom-dictionary"></a>Personalizzare Comportamento di word breaker con un dizionario personalizzato
  È possibile personalizzare il comportamento del word breaker per una particolare lingua creando un file del dizionario personalizzato specifico della lingua. Ad esempio, è possibile impedire l'attività del word breaker per determinati termini o modelli.  
  
 Per ulteriori informazioni, vedere il seguente articolo SharePoint:  
  
 [Creare un dizionario personalizzato (SharePoint Server 2010)](https://go.microsoft.com/fwlink/?LinkId=215011)  
  
 Per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], posizionare file del dizionario personalizzato nella seguente cartella:  
  
 `C:\Program Files\Microsoft SQL Server\<instance name>\MSSQL\Binn`  
  
 Dopo aver creato o modificato i file del dizionario personalizzato, riavviare l'Utilità di avvio del Daemon Full-text SQL attraverso il seguente comando:  
  
 `exec sp_fulltext_service 'restart_all_fdhosts'`  
  
  
