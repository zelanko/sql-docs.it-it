---
title: Impostazioni progetto (Mapping di tipo) (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 2698fb3a-f9e6-4e04-94e0-dad289d7ed0a
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: d7b16bdf3717fa14f91af41663cbd65365eac52a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68028666"
---
# <a name="project-settings-type-mapping-sybasetosql"></a>Impostazioni del progetto (mapping dei tipi) (SybaseToSQL)
La pagina del mapping dei tipi dei **impostazioni del progetto** finestra di dialogo contiene impostazioni che Personalizza modalità di conversione di tipi di dati di Sybase Adaptive Server Enterprise (ASE) in SSMA [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] i tipi di dati.  
  
La pagina del mapping dei tipi è disponibile nel **impostazioni del progetto** e **impostazioni di progetto predefinite** finestre di dialogo.  
  
-   Per specificare le impostazioni di mapping di tipo per tutti i progetti SSMA futuri, nel **degli strumenti** dal menu **impostazioni di progetto predefinite**, selezionare tipo di progetto di migrazione per i quali impostazioni sono necessarie per essere visualizzati o modificato da **versione di destinazione della migrazione** elenco a discesa e quindi selezionare **mapping tra i tipi** nella parte inferiore del riquadro di sinistra.  
  
-   Per specificare le impostazioni per il progetto corrente, il **strumenti** dal menu **le impostazioni del progetto**e quindi selezionare **mapping tra i tipi** nella parte inferiore del riquadro di sinistra.  
  
## <a name="options"></a>Opzioni  
**Tipo origine**  
Il tipo di dati di ambiente del servizio App connessa.  
  
**Tipo di destinazione**  
La destinazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo di dati per il tipo di dati di ambiente del servizio App specificato.  
  
Vedere la tabella nella sezione seguente per il valore predefinito SSMA per Sybase mapping dei tipi.  
  
**Aggiungi**  
Fare clic per aggiungere un tipo di dati all'elenco di mapping.  
  
**Modifica**  
Fare clic per modificare il tipo di dati selezionato nell'elenco di mapping.  
  
**Rimuovi**  
Fare clic per rimuovere il mapping dei tipi di dati selezionato dall'elenco di mapping.  
  
**Ripristina predefiniti**  
Fare clic per reimpostare l'elenco di mapping di tipo ai valori predefiniti di SSMA.  
  
## <a name="default-type-mapping"></a>Mapping dei tipi predefiniti  
Nella tabella seguente contiene il mapping dei tipi predefiniti tra l'ambiente del servizio App e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] i tipi di dati.  
  
|Tipo di dati di ambiente del servizio App|Tipo di dati di SQL Server|  
|-----------------|------------------------|  
|**bigint**|**bigint**|  
|**binary**|**binary**|  
|**binario [\*.. 8000]**|**binary[\*]**|  
|**binary[8001..\*]**|**varbinary(max)**|  
|**bit**|**bit**|  
|**char**|**char**|  
|**char varying**|**varchar**|  
|**Char varying [\*.. 8000]**|**varchar[\*]**|  
|**Char varying [8001 e..\*]**|**ntext**|  
|**char[\*..8000]**|**char[\*]**|  
|**char[8001..\*;]**|**ntext**|  
|**character**|**char**|  
|**variabili di carattere**|**varchar**|  
|**variabili di carattere [\*.. 8000]**|**varchar[\*]**|  
|**variabili di carattere [8001 e..\*]**|**ntext**|  
|**caratteri [\*.. 8000]**|**char[\*]**|  
|**caratteri [8001 e..\*]**|**ntext**|  
|**data**|**data**|  
|**datetime**|**datetime2 [3]**|  
|**DEC**|**decimal**|  
|**dec[\*..\*]**|**decimale [\*]**|  
|**dec[\*..\*][\*..\*]**|**decimal[\*][\*]**|  
|**decimal**|**decimal**|  
|**decimale [\*.. \*]**|**decimale [\*]**|  
|**decimal[\*..\*][\*..\*]**|**decimal[\*][\*]**|  
|**valore a precisione doppia**|**float [53]**|  
|**float**|**float [53]**|  
|**float[\*..15]**|**float[24]**|  
|**float[16..\*]**|**float [53]**|  
|**image**|**image**|  
|**int**|**int**|  
|**integer**|**int**|  
|**longsysname**|**nvarchar[255]**|  
|**money**|**money**|  
|**National char**|**nchar**|  
|**National char [\*.. 4000]**|**nchar[\*]**|  
|**National char varying**|**nvarchar**|  
|**National char varying [\*.. 4000]**|**nvarchar[\*]**|  
|**National char varying [4001..\*]**|**nvarchar(max)**|  
|**National char [4001..\*]**|**nvarchar(max)**|  
|**caratteri nazionali**|**nchar**|  
|**caratteri nazionali [\*.. 4000]**|**nchar[\*]**|  
|**caratteri nazionali [4001..\*]**|**nvarchar(max)**|  
|**variabile di caratteri nazionali**|**nvarchar**|  
|**variabile di caratteri nazionali [\*.. 4000]**|**nvarchar[\*]**|  
|**variabile di caratteri nazionali [4001..\*]**|**nvarchar(max)**|  
|**varchar nazionali**|**nvarchar**|  
|**varchar National [\*.. 4000]**|**nvarchar[\*]**|  
|**varchar National [4001..\*]**|**nvarchar(max)**|  
|**nchar**|**nchar**|  
|**nchar varying**|**nvarchar**|  
|**nchar varying [\*.. 4000]**|**nvarchar[\*]**|  
|**nchar varying [4001..\*]**|**nvarchar(max)**|  
|**nchar[\*..4000]**|**nchar[\*]**|  
|**nchar[4001..\*]**|**nvarchar(max)**|  
|**numeric**|**numeric**|  
|**numeric[\*..\*]**|**numeric[\*]**|  
|**numeric[\*..\*][\*..\*]**|**numeric[\*][\*]**|  
|**nvarchar**|**nvarchar**|  
|**nvarchar [\*.. 4000]**|**nvarchar[\*]**|  
|**nvarchar[4001..\*]**|**nvarchar(max)**|  
|**real**|**float[24]**|  
|**smalldatetime**|**smalldatetime**|  
|**smallint**|**smallint**|  
|**smallmoney**|**smallmoney**|  
|**sysname**|**nvarchar[128]**|  
|**sysname[\*..\*]**|**nvarchar[255]**|  
|**text**|**text**|  
|**time**|**tempo [3]**|  
|**timestamp**|**rowversion**|  
|**tinyint**|**tinyint**|  
|**unichar**|**nchar**|  
|**UNICHAR varying**|**nvarchar**|  
|**UNICHAR varying [\*.. 4000]**|**nvarchar[\*]**|  
|**UNICHAR varying [4001..\*]**|**nvarchar(max)**|  
|**unichar[\*..4000]**|**nchar[\*]**|  
|**unichar[4001..\*]**|**nvarchar(max)**|  
|**unitext**|**nvarchar(max)**|  
|**univarchar**|**nvarchar**|  
|**univarchar[\*..4000]**|**nvarchar[\*]**|  
|**univarchar[4001..\*]**|**nvarchar(max)**|  
|**bigint senza segno**|**numerico [20] [0]**|  
|**unsigned int**|**bigint**|  
|**smallint non firmati**|**int**|  
|**tinyint non firmati**|**tinyint**|  
|**varbinary**|**varbinary**|  
|**varbinary [\*.. 8000]**|**varbinary[\*]**|  
|**varbinary[8001..\*]**|**varbinary(max)**|  
|**varchar**|**varchar**|  
|**varchar[\*..8000]**|**varchar[\*]**|  
|**varchar[8001..\*]**|**ntext**|  
  
