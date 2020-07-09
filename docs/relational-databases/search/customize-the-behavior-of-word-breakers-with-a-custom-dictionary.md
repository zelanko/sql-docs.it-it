---
title: Personalizzare il comportamento dei word breaker con un dizionario personalizzato
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: search, sql-database
ms.technology: search
ms.topic: conceptual
ms.assetid: a8e278d1-aeaa-48f1-a0c6-5de232c983e4
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.custom: seo-lt-2019
ms.openlocfilehash: d9a3f034312dcb6be52534968034fe526cfa5955
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85758067"
---
# <a name="customize-behavior-of-word-breakers-with-a-custom-dictionary-sql-server-search"></a>Personalizzare il comportamento dei word breaker con un dizionario personalizzato (ricerca di SQL Server)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  È possibile personalizzare il comportamento del word breaker per una particolare lingua creando un file del dizionario personalizzato specifico della lingua. Ad esempio, è possibile impedire l'attività del word breaker per determinati termini o modelli.  
  
 Per ulteriori informazioni, vedere il seguente articolo SharePoint:  
  
 [Creare un dizionario personalizzato (SharePoint Server 2010)](https://go.microsoft.com/fwlink/?LinkId=215011)  
  
 Per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], posizionare file del dizionario personalizzato nella seguente cartella:  
  
 `C:\Program Files\Microsoft SQL Server\<instance name>\MSSQL\Binn`  
  
 Dopo aver creato o modificato i file del dizionario personalizzato, riavviare l'Utilità di avvio del Daemon Full-text SQL attraverso il seguente comando:  
  
 `exec sp_fulltext_service 'restart_all_fdhosts'`  
  
  
