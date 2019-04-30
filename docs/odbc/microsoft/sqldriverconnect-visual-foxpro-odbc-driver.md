---
title: SQLDriverConnect (Driver ODBC Visual FoxPro) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLDriverConnect function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 10492c8f-3a18-4971-9db8-879e878083b9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dc0bcf6a191f67b87b422b17778f56feda1f5227
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63238083"
---
# <a name="sqldriverconnect-visual-foxpro-odbc-driver"></a>SQLDriverConnect (driver ODBC Visual FoxPro)
> [!NOTE]  
>  In questo argomento contiene informazioni specifiche del Driver ODBC Visual FoxPro. Per informazioni generali su questa funzione, vedere l'argomento appropriato nel [riferimento all'API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Supporto: Full  
  
 Conformità di API ODBC: Livello 1  
  
 Si connette a un'origine dati esistente, che può essere un' [database](../../odbc/microsoft/visual-foxpro-terminology.md) o una directory di [libero tabelle](../../odbc/microsoft/visual-foxpro-terminology.md). Vengono ignorate le parole chiave attributo ODBC UID e PWD. La tabella seguente elenca le parole chiave di attributo supportati aggiuntivo.  
  
|Parola chiave di attributo ODBC|Valore di attributo|  
|----------------------------|---------------------|  
|DSN||  
|UID|Ignorato dal Driver ODBC Visual FoxPro, ma non genera un errore.|  
|PWD|Ignorato dal Driver ODBC Visual FoxPro, ma non genera un errore.|  
|Driver|Il nome e il percorso del Driver ODBC Visual FoxPro; implementata da Gestione Driver.|  
  
|Parola chiave di attributo Visual FoxPro ODBC Driver|Valore di attributo|  
|-------------------------------------------------|---------------------|  
|BackgroundFetch|"Sì" o "No"|  
|Fascicola|"Macchina" o altre sequenze di collazione. Per un elenco di sequenze di collazione supportati, vedere [SET COLLATE](../../odbc/microsoft/set-collate-command.md).|  
|Descrizione||  
|Exclusive|"Sì" o "No"|  
|SourceDB|Il percorso completo alla directory contenente zero o più [libero tabelle](../../odbc/microsoft/visual-foxpro-terminology.md), o il nome di file e percorso assoluto per un [database](../../odbc/microsoft/visual-foxpro-terminology.md).|  
|SourceType|"DBC" o "DBF"|  
|Version||  
  
 Se non viene specificato il nome dell'origine dati, gestione Driver richiede all'utente le informazioni (a seconda dell'impostazione delle *fDriverCompletion* argomento) e quindi prosegue. Se sono necessarie ulteriori informazioni, il Driver ODBC Visual FoxPro consente di visualizzare la finestra di dialogo dei messaggi di richiesta.  
  
 Per altre informazioni, vedere [SQLDriverConnect](../../odbc/reference/syntax/sqldriverconnect-function.md) nel *riferimento per programmatori ODBC*.
